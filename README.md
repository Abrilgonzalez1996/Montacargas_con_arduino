<h1 align= "center">Primer Parcial SPD 🤖</h1>

<p align="center">
   <img src= "Img/ArduinoTinkercad.jpg" />
</p>

# Integrantes 👩‍🎓 
- Abril Mariel Gonzalez Bernabeu

# Proyecto: Montacargas 
<p align="center">
   <img src= "Img/Proyecto montacargas.png"/>
</p>

# Objetivo: 
El objetivo es que implementes un sistema que pueda recibir ordenes de subir, bajar o pausar desde diferentes pisos y muestre el estado actual del montacargas en el display 7 segmentos. 

# Funciones principales:

Esta función establece los modos de los pines, enciende un LED rojo y luego llama a otras funciones (prender_tablero() y imprimir_mensaje()) para señalizar por primera y unica vez el piso en donde se encuentra y luego imprime el mensaje.
```c++
void setup(){
  pinMode(led_verde, OUTPUT);
  pinMode(led_rojo, OUTPUT);
  Serial.begin(9600);
  for(int i = 0; i < 7; i++){
  	pinMode(tablero[i], OUTPUT);
    if(i < 3){
    	pinMode(botones[i], OUTPUT);
    }
  }
  digitalWrite(led_rojo, HIGH);
  mensaje = prender_tablero(numero_prender, tablero, HIGH);
  imprimir_mensaje(mensaje);
}
```

Esta función realiza un ciclo continuo de lectura de los botones y toma acciones según las condiciones especificadas. Esto incluye encender y apagar LEDs, establecer claves y llamar a la funcion para prender el tablero, segun el retorno de la primer funcion la habilita o no.
```c++
void loop(){
  subir = digitalRead(botones[0]);
  bajar = digitalRead(botones[2]);
  delay(250);
  if(subir == HIGH && numero_prender != 9 ){
    bandera = prender_led(led_verde, led_rojo, botones[1]);
 	 clave = "subir";
  }else if(bajar == HIGH && numero_prender != 0){
    clave = "bajar";
    bandera = prender_led(led_verde, led_rojo, botones[1]);
  }
  if(bandera == true){
    subir_bajar_montacargas(tablero, clave);
    bandera = false;
  }
}
```

# Link al proyecto en tinkercad
- https://www.tinkercad.com/things/gjzBx4F55UK

# Link del codigo del proyecto en GDB
- https://onlinegdb.com/dCO7ElX8y
