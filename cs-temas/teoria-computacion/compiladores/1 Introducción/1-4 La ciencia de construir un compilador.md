# 1.4 La ciencia de construir un compilador

El diseño de compiladores está lleno de bellos ejemplos, en donde se resuelven problemas complicados del mundo real mediante la abstracción de la esencia del problema en forma matemática. Éstos sirven como excelentes ilustraciones de cómo pueden usarse las abstracciones para resolver problemas: se toma un problema, se formula una abstracción matemática que capture las características clave y se resuelve utilizando técnicas matemáticas. La formulación del problema debe tener bases y una sólida comprensión de las características de los programas de computadora, y la solución debe validarse y refinarse de forma empírica.   
Un compilador debe aceptar todos los programas fuente conforme a la especificación del lenguaje; el conjunto de programas fuente es infinito y cualquier programa puede ser muy largo, posiblemente formado por millones de líneas de código. Cualquier transformación que realice el compilador mientras traduce un programa fuente debe preservar el significado del programa que está compilando. Por ende, los escritores de compiladores tienen influencia no sólo sobre los compiladores que crean, sino en todos los programas que compilan sus compiladores. Esta capacidad hace que la escritura de compiladores sea en especial gratificante; no obstante, también hace que el desarrollo de los compiladores sea todo un reto.

## 1.4.1 Modelado en el diseño e implementación de compiladores

El estudio de los compiladores es principalmente un estudio de la forma en que diseñamos los modelos matemáticos apropiados y elegimos los algoritmos correctos, al tiempo que logramos equilibrar la necesidad de una generalidad y poder con la simpleza y eficiencia.   
Algunos de los modelos más básicos son las máquinas de estados finitos y las expresiones regulares. Estos modelos son utiles para descubrir las unidades de léxico de los programas (palabras clave, identificadores y demás) y para describir los algoritmos que utiliza el compilador para reconocer esas unidades. Además, entre los modelos esenciales se encuentran las gramaticas libres de contexto, que se utilizan para describir la estructura sintáctica de los lenguajes de programación.

## 1.4.2 La ciencia de la optimización de código


