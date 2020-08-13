# 1.2 La estructura de un compilador

De momento, al compilador se le ha tratado como una caja simple que mapea un programa fuente a un programa destino con equivalencia semántica. Si lo analisamos un poco, nos damos cuenta que existen dos procesos en esta asignación: **análisis** y **síntesis**.   

El **análisis**: Divide el programa fuente en componentes e impone una estructura gramatical sobre ellas. Después esta estructura la utiliza para crear una representación intermedia del programa fuente. Si se detecta que el programa fuente está mal formado en cuanto a la sintaxis, o que no tiene una semantica consistente, entonces debe proporcionar mensajes informativos para que el usuario pueda corregirlo. La parte del análisis también recolecta información sobre el programa fuente y almacena una estructura de datos llamada **_tabla de símbolos_**, la cual se pasa junto con la representación intermedia a la parte de la síntesis.   

La **síntesis**: Construye el programa destino deseado a partir de la representación intermedia y de la información en la tabla de símbolos.

> A la parte del análisis se le llama comunmente _frontend_ y a la parte de la síntesis _backend_.   

Si examinamos el proceso de compilación con más detalle vemos que opera en forma de _fases_, cada una de las cuales transforma una representación del programa fuente en otro. En la figura 1.6 se muestra una descomposición típica de un compilador en fases. **En la práctica, varias fases pueden agruparse, y las representaciones intermediarias entre las fases agrupadas no necesitan construirse de manera explícita**. La tabla de símbolos, que almacena información sobre el programa fuente, se utiliza en todas las fases del compilador.

> Algunos compiladores tienen una fase de optimización de código independiente de la máquina, entre el _frontend_ y el _backend_. Como esta es opcional, puede faltar una de las dos fases de optimización de la figura 1.6.   

![](img6.png)   

## 1.2.1 Análisis de Léxico

