INTRODUCCIÓN

Este informe describe un sistema electrónico que permite controlar la intensidad de tres LED de manera gradual, visualizando el ciclo de trabajo (duty cycle) de la señal de control. 
El sistema utiliza modulación por ancho de pulso (PWM) para regular la cantidad de tiempo que los LED permanecen encendidos durante un período determinado. 
Esto permite ajustar la percepción de brillo de los LEDs.

CONFIGURACIÓN 

El system clock del microcontrolador se configuro a 72Mhz.
La blue pill utiliza 12bits de resolución (4096) en el ADC para convertir las señales analógicas en digitales, por ende, 
los valore que leeremos del Potenciómetro serán 0 en su valor mínimo y 4096 en su valor máximo. Se utilizará el ADC1, 
habilitando continuous conversión mode, con un tiempo de muestreo de 239.5 ciclos, además de habilitar la interrupción del ADC.
Para la comunicación se utilizó el USART3, sin interrupcion. También se utilizará el timer 1, se configuro el APB2 a 9MHz, 
un prescaler a 180-1 y el counter period de 1000 para obtener una frecuencia de 50Hz. 

![image](https://github.com/ErickDiaz2001/Ejercicio_6/assets/169405943/fb017e92-4440-420e-a0ff-9e63ceb6edeb)

![image](https://github.com/ErickDiaz2001/Ejercicio_6/assets/169405943/f15091ba-ddfb-4c54-a7fd-05209ec8bcee)

COMPONENTES DEL SISTEMA

El sistema se compone de los siguientes elementos

•  MICROCONTROLADOR: Un microcontrolador, es el cerebro del sistema. Se encarga de generar la señal PWM y regular la intensidad lumínica a los LEDs. 

•  LEDs: Los LEDs son los dispositivos que emiten luz. En este caso, se utilizan tres LEDs para demostrar el control de intensidad individual. 

•  POTENCIÓMETRO: Un potenciómetro se utiliza como entrada para el usuario, permitiendo ajustar el ciclo de trabajo de la señal PWM y, en consecuencia, la intensidad de los LEDs.

•	INCLUSIÓN DE BIBLIOTECAS:

o	stdio.h: contiene las definiciones y funciones básicas que nos permite realizar operaciones de entrada y salida en C, como printf() y scanf().

o	itoa.h: convierte el número entero n en una cadena de caracteres.

LECTURA DEL VALOR DEL ADC:

	Se utiliza la función HAL_ADC_GetValue() para leer el valor del ADC y guardarlo en una variable de de 16 bits.

	Para cambiar los valores del potenciómetro de 0 – 4095 a 0 – 1000 correspondiste al tiempo en estado alto, se utilizó la función map para convertir números de un rango a otro y guardarlos en el registro CCR1.

o	CÁLCULO DEL VOLTAJE REAL:

	Se calcula el voltaje real utilizando la siguiente fórmula: Voltaje = (adc_Valor * Voltaje de referencia) / (2^Resolución)

	La fórmula toma en cuenta el valor leído del ADC (adc_Valor), la tensión de referencia del ADC (3.3V) y la resolución del ADC.

o	IMPRESIÓN DEL RESULTADO:

	Se utiliza la función printf() para imprimir en la UART el valor leído del ADC ("ADC CH1 value: ") seguido del valor leído, luego se imprimir el mensaje "Max sample value: " seguido del valor máximo posible de la lectura (1024).

	Otra opción es de utilizar la función itoa() para la conversión de los valores e imprimirlo mediante hal_uart_transmit().

FUNCIONAMIENTO DEL SISTEMA

El microcontrolador genera una señal PWM con una frecuencia fija y un ciclo de trabajo variable. 
El ciclo de trabajo se determina por el valor del potenciómetro. La señal PWM controla la cantidad de tiempo que los LEDs permanecen encendidos. 
Cuanto mayor sea el ciclo de trabajo, más tiempo estarán encendidos los LEDs y mayor será su intensidad percibida.
En una terminal se muestra el valor del ciclo de trabajo en tiempo real, permitiendo al usuario observar cómo afecta el ajuste del potenciómetro a la intensidad de los LEDs.

ANÁLISIS DE RESULTADOS 
 
![image](https://github.com/ErickDiaz2001/Ejercicio_6/assets/169405943/489da8ad-97c1-45b6-b244-93f9877ccc8b)

https://youtu.be/-86ixYuWPiQ

CONCLUSIÓN

El sistema de control de intensidad de LED con ciclo de trabajo variable es una herramienta versátil y útil para controlar la intensidad de la luz emitida por LEDs. 
El sistema es fácil de implementar y tiene una amplia gama de aplicaciones.

