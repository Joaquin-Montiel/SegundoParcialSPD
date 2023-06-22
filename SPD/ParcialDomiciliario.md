Segundo Parcial SPD  
## Tema: 
Sistema de incendio con Arduino
![Imagen del proyecto]()
## Alumno: 
Joaquin Montiel
## Consigna:
Objetivo:
El objetivo de este proyecto es diseñar un sistema de incendio utilizando Arduino que pueda
detectar cambios de temperatura y activar un servo motor en caso de detectar un incendio.
Además, se mostrará la temperatura actual y la estación del año en un display LCD.
Componentes necesarios:
Arduino UNO
Sensor de temperatura
Control remoto IR (Infrarrojo)
Display LCD (16x2 caracteres)
Servo motor
Cables y resistencias según sea necesario
Protoboard para realizar las conexiones
Dos leds.
Funcionalidad requerida:
Conexiones:
Conecta el sensor de temperatura al pin analógico A0 de Arduino.
Conecta el control remoto IR al pin digital 11 de Arduino.
Conecta el display LCD utilizando los pines correspondientes de Arduino.
Conecta el servo motor a uno de los pines PWM de Arduino (por ejemplo, pin 9).
Control remoto:
Configura el control remoto IR para recibir señales.
Define los comandos necesarios para activar y desactivar el sistema de incendio.
Utiliza un algoritmo para determinar la estación del año (por ejemplo, rangos de temperatura
para cada estación).
Detección de temperatura:
Configura el sensor de temperatura y realiza la lectura de la temperatura ambiente.
Muestra la temperatura actual en el display LCD.
Sistema de alarma:
Define un umbral de temperatura a partir del cual se considera que hay un incendio (por ejemplo, temperatura superior a 60 grados Celsius).
Cuando se detecta un incendio (temperatura por encima del umbral), se activa el servo motor para simular una respuesta del sistema de incendio.
Mensajes en el display LCD:
Muestra la temperatura actual y la estación del año en el display LCD.
Cuando se detecta un incendio, muestra un mensaje de alarma en el display LCD.
Punto libre:
Se deberá agregar dos leds y darle una funcionalidad de su elección, acorde al
proyecto previamente detallado.
Recuerda proporcionar un diagrama de conexiones y el código necesario para implementar cada una de las funcionalidades requeridas. Esto ayudará a comprender y construir el sistema de incendio con Arduino.
Aclaraciones para la aprobación de la parte práctica:
• Debe haber buen uso de las funciones.
• El código debe ser prolijo y legible.
1- debe poder explicar cada punto
2- debe poder modificar la funcionalidad agregando lo que sea necesario
3- Documentación:
• Deberán presentar un diagrama esquemático del circuito y explicar el
funcionamiento aplicado de cada componente.
• Presentar el código fuente del proyecto de Arduino listo para ser
implementado.
• Deberán explicar el funcionamiento integral utilizando documentación
MarkDown.

## Descripcion:
Desarrolle un sistema de incendios que inicia cuando preciono el boton de encendido del control remoto IR.
Este circuito hace una lectura de la temperatura proporcional a la temperatura del ambiente. Esta temperatura es mostrada por el LCD con la funcion 'mostrarTemperaura()'. 
Esa misma temperatura es comparada para determinar las estacion del año con la funcion 'mostrarEstacion()'. En la misma funcion si la temperatura esta entre los 59° y 46° grados emitimos un 'alerta naranja' en el LCD y a traves del led amarillo que se enciende, pero si la temperatura es igual o supera los 60° grados prendemos el led rojo con un catel del peligro alertando a los presentes y tambien encendemos el servo motor para lograr apagar el fuego con la funcion 'moverServo()'. Por ultimo si deseamos apagar el circuito apretamos la 'FUNC/STOP' y el mismo se apaga.


## Funcion Principal:

//Funcion que toma la temperatura
float obtenerTemperatura(){
  int lecturaSensor = analogRead(A0);// Con analogRead leemos el valor del sensor de temperatura
  float temperatura = map(lecturaSensor, 20, 358, -40, 125);
  return temperatura;
}


//Fragmento de codigo:
```
void setup(){
  Serial.begin(9600);
  pinMode(LED_1, OUTPUT);
  pinMode(LED_2, OUTPUT);
  IrReceiver.begin(sensorIR, DISABLE_LED_FEEDBACK); //inicializo el control remoto IR
  myLCD.begin(16, 2); //Inicializo el LCD 16x2
  myServo.attach(9); //Inicializo el servo
  myServo.write(0);//posiciono el servo en 0
}

void loop(){
if (IrReceiver.decode()) 
{
  Serial.println(IrReceiver.decodedIRData.decodedRawData, HEX);
  IrReceiver.resume();
}
  if(IrReceiver.decodedIRData.decodedRawData == tecla_1){ //inicio el circuito de incendios con la tecla_1
      float temperatura = obtenerTemperatura();
 	  mostrarTemperatura(temperatura);
  	  mostrarEstacion(temperatura);
      Serial.println(temperatura);
    }
  else if(IrReceiver.decodedIRData.decodedRawData == tecla_2){//apago el circuito de incendios con el control remoto a partir de la tecla_2
  }
 Serial.println(irResults.value, HEX);   
}
```

## Link al proyecto en Tinkercad
[Link](https://www.tinkercad.com/things/jiRLBVLVohf-cool-bruticus/editel?sharecode=7iiwJoQTG--QCElCKcPaycjl9qNWVLkyh_klSp1lrog)

## Link al codigo completo en GDB Online
[Link](https://onlinegdb.com/YtKhmy-Oaz)


