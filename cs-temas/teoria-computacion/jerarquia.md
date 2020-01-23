# Jerarquía Chomsky en teoría de la computación


De acuerdo con la jerarquía Chomsky, la gramática está dividida en 4 tipos:

> **Tipo 0**, conocido como gramática sin restricciones.\
> **Tipo 1**, conocido como gramática sensitiva al contexto.\
> **Tipo 2**, conocido como gramática de contexto libre.\
> **Tipo 3**, conocido como gramática regular.

![](https://media.geeksforgeeks.org/wp-content/uploads/20190227115949/Comsky-1.png)

## Tipo 0, gramática sin restricciones.

Incluye a todas las gramaticas formales. Estas gramáticas generan todos los
lenguajes capaces de ser reconocidos por una _máquina de Turing_. Los lenguajes
son conocidos como lenguajes recursivamente enumerables. Nótese que esta
categoría es diferente de la de los lenguajes recursivos, cuya decisión puede
ser realizada por una _máquina de Turing_ que se detenga.

### Máquina de Turing.

Una máquina de Turing es un dispositivo que manipula símbolos sobre una cinta
de acuerdo con una tabla de reglas. Apesar de su simplicidad puede ser usada
para simular la lógica de cualquier algoritmo de computador y es
particularmente útil en la explicación de las funciones que realiza una **CPU**
dentro del computador.

Originalmente fue definida por el matemático inglés Alan Turing como una
_<<maquina automática>>_ en 1936 en la revista _Proceedings of the London
Mathematical Society_. La _máquina de Turing_ no está diseñada como una
tecnología de computación práctica, sino como un dispositivo hipotético que
representa una máquina de computación.

Turing dió una definición sucinta del experimento en su ensayo en 1948,
_<<máquinas inteligentes>>_. Refiriendose a su publicación de 1936, Turing
escribió que la máquina de Turing, aquí llamada máquina de computación lógica,
consistía en:  

> ... una ilimitada capacidad de memoria obtenida en la forma de una cinta
infinita marcada con cuadros, en cada uno de los cuales podría imprimirse un
símbolo. En cualquier momento hay un símbolo en la máquina; llamado el símbolo
leído. La máquina puede alterar el símbolo leído. La máquina puede alterar un
símbolo leído y su comportamiento está en parte determinado por ese símbolo,
pero los símbolos en otros lugares de la cinta no afectan el comportamiento de
la máquina. Sin embargo, la cinta se puede mover hacia atrás a través de la
máquina, siendo esto una de las operaciones elementales de la máquina. Por lo
tanto cualquier símbolo en la cinta puede tener finalmente una oportunidad.

Se dará una definición más completa en otro archivo...

## Tipo 1, grámaticas sensibles al contexto.

Generan los lenguajes sensibles al contexto. Estas grámaticas tienen reglas de
la forma
![](https://wikimedia.org/api/rest_v1/media/math/render/svg/1173552bcbf68bb06baf9b0a2f543dbc845caefd)
con A un no terminal
y ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/b79333175c8b3f0840bfb4ec41b8072c83ea88d3)
, ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/7ed48a5e36207156fb792fa79d29925d2f7901e8)
y ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/a223c880b0ce3da8f64ee33c4f0010beee400b1a) 
cadenas de terminales y no terminales 
