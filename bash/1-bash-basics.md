# Conceptos básicos de bash.

Desde los comienzos de los años 70, cuando fue creado por primera vez, el
sistema operativo UNIX se ha vuelto cada vez más popular. Durante esas fechas
se ha ramificado en diferentes versiones y ha tomado muchos nombres como
Ultrix, AIX, Xenix, SunOS, and Linux. Empezando en minicomputadoras y [unidades
centrales](https://es.wikipedia.org/wiki/Unidad_central), se ha movido hacia
estaciones de trabajo de escritorio e incluso computadoras personales.

Varias capas de eventos toman lugar cuando introduces un comando, pero vamos
a considerar sólo la capa superior conocida como _shell_. Generalmente
hablando, un _shell_ es cualquier interfaz de usuario para el sistema operativo
UNIX, i.e., cualquier programa que tome un _input_ del usuario, lo traduzca
a instrucciones que el sistema operativo pueda entender y transporta el
_output_ del sistema operativo de vuelta al usuario.

Hay muchos tipos de interfaces de usuario. _bash_ pertenece a la categoría más
común, conocido como interfaces de usuario basadas en caracteres. Estas
interfaces aceptan lineas de comandos textuales que el usuario _tipea_ en él;
estas interfaces usualmente producen _output_ basado en texto. Otro tipo de
interfaces incluyen las cada vez más comúnes interfaces de usuario gráficas
(**GUI**) el cual da una habilidad de mostrar gráficos arbitrarios y aceptar
entradas de un mouse o de otro dispositivo apuntador, interfaces _touch-screen_
y así.

## ¿Qué es un _Shell_?

El trabajo del _Shell_ es entonces el de traducir los comandos del usuario en
instrucciones del sistemas operativos. Por ejemplo, considera la siguiente
línea de comando:

```bash

sort -n phonelist > phonelist.sorted

```

Esto significa, "Ordena líneas en el archivo _phonelist_ en orden númerico,
y coloca el resultado el resultado en el archivo _phonelist.sorted_." 

Esto es lo que la _Shell_ hace con el comando:

1. Rompe la línea en piezas _sort_, _-n_, _phonelist_, _>_, _phonelist.sorted_.
Estas piezas son llamadas palabras.
2. Determina el propósito de las palabras: _sort_ es un comando, _-n_
y _phonelist_ son argumentos, y _>_ y _phonelist.sorted_, tomados juntos, son
instrucciones de entrada y salida (**I/O**).
3. Configura la entrada y salida de acuerdo con _> phonelist.sorted_ (lo
escribe en el archivo _phonelist.sorted_) y algunas instrucciones implicitas
y estándar.
4. Encuentra el comando _sort_ en un archivo y lo ejecuta con la opción
_**-n**_(orden númerico) y el argumento _phonelist_ (archivo de entrada).

Por supuesto, cada uno de esos pasos implica varios sub-pasos, cada uno incluye
una instrucción en particular al sistema operativo subyacente. 

Recuerda que la _Shell_ en sí no es UNIX--Sólo la interfaz de usuario a ella.
UNIX fue de los primeros sistemas operativos en hacer la interfaz de usuario
independiente del sistema operativo.

## La historia de las _Shells_ en UNIX.

La independencia de la _Shell_ del sistema operativo UNIX por sí ha llevado al
desarrollo de decenas de _Shells_ en toda la historia de UNIX--a pesar de que
sólo unas cuantas han conseguido el uso extendido.

La primera _Shell_ mayor fue la _Bourne Shell_(nombrada así por su inventor,
Steven Bourne); fue incluida en la primera versión pupular de UNIX, su versión
7, en 1979. La _Bourne Shell_ es conocida por el sistema como _**sh**_.
a pesar de que UNIX ha pasado por muchos cambios, la _Bourne Shell_ sigue
siendo popular y escencialmente sin cambios. Varias utilidades
y caracteristicas de administración de UNIX dependen de ella.

## La _Bourne Again Shell_.

Fue creada para el uso del proyecto GNU. El proyecto GNU fue iniciado por
Richard Stallman de la _Free Software Foundation_(_FSF_) con el propósito de
crear un sistema operativo UNIX-compatible y remplazar todas las utilidades
comerciales con las de libre distribución. GNU encarna no solo nuevas
utilidades de software, también un concepto de distribución nuevo: el
_copyleft_. El software _Copyleft_ podía ser libremente distribuido tanto como
sin restricciones fueran puestas en más distribuciones.

_bash_, destinado a ser la _shell_ estándar para el sistema GNU, nació
oficialmente en domingo 10 de enero de 1988. Brian Fox escribió las versiones
originales de _bash_ y _readline_ y continuó mejorando la _shell_ hasta 1993.
Más tarde en 1989 se le unió a Chet Ramey, el cuál fue responsable de numerosos
arreglos de _bugs_ y la inclusión de varias caracteristicas útiles. Chet Ramey
es ahora el mantenedor oficial de _bash_ y continua haciendo otras mejoras.

## Características de _bash_.

A pesar de que _Bourne Shell_ sigue siendo conocido como la _shell_ "estandar",
_bash_ se está volviendo cada vez más popular. Añadiendole la compatibilidad
con la _Bourne Shell_, incluye las mejores caracteristicas de la _C y Korn
Shells_ también como varias ventajas propias.

Los modos de edición de línea de comandos de _bash_ son una característica que
tiende a atraer a la gente primero. Con edición en la línea de comandos es más
fácil ir atrás y arreglas mistakes o modificar comando previos que con el
mecanismo de historial de la _C Shell_.

La otra gran característica de _bash_ que está destinado mayormente a los
usuarios interactivos es el control de trabajos. El control de trabajos te
da la habilidad de parar, iniciar y pausar cualquier número de comandos al
mismo tiempo. Esta característica fue tomada de la _C Shell_ literalmente.

El resto de ventajas importantes de _bash_ son principalmente para
programadores y customizadores de la _Shell_. Tiene muchas nuevas opciones
y variables para la customización, y sus características de programación han
sido significativamente expandidas para incluir definición de funciones, más
estructuras de control, aritmética de enteros, control avanzado de _I/O_ y más.
 
