# alarmabarrial
Alrama comunitaria, para avisar en la cuadra, o en el barrio cuando dejaron a un vecino o varios sin Luz. Tecnologias: LoraWan, App Movil, Unidad hogareña (bateria, bocina, luz, Lora, detectores)

## Objetivo: 
El objetivo inicial es crear una alarma ecnonómica que este al alcance de los vecinos del barrio para avisarnos y activarse cuando a alguien le cortan la luz.
Si bien es cierto que pueden existir cortes de luz generales, el objetivo es contar con un sistea que advierta de cortes puntales y tenga la capacidad de detectar si el corte es general o no. Por ejemplo si todos los vecinos tienen corte no se dispara mimguna alarma pues parece ser un problema de la red electrcia. En cambio si el corte es de solo unos vecinos y de la misma acera, se entiende que el corte es por accion maliciosa para luego tratar de acceder al hogar sin tener disponnibles camaras ni sistemas IP de alarma / monitoreo.

## Tecnologias:
Existen varias partes de este proyecto por lo que vamos a ir modificando esta sección de forma frecuente, pero la idea principal esta en los siguientes módulos.

### Comunicaciones
Aqui podemos tener alguna variante no establecida aun, pero la idea es contar con un sistema que no implique costos mensuales, por eso no es que lo utilizaremos con un chip de datos o vos celculares. Tampoco con la red Wifi hogareña, pues la misma queda desactivada al perder la corriente, por lo que tenemos según nuestars capacidades dos opciones. *LORA* o *RF* Debido al corto alcance necesario y a la opcion de trabajar en mesh, haciendo que cada unidad hogareña sea repetidora de la otra, pensamos en que cualquiera de las dos puede ser una biena solucion, solo hay que estudiar, viabilidad de HW, costos y alcances reales.

### Unidad hogareña
La unidad hogareña, será una caja estanco de metal o plastico, la cual cuente en su interior con una bateria, una conexión a 220V, un disyuntor, un esp32 o similar con lora o RF, una bocina de 12v y una luz estroboscopica de 12v, un par de led, un rojo que indica que esta funciando la bateria, uno verde que indica que recibe 220v y si ese iene otro coloro, que se configure en amarillo o se pone otro para indicar cuando falta 220v. Por ultimo un shitch para desconectar el sistma por x motivo.
Además estara conectado a wifi cuando tiene corriente, para envir la información propia y si recibe de otra unidad también, la info mediante MQTT o similar un servidor exterior.
En caso de falta de wifi (por energia o corte de cable de fibra), no se podra enviar la alerta por wifi, es por esto que el dispositivo lora se comunicara con otro lora del barrio para transmitir su señal, esto aprecera ademas en el panel como alerta de vecnio y llegara por push a las app necesarias.

Se puede dejar nuevas adiciones para mas adelante, como sensor de inciendio.


### App Movil
Las app moviles principalmente contara con un sistema de push para avisar cuando algun vecino esta con la arama activada, ademas de poder acceder a un panel del barrio y ver cuales son las alarmas activadas, ademas de tener un estado del tiempo si es posible para saber si hay fuertes vientos y tormenta electrica que pueden haber generado una falsa alarma.
A su vez la app puede tener botón de panico para activar su propia alarama y avisar al resto.

### Servidor Central
El servidor central es el que recibira mediante MQTT las alramas de los vecinos, ya sea mediante boton de panico o sistema automatico por falta de energia de red. Tambien puede geenrar alertas por falta de señal de un vecino, lo cual puede indciar robo de la unidad o falta de bateria.

Si llega un mensaje de alarma desde una unidad hogareña, se activa la alarma en ese hogar y si la alarma tiene diferentes tonos, se puede activar con otro tono de alerta en el resto de los vecinos.

En el caso que lo que se haya acionado sea el boton de panico, se activara en caso de que existan dos alamras (o modos de sonidi) la alarma secundaria, si solo hay una, pues se activa la única

### Dispositivo de pánico
Se puede añadir un dispositivo de pánico con un boton lora para enviar la señal a la unidad hogareña y que esta a su vez la envie al servidor.

## Plataformas y tecnologias
Si bien estamos en una etapa inicial, la idea es utilizar difernetes tecnologias por modulos.

Una opcion viable puede ser instalar https://openremote.io/ el cual sirve como servidor, dashboard e incluye una app movil que puede utilizarse, hay que estudiarlo....

### Unidad Hogareña
esp32 con arduino para el manejo de los dispotivos hogareños y Lora

###Servidor Cenrtal 
Un servidor en la nube, el cual puede ser varias opciones, por ejemplo Vercel, y el mismo u otro que maneje MQTT

### App Movil
Para las app moviles se puede usar flutter o algo tipo Ionic



