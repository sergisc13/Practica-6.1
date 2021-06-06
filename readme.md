´´´
#include <Arduino.h>
#include <SPI.h>
#include <SD.h>
File myFile;
void setup(){
Serial.begin(9600);
Serial.print("Iniciando SD ...");
SPI.begin(18,19,23,4);
if(! SD.begin(4)){
Serial.println("No se pudo inicializar");
return;
}
Serial.println("inicializacion exitosa");
// Escribimos en el fichero
myFile = SD.open("/archivo.txt",FILE_WRITE);
myFile.println("Hola mundo!!");
myFile.close();
myFile=SD.open("/archivo.txt"); //Abrimos, mostramos y leemos
if (myFile) {
Serial.println("archivo.txt:");
while (myFile.available()) {
Serial.write(myFile.read());
}
myFile.close();
}
else {
Serial.println("Error al abrir el archivo");
}
}
void loop(){}
´´´
## FUNCIONAMIENTO

Después empieza el void setup() , inicia una comunicación en serie a una
velocidad de 9600 bauds, y en la segunda hace una impresión por pantalla.
Creamos un if donde si no se inicia la función SD.begin() en el pin 4, se imprime por pantalla "No
se pudo inicializar"
Abrimos un archivo con SD.open() . En caso de que no exista el fichero, el parámetro
FILE_WRITE permite que se cree el archivo y se abra immediatamente.
Escribimos en este archivo con myFile.println() y seguidamente lo cerramos.
Hacemos otro if que lo que hace es: si el archivo mencionado anteriormente se ha abierto
imprimiremos por pantalla lo que este tenga escrito, esto lo haremos utilizando un
while (myFile.available()) , y al final de todo este if cerraremos el archivo con myFile.close()

## SALIDA DEL TERMINAL

Si no hay ningún error, por el terminal se ve el siguiente texto:
Iniciando SD ...sd init ok
inicializacion exitosa
Hola mundo!!
