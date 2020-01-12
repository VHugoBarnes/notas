# Introducción a la teoría de la computación

La teoría del automata (también conocida como teoría de la computación) esuna
rama teoríca de las ciencias de la computación y las matemáticas, la cual
principalmente maneja la lógica de la computación en lo que respecta a máquinas
simples, que son referidas como autómatas.

El autómata le permite a los cientifícos entender cómo las máquinas computan
las funciones y resuelven los problemas. La principal motivación detrás del
desarrollo de la teoría del autómata fue el de desarrollar métodos para
describir y analizar el comportamiento dinámico de sistemas discretos.

La palabra autómata fue originada de la palabra  _"Automaton"_ el cual está
estrechamente relacionada con _"Automation"_.

Ahora, vamos a entender las terminologías básicas, las cuales son muy
importantes y frecuentemente usadas en **Teoría de la computación**.

- **Símbolo:** El símbolo es el bloque más pequeño de construcción, puede ser
cualquier alfabeto, letra o cualquier imágen.

    ![](https://media.geeksforgeeks.org/wp-content/uploads/strng.png)

- **Alfabetos:** Los alfabetos son un conjunto de símbolos, los cuales siempre
   son fínitos.

    ![](https://media.geeksforgeeks.org/wp-content/uploads/alpha1.png)

- **Cadena de texto:** La cadena de texto es una sequencia fínita de algún
   alfabeto. La cadena de texto es generalmente denotada como _**w**_ y el
tamaño de una cadena de texto es denotado por _**|w|**_.

  > Una cadena de texto vacía es una cadena de texto con
  > cero ocurrencias de símbolos, representada como **ε**.
  >
  > **El número de cadenas de texto (de tamaño 2)**
  > **que pueden ser generadas sobre el alfabeto {a, b}**
  > <center>
  >
  > | 1      | 2      |
  > | :----: | :----: |
  > | a      | a      |
  > | a      | b      |
  > | b      | a      |
  > | b      | b      |
  >
  >  </center>
  > Largo de la cadena de texto |w| = 2
  > Número de cadena de texto = 4
  >
  > **Conclusión:**
  >
  > Para el alfabeto {a, b} con el tamaño **n**, el número de cadenas de texto que
  > pueden ser generadas = **2^n**

  **Nota -** Si el número de Σ's(sumatorias(?)) es representada por |Σ|, entonces
  el número de cadenas de textos de largo **n**, posible sobre Σ es
|**Σ**|**^n**.

- **Lenguaje:** Un lenguaje es un conjunto de __cadenas de texto__, escogidos
   de Σ* o podemos decir- 'Un lenguaje es un subconjunto de Σ*'. Un lenguaje el
cual puede ser formado sobre 'Σ' puede ser **fínito** o **infínito**.

  ![](https://media.geeksforgeeks.org/wp-content/uploads/lang.png)

<u>**Potencias de 'Σ':** </u>

Se dice que Σ = {a, b}, entonces:

**Σ⁰** = conjunto de todas las cadenas de texto sobre Σ de largo 0. {e}\
**Σ¹** = conjunto de todas las cadenas de texto sobre Σ de largo 1. {a, b}\
**Σ²** = conjunto de todas las cadenas de texto sobre Σ de largo 2. {aa, ab,
 ba. bb}\
i.e. |Σ²|=4 y similarmente, |Σ³|=8

> Σ* es un conjunto universal. \
> Σ* = Σ^0 U Σ1 U Σ2 ..........\
>    = {ε} U {a, b} U {aa, ab, ba, bb}\
>    = .............   //lenguaje infínito.



