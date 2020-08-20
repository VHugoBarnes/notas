# 1.2 La estructura de un compilador

De momento, al compilador se le ha tratado como una caja simple que mapea un programa fuente a un programa destino con equivalencia semántica. Si lo analisamos un poco, nos damos cuenta que existen dos procesos en esta asignación: **análisis** y **síntesis**.   

El **análisis**: Divide el programa fuente en componentes e impone una estructura gramatical sobre ellas. Después esta estructura la utiliza para crear una representación intermedia del programa fuente. Si se detecta que el programa fuente está mal formado en cuanto a la sintaxis, o que no tiene una semantica consistente, entonces debe proporcionar mensajes informativos para que el usuario pueda corregirlo. La parte del análisis también recolecta información sobre el programa fuente y almacena una estructura de datos llamada **_tabla de símbolos_**, la cual se pasa junto con la representación intermedia a la parte de la síntesis.   

La **síntesis**: Construye el programa destino deseado a partir de la representación intermedia y de la información en la tabla de símbolos.

> A la parte del análisis se le llama comunmente _frontend_ y a la parte de la síntesis _backend_.   

Si examinamos el proceso de compilación con más detalle vemos que opera en forma de _fases_, cada una de las cuales transforma una representación del programa fuente en otro. En la figura 1.6 se muestra una descomposición típica de un compilador en fases. **En la práctica, varias fases pueden agruparse, y las representaciones intermediarias entre las fases agrupadas no necesitan construirse de manera explícita**. La tabla de símbolos, que almacena información sobre el programa fuente, se utiliza en todas las fases del compilador.

> Algunos compiladores tienen una fase de optimización de código independiente de la máquina, entre el _frontend_ y el _backend_. Como esta es opcional, puede faltar una de las dos fases de optimización de la figura 1.6.   

![](img6.png)   

## 1.2.1 Análisis de Léxico

A la primera fase de un compilador se le llama análisis de léxico o escaneo. El analizador de léxico lee el flujo de caracteres que componen el programa fuente y los agrupa en secuencias significativas, conocidas como lexemas. Para cada lexema, el analizador léxico produce como salida un token de la forma:   

```xml
<nombre-token, valor-atributo>
```

que pasa a la fase siguiente, el análisis de síntaxis. En el token, el primer componente _nombre-token_ es un símbolo abstracto que se utiliza durante el análisis sintáctico, y el segundo componente _valor-atributo_ apunta a una entrada en la tabla de símbolos para este token. La información de la entrada en la tabla de símbolos se necesita para el análisis semántico y la generación de código.   

Por ejemplo, suponga que un programa fuente contiene la instrucción de asignación:   

```python
posicion = inicial + velocidad * 60  (1.1)
```

Los caracteres en esta asignación podrían agruparse en los siguientes lexemas y mapearse a los siguientes tokens que se pasan al analizador sintáctico.   

1. **posición** es un lexema que se asigna a un token **<id,1>** en donde **id** es un símbolo abstracto que representa la palabra _identificador_ y **1** apunta a la entrada de la tabla de símbolos para **posición**. La entrada en la tabla de símbolos para un identificador contiene información acerca de éste, como su nombre y tipo.   
2. El símbolo de asignación **=** es un lexema que se asigna al token **<=>**. Como este token no necesita un _valor-atributo_, hemos omitido el segundo componente.   
3. **inicial** es un lexema que se asigna al token **<id,2>**, en donde 2 apunta a la entrada en la tabla de símbolos para **inicial**.   
4. **+** es un lexema que se asigna al token **<+>**.   
5. **velocidad** es un lexema que se asigna al token **<id,3>**, en donde 3 apunta a la tabla de símbolos para **velocidad**.   
6. **\*** es un lexema que asigna al token **<*>**.   
7. 60 es un lexema que se asigna al token **<60>**.   

El analizador léxico ignora los espacios en blanco que separan los lexemas.   
La figura 1.7 muestra la representación de la instrucción de asignación 1.1 después del análisis léxico como la secuencia de tokens.   

``` xml
<id,1> <=> <id,2> <+> <id,3> <*> <60>
```
En esta representación, los nombres de los tokens =, + y * son símbolos abstractos para los operadores de asignación, suma y multiplicación, respectivamente.   

![](img7.png)
> Figura 1.7 Traducción de una instrucción de asignación.

## 1.2.2 Análisis Sintáctico   

La segunda fase del compilador es el analizador sintáctico o _parser_. El parser utiliza los primeros componentes de los tokens producidos por el analizador de léxico para crear una representación intermedia en forma de árbol que describa la estructura gramatical del flujo de tokens. Una representación típica es el _árbol sintáctico_, en el cual cada nodo interior representa una operación y los hijos del nodo representan los argumentos de la operación. En la figura 1.7 se muestra un árbol sintáctico para el flujo de tokens (1.2) como salida del analizador sintáctico.   
Este árbol muestra el orden en que debe llevarse a cabo las operaciones en la siguiente asignación:

```python
        posicion = inicial + velocidad * 60
```

El árbol tiene un nodo interior etiquetado como *, con <id,3> como su hijo izquierdo, y el entero 60 como su hijo derecho. El nodo <id,3> representa el identidicador `velocidad`. El nodo etiquetado como * hace explicito que primero debemos multiplicar el valor de la `velocidad` por 60. El nodo etiquetado como `+` indica que debemos sumar el resultado de esta multiplicación al valor `inicial`. La raíz del árbol, que se etiqueta como `=`, indica que debemos almacenar el resultado de esta suma en la ubicación para el identifiador de `posicion`. Este ordenamiento de operaciones es consistente con las convenciones usuales de la aritmética, las cuales nos indican que la multiplicación tiene mayor procedencia que la suma y, por ende, debe realizarse antes que la suma.   
Las fases siguientes del compilador utilizan la estructura gramatical para ayudar a analizar el programa fuente y generar el programa destino. En el capítulo 4 se usarán gramáticas libres de contexto para especificar la estructura gramatical de los lenguajes de programación, y hablaremos sobre los algoritmos para construir analizadores sintácticos eficientes de manera automática, a partir de ciertas clases gramáticas. En los capítulos 2 y 5 veremos que las definiciones orientadas a la sintaxis pueden ayudar a especificar la traducción de las construcciones del lenguaje de programación.   

## 1.2.3 Análisis semántico

En _analizador semántico_ utiliza el árbol sintáctico y la información de la tabla de símbolos para comprobar la consistencia semántica del programa fuente con la definición del lenguaje. **También recopila información sobre el tipo** y la guarda, ya sea en el árbol sintáctico o en la tabla de símbolos, para usarla más adelante durante la generación de código intermedio.   
**Una parte importante del análisis semántico es la comprobación** (_verificación_) de tipos, en donde el compilador verifica que cada operador tenga operandos que coincidan. Por ejemplo, muchas definiciones de lenguajes de programación requieren que el índice de un arreglo sea entero; el compilador debe reportar si un error si se utiliza un número de punto flotante para indexar el arreglo.   
La especificación del lenguaje puede permitir ciertas conversiones de tipo conocidas como _coerciones_. Por ejemplo, puede aplicarse un operador binario aritmetico a un par de enteros o a un par de números de punto flotante. Si el operador se aplica a un número de punto flotante y a un entero, el compilador puede convertir u obligar a que se convierta en un número de punto flotante.   
Dicha conversión aparece en la figura 1.7. Suponga que `posicion`, `inicial`, y `velocidad` se han declarado como números de punto flotante, y que el lexema `60`por sí solo forma un entero. El comprobador de tipo en el analizador semántico de la figura 1.7 descubre que se aplica el operador * al número de punto flotante `velocidad` y al entero `60`. En este caso, el entero se puede convertir a un número de punto flotante. Observe en la figura **1.7** que la salida del analizador semántico tiene un nodo adicional para el operador **`inttofloat`**, que convierte de manera explícita su argumento tipo entero a un número de punto flotante. En el capítulo 6 hablaremos sobre la comprobación de tipos y el análisis semántico.

## 1.2.4 Generación de código intermedio

En el proceso de traducir un programa fuente a código destino, un compilador puede construir una o más representaciones intermedias, las cuales pueden tener una variedad de formas. Los árboles sintácticos son una forma de representación intermedia; por lo general, se utilizan durante el análisis sintáctico y semántico.   
Después del análisis sintáctico y semántico del programa fuente, muchos compiladores generan un nivel bajo explícito, o una representación intermedia similar al código máquina, que podemos considerar como un programa para una máquina abstracta. Esta representación intermedia debe tener dos propiedades importantes: debe ser fácil de producir y fácil de traducir en la máquina destino.   
En el capítulo 6, consideramos una forma intermedia llamada _código de tres direcciones_, que consiste en una secuencia de instrucciones similares a ensamblador, con tres operandos por instrucción. Cada operando puede actuar como registro. La salida del generador de código intermedio de la figura 1.7 consiste en la secuencia de código de tres direcciones.  

```python
        t1 = inttofloat(60)
        t2 = id3 * t1
        t3 = id2 + t2
        id1 = t3                         (1.3)
```

Hay varios puntos que vale la pena mencionar sobre las instrucciones de tres direcciones. **En primer lugar**, cada instrucción de asignación de tres direcciones tiene, al menos, un operador de lado derecho. Por ende, estas instrucciones corrigen el orden en el que van a realizarse las operaciones; la multiplicación va antes que la suma en el programa fuente (1.1). **En segundo lugar**, el compilador debe generar un nombre temporal para guardar el valor calculado por una instrucción de tres direcciones. **En tercer lugar**, algunas "instrucciones de tres direcciones" como la primera y la última en la secuencia (1.3) anterior, tiene menos de tres operandos.   
En el capítulo 6 hablaremos sobre las representaciones intermedias principales que se utilizan en los compiladores. En el capítulo 5 introduce las técnicas para la traducción dirigida por la sintaxis, las cuales se dividen en el capítulo 6 para la comprobación de tipos y la generación de código intermedio en las construcciones comunes de los lenguajes de programación, como las expresiones, las construcciones de control de flujo y las llamadas a procedimientos.   

## 1.2.5 Optimización de código

La fase de optimización de código independiente de la máquina trata de mejorar el código intermedio, de manera que se produzca un mejor código destino. Por lo general, mejor significa más rápido, pero pueden lograrse otros objetivos, como un código más corto, o un código de destino que consuma menos poder. Por ejemplo, un algoritmo directo genera el código intermedio (1.3), usando una instrucción para cada operador en la representación tipo árbol que produce un analizador semántico.  
Un algoritmo simple de generación de código intermedio, seguido de la optimización de código, es una manera razonable de obtener un buen código de destino. El optimizador puede deducir que la conversión del 60, de entero a punto flotante, puede realizarse de una vez por todas en el tiempo de compilación, por lo que puede eliminar la operación **`inttofloat`** sustitutendo el 60 por el número de punto flotante 60.0. Lo que es más, `t3` se utiliza sólo una vez para transmitir su valor a `id1`, para que el optimizador pueda transformar (1.3) en la siguiente secuencia más corta.   

```python
        t1 = id3 * 60.0
        id1 = id2 + t1                  (1.4)
```

Hay una gran variación en la cantidad de optimización de código que hacen los distintos compiladores. En aquellos que realizan la mayor optimización, a los que se les denomina como "compiladores optimizadores", se invierte mucho tiempo en esta fase. Hay optimizaciones simples que mejoran en forma considerable el tiempo de ejecución del programa destino, sin reducir demasiado la velocidad de la compilación. Los capítulos 8 en adelante hablan con más detalle sobre las optimizaciones independientes y dependientes de la máquina.

## 1.2.6 Generación de código

El generador de código recibe como entrada una representación intermedia del programa fuente y le asigna un lenguaje destino. Si el lenguaje destino es código máquina, se seleccionan registros o ubicaciones (localidades) de memoria para cada una de las variables que utiliza el programa. Después, las instrucciones intermedias se traducen en secuencias de instrucciones de máquinas que realizan la misma tarea. Un aspecto de la generación de código es la asignación juiciosa de los registros para guardar las variables.   
Por ejemplo, usando los registros **R1** y **R2**, el código intermedio en (1.4) podría traducirse de la siguiente manera:   

```assembly
    LDF  R2,  id3
    MULF R2,  R2, #60.0
    LDF  R1,  id2
    ADDF R1,  R1, R2
    STF  id1, R1
```

## 1.2.7 Administración de la tabla de símbolos

Una función escencial de un compilador es registrar los nombres de las variables que se utilizan en el programa fuente, y recolectar la información sobre varios atributos de cada nombre. Estos atributos pueden proporcionar información acerca del espacio de almacenamiento que se asigna para un nombre, su tipo, su alcance (en qué parte del programa puede usarse su valor), y en el caso de los nombres de procedimientos, cosas como el número y los tipos de argumento (por ejemplo, por valor o por referencia) y el tipo devuelto.   
La tabla de símbolos es una estructura de datos que contiene el registro para cada nombre de variable, con campos para los atributos del nombre. La estructura de datos debe diseñarse de tal forma que permita al compilador buscar el registro para cada nombre, y almacenar u obtener datos de ese registro con rapidez. En el capítulo 2 hablaremos sobre las tablas de símbolos.