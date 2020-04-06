# **LABORATORIO BCD**

## Integrantes


Juan David Sandoval Suarez 39718;


Bryan Daniel Melo Guzman 49686;


Fabian Santiago Martin Morantes 60821;

# Introducci贸n

Para la realizaci贸n de este laboratorio, utilizamos los c贸digos base que el profesor nos proporcion贸 para el correcto funcionamiento del laboratorio. Cabe resaltar que se debe entender cada l胣ea del c贸digo para poder tener un mejor entendimiento a la hora de hacer preguntas que surgen a lo largo del laboratorio.   

## Dise帽o BCD-7seg

Para el dise帽o de un display de 7 segmentos y su respectiva visualizaci贸n, se debe implementar el c贸digo base que tenemos y entender cada l胣ea para as� poder conseguir conocimientos m谩s exactos al momento de implementar m谩s displays.




En este punto, ya se estar en la capacidad de describir e implementar Hardware sencillo, con la ayuda de herramientas computaciones.  y como se vio en los dos ejemplos anteriores, la suma se visualiza en leds,  algo que es dif铆cil para  validad visualmente la respuesta. Por lo tanto, es aconsejable tener una visualizaci贸n mas acorde a las necesidades, como por ejemplo  visualizar los resultados en el [ Display 7 Segmentos](https://en.wikipedia.org/wiki/Seven-segment_display) 

En este Ejercicio se propone que realicen el dise帽o, sintentizaci贸n e implementaci贸n del Display de 7 sergmentos, el cual permita visualizar n煤meros  en representaci贸n hexadecimal (0x0 a 0xF).  En el siguiente gr谩fico, se observa cual es el funcionamiento deseado del display:


![gif display](https://upload.wikimedia.org/wikipedia/commons/2/2b/Seven_segment_display-animated.gif)

Imagen tomada de [User:Guam + Various](https://commons.wikimedia.org/wiki/File:Seven_segment_display-animated.gif)

A continuaci贸n se presentan los pasos recomendados para el ejercicio:

**Definir la caja funcional del BCD**: 

![bcd_black](https://github.com/Fabeltranm/SPARTAN6-ATMEGA-MAX5864/blob/master/lab/lab03-BCD2SSeg/doc/BCD2SSeg.jpg)

Si observa la caja negra/ funcional  ademas  de la salidad de 7 segmentos contiene  una salida `An`. esta salida es para conectar eventualmente el 谩nodo del display y  poder hacer visualizaci贸n din谩mica, cuando se tiene mas de un display conectado.


**Definir la descripci贸n Funcional**

Un display 7 segmentos es un visualizador de numeros o letras dependiendo de la conexion externa para lo que se desee implementar. Esta construido por unos leds que tienen unas conexiones internas para su correcto funcionamiento, existen dos tipos de visualizadores y se diferencian en la entrada de alimentacion. 

**Anodo Comun:** Este visualizador tiene todos los anodos de los leds conectados internamente. Para poder encender cada uno de los segmentos, se debe aplicar un potencial negativo (en logica binaria 0).

**Catodo Comun:** Este visualizador tiene todos los catodos de los leds conectados internamente. Para poder encender cada uno de los segmentos, se debe aplicar un potencial positivo (en logica binaria 1).

Se recomienda implementar externamente una resitencia detro de lo posible de 330? a cada segmento del display para asi poder limitar la corriente.
Despues de tener claro lo anterior, procedemos a realizar la tabla de verdad del visualizador de 7 segmentos (display), para cada numero y/o letra que se desee ver. Para ello se tiene en cuenta la conexion interna del display que se presenta a continuacion:

![imagen_display_7_seg](https://http2.mlstatic.com/display-7-segmentos-D_NQ_NP_965598-MLM29489271353_022019-F.jpg)

De la anterior imagen podemos sacar las siguientes tablas de verdad:

![tabla_de_verdad](https://http2.mlstatic.com/display-7-segmentos-D_NQ_NP_965598-MLM29489271353_022019-F.jpg)





dbnfvjfd vodjfj klvckjeufn f

Para ello recuerde  que puede hacer uso, bien sea, de las tablas de verdad o de la descripci贸n algor铆tmica del BCD a  siete segmentos. Recuerde que cada Segmento es una salida  del dise帽o. Ejemplo, si desea  visualizar el n煤mero **1**, la salida seria  de `Sseg es 0110000`. observe la gr谩fica a continuaci贸n, para generar las salidas acorde al n煤mero de entrada.

![sseg](https://upload.wikimedia.org/wikipedia/commons/thumb/0/02/7_segment_display_labeled.svg/1024px-7_segment_display_labeled.svg.png)


* Definir en  HDL el comportamiento del sistema ** :  Use Verilog para hacer la descripci贸n funcional
**simulaci贸n de Sistema** :  Use el Testbench para este fin.


# Ejercicio - Visualizaci贸n Din谩mica 4 Display


Si el dise帽o digital de alg煤n sistema se requiere mas de un display de 7 segmentos, es necesario  generar una visualizaci贸n tal que sea necesario el menor n煤mero de pines para conectar todos los display en con la FPGA.

Por ahora, se ha visualizado el n煤meros en un solo display de 7 segmentos. Pero en la mayor铆a de los casos, los 7 pines de los c谩todos est谩n inter-conectados entre cada display, como se observa en la figura:

![conex](https://github.com/Fabeltranm/SPARTAN6-ATMEGA-MAX5864/blob/master/lab/lab04_display_7segx4/doc/conex.png)

Por lo tanto, se debe  realizar una multiplexaci贸n  entre los Anodos de cada Display, con el fin de visualizar en cada display un n煤mero diferente.  En otras palabras, en cada instante de tiempo, solo un display se encuentra activo. En este sentido, se debe garantizar que el destello en la visualizaci贸n entre cada display no se perciba. Para ello, cada display debe activarse m谩ximo cada 16 ms.

Visualmente esto se entiende mas con la siguiente simulaci贸n, donde se desea visualizar el  n煤mero en representaci贸n hexadecimal `0x4321`:


![diagrama](https://github.com/Fabeltranm/SPARTAN6-ATMEGA-MAX5864/blob/master/lab/lab04_display_7segx4/doc/4sseg.jpg)


## Diagrama Caja negra 

Como siempre, antes de realizar la descripci贸n del hardware se debe dise帽ar la caja funcional del modulo, con las entradas y salidas

![diagrama caja negra ](https://github.com/Fabeltranm/SPARTAN6-ATMEGA-MAX5864/blob/master/lab/lab04_display_7segx4/doc/display_7segx4.jpg)

En este sentido, se adiciona al HDL de siete segmentos 4 se帽ales de control para el LCD, llamadas An. cada bit de la se帽al `An` debe ser modificado en el tiempo, con el fin de activar solo un display.  

## Diagrama Estructural 

![estructural](https://github.com/Fabeltranm/SPARTAN6-ATMEGA-MAX5864/blob/master/lab/lab04_display_7segx4/doc/display_7segx4_Diag_Estructural.jpg)

Se evidencia que se deben construir cuatro m贸dulos  b谩sicos, de los cuales uno de ellos esta descrito en el ejercicio anterior, [BCDtoSSeg.v](https://github.com/Fabeltranm/SPARTAN6-ATMEGA-MAX5864/blob/master/lab/lab04_display_7segx4/src_ise_basys2/display_7segx4/BCDtoSSeg.v) . Los otros tres bloques son:

* Divisor de frecuencia: Su funci贸n es dividir la frecuencia de  `clk` de entrada, en el tiempo requerido para cada camvio de 谩nodo
* Selector de 脕nodo: Sincronizado con la frecuencia  que genera el divisor, cambia en cada instante de tiempo el  谩nodo, se puede ver como un registro de desplazamiento del bit 0 `1110 1101 1011 0111`
* Selector de Datos: dependiendo del 谩nodo activado, activa los datos correspondientes.

# Entregables

Una vez clone el repositorio y lea la anterior guia, realice lo siguiente:

En el paquete de trabajo [WP04](https://classroom.github.com/g/zCBwHHKX)   esta la descripci贸n del hardware que se implementa para visualizar un n煤mero hexadecimal de 32 bits en un display  y en 4 display de 7 segmentos.


* Comprenda cada l铆nea del c贸digo HDL de los  archivos que se encuentra en la carpera src. Si cree necesario realice los respectivos comentarios en el mismo archivo y comente
* Realice en quartus la simulaci贸n para el BCD-7seg, analice los resultados.
* Cree el nuevo proyecto HDL para Visualizaci贸n Din谩mica 4 Display, tomando como base los archivos dados.
* Creer el archivo testbench.v
* Genera la simulaci贸n, Revise que el sistema funciona como usted lo esperaba. Realice lo comentarios necesarios en el archivo README.md.
* Modificar o A帽adir los bloques necesarios para que la visualizaci贸n sea en representaci贸n Decimal y no Hexadecimal.
* Realice la respectiva publicaci贸n del repositorio antes de la fecha dada con todo el c贸digo  fuente 

# HDL

## 7 Segmentos 1 Display

```verilog 

module BCDtoSSeg (BCD, SSeg, an);

  input [3:0] BCD;
  output reg [0:6] SSeg;
  output [3:0] an;

assign an=4'b1110;

//programacion para 7 segmentos de anodo comun
always @ ( * ) begin
  case (BCD)//Inicio de casos en orden decendente
   4'b0000: SSeg = 7'b0000001; // "0"  
	4'b0001: SSeg = 7'b1001111; // "1" 
	4'b0010: SSeg = 7'b0010010; // "2" 
	4'b0011: SSeg = 7'b0000110; // "3" 
	4'b0100: SSeg = 7'b1001100; // "4" 
	4'b0101: SSeg = 7'b0100100; // "5" 
	4'b0110: SSeg = 7'b0100000; // "6" 
	4'b0111: SSeg = 7'b0001111; // "7" 
	4'b1000: SSeg = 7'b0000000; // "8"  
	4'b1001: SSeg = 7'b0000100; // "9" 
	//paso de binario a hexa
   4'ha: SSeg = 7'b0001000;	//A
   4'hb: SSeg = 7'b1100000;	//B
   4'hc: SSeg = 7'b0110001;	//C
   4'hd: SSeg = 7'b1000010;	//D
   4'he: SSeg = 7'b0110000;	//E
   4'hf: SSeg = 7'b0111000;	//F
    default:
    SSeg = 0;
  endcase
end

endmodule
```