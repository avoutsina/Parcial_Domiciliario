## Parcial Domiciliario SPD
![portada](https://github.com/avoutsina/Parcial_Domiciliario/assets/138216833/ee5d06b2-baec-4fed-aec1-3a502827d6b1)



## Integrantes 
-Alejandro Voutsina Labrin


## Proyecto: Primera parte
![primera-parte](https://github.com/avoutsina/Parcial_Domiciliario/assets/138216833/7e961fff-ec02-4be8-90e3-5a17d4fe2595)


## Descripción
Este proyecto nos permite mostrar mediante dos displays 7 segmentos los valores de un contador el cual puede ser modificado con los pulsadores de subir, bajar y reiniciar.

## Función principal
Esta funcion se encarga de cambiar los valores numericos de los displays.

A, B, C, D, E, F y G son defines correspondientes a cada led de los displays.



~~~ C (lenguaje en el que esta escrito)
void mostrarDigito(int digito)
//Hace un switch case con los dígitos del 0 al 9 y muestra
//el dígito que se le pase por parámetro
{
  digitalWrite(A, LOW);
  digitalWrite(B, LOW);
  digitalWrite(C, LOW);
  digitalWrite(D, LOW);
  digitalWrite(E, LOW);
  digitalWrite(F, LOW);
  digitalWrite(G, LOW);
  switch (digito)
  {
   case 1:
   {
    digitalWrite(B, HIGH);
    digitalWrite(C, HIGH);
    break;
    }
    case 2:
    {
    digitalWrite(A, HIGH);
    digitalWrite(B, HIGH);
    digitalWrite(D, HIGH);
    digitalWrite(E, HIGH);
    digitalWrite(G, HIGH);
    break;
    }
    case 3:
    {
    digitalWrite(A, HIGH);
    digitalWrite(B, HIGH);
    digitalWrite(C, HIGH);
    digitalWrite(D, HIGH);
    digitalWrite(G, HIGH);
    break;
    }
    case 4:
    {
    digitalWrite(B, HIGH);
    digitalWrite(C, HIGH);
    digitalWrite(F, HIGH);
    digitalWrite(G, HIGH);
    break;
    }
    case 5:
    {
     digitalWrite(A, HIGH);
     digitalWrite(C, HIGH);
     digitalWrite(D, HIGH);
     digitalWrite(F, HIGH);
     digitalWrite(G, HIGH);
     break;
    }
    case 6:
    {
     digitalWrite(A, HIGH);
     digitalWrite(C, HIGH);
     digitalWrite(D, HIGH);
     digitalWrite(E, HIGH);
     digitalWrite(F, HIGH);
     digitalWrite(G, HIGH);
     break;
    }
    case 7:
    {
     digitalWrite(A, HIGH);
     digitalWrite(B, HIGH);
     digitalWrite(C, HIGH);
     break;
    }
    case 8:
    {
    digitalWrite(A, HIGH);
    digitalWrite(B, HIGH);
    digitalWrite(C, HIGH);
    digitalWrite(D, HIGH);
    digitalWrite(E, HIGH);
    digitalWrite(F, HIGH);
    digitalWrite(G, HIGH);
    break;
    }
    case 9:
    {
    digitalWrite(A, HIGH);
    digitalWrite(B, HIGH);
    digitalWrite(C, HIGH);
    digitalWrite(D, HIGH);
    digitalWrite(F, HIGH);
    digitalWrite(G, HIGH);
    break;
    }
    case 0:
    {
    digitalWrite(A, HIGH);
    digitalWrite(B, HIGH);
    digitalWrite(C, HIGH);
    digitalWrite(D, HIGH);
    digitalWrite(E, HIGH);
    digitalWrite(F, HIGH);
    break;
    }
  }
}
~~~

Esta funcion se encarga prender el display correspondiente al valor numerico a mostrar.

UNIDAD y DECENA son defines de los displays correspondientes a los valores.

~~~ C 
//Selecciona el display que se le pase por parámetro
void elegirDisplay(int display)
{
  if (display == UNIDAD)
  {
    digitalWrite(UNIDAD, 0);
    digitalWrite(DECENA, 1);
    delay(DISPLAYS_ENCENDIDOS);
  }
  else if (display == DECENA)
  {
   digitalWrite(UNIDAD, HIGH);
   digitalWrite(DECENA, LOW);
   delay(DISPLAYS_ENCENDIDOS);
  }
  //Si el parámetro que se le pasa no es ninguno de los
  //anteriores, la función mantiene a los dos apagados.
  else
  {
   digitalWrite(UNIDAD, HIGH);
   digitalWrite(DECENA, HIGH);
  }
  
}
~~~

Esta funcion se encarga de mostar los valores que deben mostar cada display en vase al valor del contador.

~~~ C 
//Enciende los displays con sus valores respectivos
void encenderDisplay(int contador)
{
 elegirDisplay(DISPLAYS_APAGADOS);
 mostrarDigito(contador/10); //Cálculo para obtener las decenas
 elegirDisplay(DECENA);
 elegirDisplay(DISPLAYS_APAGADOS);
 mostrarDigito(contador - 10*(contador / 10));//Cálculo para obtener las unidades
 elegirDisplay(UNIDAD);
}
~~~

Esta funcion nos ayuda a prevenir que el contador suba drasticamente al mantener presionado alguno de los pulsadores.

~~~ C 
//Verifica que al presionar el botón y mantenerlo apretado
//no sigan cambiando los valores de los displays
int presionarBoton(void)//Esta función no recibe parámetros y devuelve un entero
{
 //Comprobamos si el botón está apagado y si anteriormente
 // también lo estaba
 botonSubir = digitalRead(SUBIR);
 botonBajar = digitalRead(BAJAR);
 botonResetear = digitalRead(RESETEAR);
 if (botonSubir)
   botonSubirPrevio = 1;
 if(botonBajar)
   botonBajarPrevio = 1;
 if(botonResetear)
   botonResetearPrevio = 1;
 
 //Devuelve el valor del pulsador si y solo si se presiona el botón
 //y anteriormente no estaba prendido
 if (botonSubir == 0 && botonSubir != botonSubirPrevio)
  {
   botonSubirPrevio = botonSubir;
   return SUBIR;
  }
 if (botonBajar == 0 && botonBajar != botonBajarPrevio)
  {
   botonBajarPrevio = botonBajar;
   return BAJAR;
  }
 if (botonResetear == 0 && botonResetear != botonResetearPrevio)
  {
   botonResetearPrevio = botonResetear;
   return RESETEAR;
  }
 return 0;
}
~~~

## :robot: Link al proyecto
- [Proyecto: Primera parte][(https://www.tinkercad.com/things/aOYiibnDjWu)](https://www.tinkercad.com/things/aTfPx16HK6o-parcialdomiciliariovoutsinalabrinalejandro/editel?sharecode=CQSGwUS37TCVx3cddo6zgpOvpWy9iCPQp2P0pVlZfY0)

## Proyecto: Segunda parte
![segunda-parte](https://github.com/avoutsina/Parcial_Domiciliario/assets/138216833/b46edafe-4a91-42a7-9289-cc8b312b5130)

## Descripción
Modificamos el primer proyecto con ayuda de mis compañeros Postulka Aieta Franco, Giuilano Sohrobigarat y Vicente Joaquin.
Las modificaciones implementan un interruptor deslizante, un motor de cc y un sensor de temperatura. Segun la posicion que adopte el interruptor el contador funcionara de manera habitual o solo mostrando los numeros primos del 0 al 99. La segunda modificacion propone el trabajo en conjunto del motor de cc y del sensor de temperatura con la finalidad de refrijerar el circuito, a medida que la temperatura sube, es captada por el sensor termico el cual acciona el motor con fin de refrijerar el circuito (el motor actuaria como ventilador). 

Motor de cc: Un motor de corriente continua (CC) es un dispositivo mecánico que convierte la energía eléctrica en energía mecánica rotativa, este recive valores del 0 al 255 los cuales regulan su velocidad de  0 a 5555 revoluciones por minuto (RPM).

Sensor de temperatura: se encarga de medir la temperatura del entorno y nos sirve como entrada analogica de datos, devolviendo valores del 20 al 358.

## Función principal

Esta funcion nos permite saber si el numero con el que esta trabajando es primo o no .

~~~ C
bool Primo(int contador)
{
 bool bandera = true;
 if (contador <= 1) //Mientras el contador sea 0 y 1 el valor será falso ya que no son primos
 {
    bandera = false;
  }
  // Verificar si el número es divisible por algún número hasta su raíz cuadrada
  int limite = sqrt(contador);
  for (int i = 2; i <= limite;i++) 
  {
    if (contador % i == 0) 
    {
      bandera =  false;//En caso de que encuentre un numero con el que
      				// el resto de su división dé 0, la bandera cambia a False 
    }
  }
  return bandera;
}
~~~

Esta funcion nos permite saber el proximo numero primo del valor con el que esta trabajando.

~~~ C
int esPrimoSube(int contador)
//Retorna el próximo numero primo que le siga al contador
{
  bool bandera = Primo(contador);
  
	if (bandera == false)
    { //Si la bandera es False, suma 1 al contador y vuelve a citar la función
     contador++;
     esPrimoSube(contador);
    }
  else
  {
  return contador;
  }
}
~~~

Esta funcion nos permite saber el numero primo previo del valor con el que esta trabajando.

~~~ C
int esPrimoBaja(int contador)
 //Retorna numero primo anterior al contador
{
  bool bandera = Primo(contador);

  if (bandera == false)
    { 
    if (contador == 0)
     { // Si el contador esta en 0 y el usuario presiona el boton para bajar
      // el contador pasa a valer 99 y volvemos a citar la funcion
      contador = 99;
      esPrimoBaja(contador);
     }
     else
     {//Si la bandera es False, resta 1 al contador y vuelve a citar la función
      contador--;
       esPrimoBaja(contador);
     }
    }
  else
  {
  return contador;
  }
}
~~~

Esta funcion nos ayuda a convertir los valores de entrada del sensor de temperatura a los valores de salida necesarios para que el motor funcione correctamente.

~~~ C
int regularMotor (void)
{//Lee el sensor de temperatura y con un map convierte los valores de entrada
 //a los valores de salida del motor
  int lecturaSensor = analogRead(SENSOR_TEMP);
  int conversorMotor = map(lecturaSensor,23,360,0,255);
  return conversorMotor;
~~~


## :robot: Link al proyecto
- [Proyecto: Segunda parte]https://www.tinkercad.com/things/bJJYaH2SSPe-parcialdomiciliariosegundapartevoutsinalabrinalejandro/editel?sharecode=A1AtrJkZ_Qv1wioe8osGD_uA8oiqcnVAlmrSiXRUoio



## Proyecto: Tercera parte
![tercera-parte](https://github.com/avoutsina/Parcial_Domiciliario/assets/138216833/f021b7ea-cc1a-482d-95d2-ddaffa4a6a78)

## Descripción
Se modifica la segunda parte agregandole un Fotodiodo, este nos determinara si el circuito funciona o no segun la señal que reciba.


## Función principal

En si se le implemento un analogread al Fotodiodo y segun el valor de que entrega el circuito fuciona con normalidad o en caso contrario, apaga los displays, el motor y reinicia el contador.
~~~ C
int prender_circuito = analogRead(FOTODIODO);
  //Si la lectura del fotodiodo es mayor a 0
  // el circuito funciona con normalidad
  if(prender_circuito > 0)
  {
    int boton_presionado = keypressed();

    if (digitalRead(SWITCH) == 0)
    {
      // Modo de contador normal
      if (boton_presionado == SUBE)
      {
        contador++;
        if (contador > 99)
        {
          contador = 0;
        }
      }
      else if (boton_presionado == BAJA)
      {
        contador--;
        if (contador < 0)
        {
          contador = 99;
        }
      }
    }
    else
    {
      // Modo de números primos
      if (boton_presionado == SUBE)
      {
        contador++;
        int nuevoContador = esPrimoSube(contador);
        contador = nuevoContador;
        if (contador > 99)
        {
          contador = 2;
        }

      }
      else if (boton_presionado == BAJA)
      { 
        contador--;
        int nuevoContador = esPrimoBaja(contador);
        contador = nuevoContador;
      }
    }
    imprimir_contador(contador);

    int velocidadMotor = regularMotor();


    analogWrite(MOTOR,velocidadMotor);
  }
else
  {//En caso contrario, se apagan los outputs
  // y se reinicia el contador
    digitalWrite(DECENA,HIGH);
    digitalWrite(UNIDAD,HIGH);
    analogWrite(MOTOR,0);
    contador=0;
  }
~~~

## :robot: Link al proyecto
- [Proyecto: Tercera parte][https://www.tinkercad.com/things/bJJYaH2SSPe-parcialdomiciliariosegundapartevoutsinalabrinalejandro/editel?sharecode=A1AtrJkZ_Qv1wioe8osGD_uA8oiqcnVAlmrSiXRUoio](https://www.tinkercad.com/things/ii5LYt26gaS-parcialdomiciliariotercerapartevoutsinalabrinalejandro/editel?sharecode=G2qVpEmgjDQnMbskhMFN4nzXICTM2DExqvhPaoxe4us)

  
