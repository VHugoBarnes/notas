# Uso interactivo de la _Shell_.

Cuando usas la _Shell_ interactivamente, te acoplas a un inicio de sesión que
empieza cuando inicias sesión y termina cuando escribes **exit** o **logout**
o presionas CTRL-D. Durante el inicio de sesión, escribes en líneas de comando
a la _Shell_; estas líneas de texto terminan en el RETURN que escribes en tu
terminal o estación de trabajo. 

Por defecto, la _Shell_ te manda para cada comando una cadena de texto con
información seguido de un signo de dólar. 

# Comandos, argumentos y opciones.

Las líneas de comandos de la _Shell_ consisten en una o más palabras, las
cuales son separadas por espacios en blanco o _TABS_. La primera palabra en la
línea es el _comando_. El resto (sí es que hay) son llamados _argumentos_
(también llamados _parametros_) al comando, los cuales son nombres de cosas
sobre la cual el comando actuará.

Por ejemplo el siguiente comando:

```bash

lp myfile.txt

```

consiste en el comando _lp_(imprime un archivo) y el único argumento
**myfile.txt**.

_lp_ trata a **myfile.txt** como el nombre de un archivo a imprimir. Los
argumentos a menudo son nombres de archivos, pero no necesariamente: en la
línea de comando **mail cam**, el programa _mail_ trata a **cam** como un
usuario al cual un mensaje será mandado.

Una _option_ es un tipo especial de argumento que le da al comando información
específica sobre qué exactamente tiene que hacer. Las opciones usualmente
consisten de un _dash_ ("-") seguido de una letra. El comando **lp -h myfile**
contiene la opción **-h**, el cual le dice a _lp_ que no imprima el "banner de
la página" antes de que imprima el archivo.

A veces las opciones toman sus propios argumentos. Por ejemplo:

```bash
lp -d lp1 -h myfile
```

tiene dos opciones y un argumento. La primera opción es **-d lp1**, que
significa "Manda la salida a la impresora (destino) llamado **lp1**.".


# Archivos

A pesar de que los argumentos a los comandos no siempre son archivos, son de
las "cosas" más importantes en un sistema UNIX. Un archivo puede contener
cualquier tipo de información, y en efecto hay diferentes tipos de archivos.
Tres tipos son por más los más importantes:

_**Archivos regulares**_

También llamados archivos de texto; estos contienen caracteres leíbles. 

_**Archivos ejecutables**_

También programas; estos son invocados como comandos. Algunos no pueden ser
leídos por humanos; otros--por ejemplo los script de _Shell_-- son archivos de
texto especiales. La _Shell_ en sí es un (non-human-readable) archivo
ejecutable llamado _bash_.

_**Directorios**_

Estos son como carpetas que contienen otros archivos--posiblemente otras
carpetas (llamadas sub-directorios).
