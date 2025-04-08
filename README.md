1. Fichero Cliente
Nombre del archivo: cliente.c (o el nombre que prefieras)

Descripción: El código implementa un cliente que se comunica con un servidor utilizando un FIFO (First In, First Out), o tubería de comunicación bidireccional. El cliente envía un mensaje al servidor y recibe la respuesta del mismo. La comunicación sigue un ciclo en el que el cliente envía cadenas de texto al servidor, recibe la respuesta (que es la cadena invertida), y continúa el proceso hasta que el mensaje "end" es ingresado, momento en el cual se cierra la comunicación.

¿Qué hace?

Define el archivo FIFO (/tmp/fifo_twoway).

Crea una tubería (FIFO) para la comunicación entre el cliente y el servidor.

Entra en un bucle infinito donde:

Solicita al usuario que ingrese una cadena de texto.

Envía esta cadena al servidor.

Lee la respuesta del servidor, la imprime y muestra su longitud.

Si el usuario ingresa la palabra "end", el cliente envía este mensaje al servidor, lo imprime y termina el proceso cerrando el archivo FIFO.

¿Cómo lo hace?

Se utiliza la función open() para abrir el archivo FIFO.

La función fgets() captura la entrada del usuario, y la cadena se prepara eliminando el salto de línea.

La función write() se utiliza para enviar el mensaje al servidor, y read() se usa para recibir la respuesta.

Se emplea un ciclo while para continuar enviando y recibiendo mensajes hasta que se ingresa "end".

2. Fichero Servidor
Nombre del archivo: servidor.c (o el nombre que prefieras)

Descripción: Este código implementa un servidor que espera recibir mensajes de un cliente a través de un FIFO. Cuando recibe un mensaje, lo invierte y lo envía de vuelta al cliente. El servidor continuará este ciclo hasta que reciba el mensaje "end", momento en el cual terminará la comunicación.

¿Qué hace?

Crea el FIFO si no existe.

Entra en un bucle infinito donde:

Lee un mensaje enviado por el cliente.

Si el mensaje es "end", cierra el archivo FIFO y termina.

Si el mensaje no es "end", invierte la cadena y la envía de vuelta al cliente.

¿Cómo lo hace?

Se utiliza la función mkfifo() para crear el FIFO si no existe.

Se utiliza open() para abrir el FIFO y read() para recibir mensajes del cliente.

La función reverse_string() invierte la cadena recibida antes de devolverla al cliente usando write().

El servidor espera entre cada comunicación usando la función sleep() para asegurar que el cliente tenga tiempo de leer las respuestas.

Explicación del código de la función reverse_string():
Esta función invierte una cadena de texto. Funciona intercambiando el primer carácter con el último, el segundo con el penúltimo, y así sucesivamente hasta que toda la cadena ha sido invertida.