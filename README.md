# Servicios en Red - Práctica 2: DNS
**DNS (Domain Name System)** es un sistema que traduce nombres de dominio legibles por humanos a direcciones IP numéricas que las computadoras utilizan para identificarse en la red. En esta práctica, exploraremos los conceptos básicos de DNS, su funcionamiento y cómo se implementa en un entorno de red.

## Sistemas de Direccionamiento Planos y Jerarquicos

Un sistema de direccionamiento es una metodo o conjunto de reglas que permite asignar, organizar y localizar identificadores unicos dentro de un conjunto de elementos. Se puede clasificar en dos tipos principales: planos y jerárquicos.

- **Planos**: En un sistema de direccionamiento plano, todos los nombres de dominio están en un mismo nivel y se resuelven de manera independiente. 

Un ejemplo de sistema de direccionamiento plano seria asignar a cada vivienda un número o nombre único sin importar su ubicación. Esto es sencillo a pequeña escala, pero a gran escala se vuelve imposible de gestionar.

- **Jerárquicos**: En un sistema de direccionamiento jerárquico, los nombres de dominio se organizan en una estructura de árbol, lo que permite una resolución más eficiente y una mejor gestión de los recursos. 

Un ejemplo de sistema de direccionamiento jerárquico es el que utilizamos en la vida real, donde las viviendas se organizan en portales, pisos, calles, ciudades y países. Esto facilita la localización y gestión de direcciones a gran escala.

## Espacio de Nombres
El espacio de nombres en DNS es una estructura jerárquica que organiza los nombres de dominio en diferentes niveles. Cada nivel del espacio de nombres se separa por un punto (.) y se lee de derecha a izquierda.

- **Raíz**: El nivel más alto del espacio de nombres es la raíz, representada por un punto (.). No se muestra explícitamente en los nombres de dominio, pero es el punto de partida para la resolución de nombres.
- **Dominios de Nivel Superior (TLD)**: Estos son los dominios que se encuentran directamente debajo de la raíz y representan las categorías más generales de nombres de dominio. Ejemplos de TLD incluyen .com (comercial), .org (organización), .net (red), entre otros.
- **Dominios de Segundo Nivel (SLD)**: Estos son los dominios que se encuentran directamente debajo de los TLD y suelen representar organizaciones o entidades específicas. Por ejemplo, en el dominio `example.com`, `example` es el dominio de segundo nivel.
- **Subdominios**: Los subdominios son divisiones adicionales dentro de un dominio de nivel superior. Por ejemplo, en el dominio `example.com`, `blog.example.com` es un subdominio. Los subdominios pueden tener sus propios registros DNS y pueden ser utilizados para organizar servicios específicos dentro de una organización.

### Tipos de Dominios de Primer Nivel (TLD)
Los dominios de primer nivel (TLD) se pueden clasificar en varias categorías:

- **TLD Genéricos (gTLD)**: Son dominios que no están asociados a un país específico y pueden ser utilizados por cualquier persona o entidad. Ejemplos incluyen .com, .org, .net, .info, entre otros.

- **TLD de Código de País (ccTLD)**: Son dominios que están asociados y gestionados por un país o territorio específico. Por ejemplo, .es para España, .fr para Francia, .jp para Japón, etc.

- **TLD Patrocinados (sTLD)**: Son dominios que están regulados por una organización específica y tienen requisitos de elegibilidad. Ejemplos incluyen .edu (educación), .gov (gobierno), .mil (militar), entre otros.

Los TLD están gestionados por la ICANN (Internet Corporation for Assigned Names and Numbers), que supervisa la asignación y administración de nombres de dominio a nivel global. En los ultimos años, se han introducido muchos TLD nuevos para ampliar las opciones disponibles para los usuarios. Como por ejemplo, .app, .dev, .design, entre otros.

Algunos TLD de código de país (ccTLD) también se utilizan de manera creativa para representar palabras o conceptos específicos. Por ejemplo, .tv (Tuvalu) se utiliza comúnmente para sitios web relacionados con la televisión y los medios de comunicación. O .me (Montenegro) se utiliza a menudo para sitios web personales. O .ai (Anguila) se utiliza para proyectos relacionados con la inteligencia artificial. O .co (Colombia) se utiliza como una alternativa corta a .com para empresas y startups. O .io (Territorio Británico del Océano Índico) es popular entre las empresas de tecnología y startups, ya que "IO" puede interpretarse como "input/output" (entrada/salida) en el contexto informático.


## Como y quien gestiona los TLD y SLD
La gestión de los TLD y SLD es un proceso colaborativo que involucra a varias entidades:

- **ICANN (Internet Corporation for Assigned Names and Numbers)**: Es la organización responsable de coordinar y supervisar el sistema de nombres de dominio a nivel global. ICANN gestiona la asignación de TLD y establece políticas para su administración.
- **Registradores de Dominios**: Son empresas acreditadas por ICANN que permiten a los usuarios registrar nombres de dominio bajo los TLD y SLD disponibles. Estos registradores actúan como intermediarios entre los usuarios y ICANN, facilitando el proceso de registro y gestión de dominios.
- **Registros de Dominios**: Son organizaciones responsables de la administración técnica y operativa de un TLD específico. Por ejemplo, Verisign es el registro para el TLD .com y .net, mientras que Nominet gestiona el TLD .uk. Los registros mantienen las bases de datos de nombres de dominio y aseguran que las solicitudes de resolución se dirijan correctamente a los servidores DNS correspondientes. Estas, son las organizaciones que poseen y operan los servidores TLD.
- **Propietarios de Dominios**: Son los individuos o entidades que registran y poseen nombres de dominio bajo un TLD o SLD específico. Los propietarios son responsables de mantener la información de contacto y configuración técnica asociada con su dominio.

## Delegación de Dominios
La delegación de dominios es el proceso mediante el cual la autoridad para gestionar un dominio se transfiere a otra entidad. Esto permite que los propietarios de dominios deleguen la administración de sus subdominios a otros servidores DNS. Por ejemplo, un dominio de nivel superior (TLD) puede delegar la gestión de un dominio de segundo nivel (SLD) a un registrador de dominios, que a su vez puede delegar la gestión de subdominios a otros servidores.

Por ejemplo, si tienes el dominio `example.com`, puedes delegar la gestión del subdominio `blog.example.com` a un servidor DNS diferente al que gestiona `example.com`. Esto se logra mediante la creación de registros NS (Name Server) en el servidor DNS principal, que indican qué servidores son responsables de resolver los nombres dentro del subdominio delegado.

## Funcionamiento de DNS
En el funcionamiento de DNS, hay varios actores involucrados que desempeñan roles clave en la resolución de nombres de dominio:

- **Servidores Raíz**: Son los servidores DNS de nivel más alto en la jerarquía de DNS. Estos servidores contienen información sobre los TLD y dirigen las consultas a los servidores correspondientes.
- **Servidores TLD**: Son responsables de gestionar los TLD específicos y dirigir las consultas a los servidores de nombres autoritativos para los dominios de segundo nivel (SLD) dentro de ese TLD.
- **Servidores de Nombres Autoritativos**: Son los servidores DNS que contienen la información completa sobre un dominio específico. Estos servidores responden a las consultas con la información necesaria para resolver el nombre de dominio a una dirección IP.
- **Resolvers**: Son los clientes DNS, es decir, los dispositivos o aplicaciones que realizan las consultas DNS en nombre de los usuarios. En general, los resolvers serán servidores externos que harán las consultas DNS por nosotros, aunque también pueden ser los propios dispositivos de los usuarios. Un resolver habitual es el de Google (8.8.8.8).

Normalmente, cuando un usuario intenta acceder a un sitio web, su computadora envía una consulta DNS a un servidor DNS. Este servidor se encarga de buscar la información necesaria consultando los servidores raíz, TLD y autoritativos en el orden adecuado hasta obtener la dirección IP correspondiente al nombre de dominio solicitado.

Además, se utilizan una serie de mecanismos con el fin de optimizar y agilizar el proceso de resolución de nombres de dominio:

- **Caché**: Los servidores DNS y los clientes almacenan durante un tiempo las respuestas a las consultas DNS para reducir la latencia y la carga en los servidores. Esto significa que si un usuario solicita el mismo nombre de dominio varias veces, es posible utilizar la respuesta almacenada en lugar de realizar una nueva consulta.
- **Consultas Recursivas**: En este tipo de consulta, el servidor DNS recibe una solicitud de un cliente y se encarga de resolverla completamente, realizando todas las consultas necesarias a otros servidores DNS hasta obtener la respuesta final.
- **Uso de Anycast**: Los servidores DNS pueden utilizar direcciones anycast para distribuir la carga de consultas entre múltiples servidores ubicados en diferentes lugares geográficos. Esto mejora la disponibilidad y reduce la latencia al dirigir las consultas al servidor más cercano.
- **Balanceo de Carga**: Los servidores DNS pueden implementar técnicas de balanceo de carga para distribuir las consultas entre múltiples servidores, mejorando así la capacidad de respuesta y la disponibilidad del servicio.
- **Redundancia**: Es común que los dominios tengan múltiples servidores de nombres autoritativos para garantizar la disponibilidad del servicio en caso de fallos en uno de los servidores.

### Flujo de Resolución DNS
El flujo de resolución DNS generalmente sigue estos pasos:

1. El usuario ingresa un nombre de dominio en su navegador web.
2. El navegador envía una consulta DNS al servidor de nombres recursivo configurado en la configuración de red del dispositivo.
3. El servidor de nombres recursivo verifica si tiene la respuesta en caché.
4. Si la respuesta no está en caché, el servidor recursivo envía una consulta al servidor raíz.
5. El servidor raíz responde con la dirección del servidor TLD correspondiente.
6. El servidor recursivo envía una consulta al servidor TLD.
7. El servidor TLD responde con la dirección del servidor de nombres autoritativo para el dominio solicitado.
8. El servidor recursivo envía una consulta al servidor de nombres autoritativo.
9. El servidor autoritativo responde con la dirección IP asociada al nombre de dominio.
10. El servidor recursivo almacena la respuesta en caché y la envía de vuelta al cliente.
11. El navegador utiliza la dirección IP para establecer una conexión con el servidor web y cargar el sitio solicitado.

[Flujo de Resolución DNS](img/flujo.png)

## Parte Práctica
En esta práctica, desplegaremos un servidor DNS para un dominio propio dentro de nuestra red local utilizando **dnsmasq**, una herramienta ligera y fácil de configurar para proporcionar servicios de DNS.

### Preparación del Entorno

En esta práctica, utilizaremos 4 maquinas virtuales en VirtualBox para simular una red local con un servidor DNS y varios clientes. Recuerdo que no es lo mismo el nombre de la máquina que el nombre de la vm en VirtualBox. Uno es el hostname y otro es el nombre que le damos en VirtualBox para identificarla.

Las maquinas se deberan llamar `debian1`, `debian2`, `debian3` y `debian4`. Recomiendo llamarlas en VirtualBox `Practica3-SR-debian1`, `Practica3-SR-debian2`, `Practica3-SR-debian3` y `Practica3-SR-debian4` respectivamente para tenerlas identificadas.

Las podeis crear a partir de una maquina debian base que ya tengais creada y con vuestro usuario. Recordad hacer una clonación enlazada y seleccionar la opción de "Generar nuevas direcciones MAC".

`debian1` sera el servidor DNS y las otras tres seran clientes que consultaran al servidor DNS.

Tambien configuraremos el adaptador 2 de cada una de las maquinas en modo "Red Interna" con el nombre de red `inet` para que todas las maquinas puedan comunicarse entre si.

#### En Todas las Masquinas

Recuerdo que para cambiar el nombre de la maquina (hostname) en Debian, se puede editar el contenido del archivo `/etc/hostname` y luego reiniciar la maquina.

El archivo `/etc/hosts` se encarga de almacenar las correspondencias entre nombres de host y direcciones IP de manera local en cada maquina. En otras prácticas, hemos estado utilizando este archivo para asignar nombres a las maquinas de nuestra red local. Pero ahora, sera el servidor DNS el encargado de resolver los nombres de las maquinas en la red.

Tambien tendremos que editar el archivo `/etc/hosts` para que el nombre de la maquina apunte a la IP correcta. Es decir, en `127.0.0.1`, que siempre apunta a la propia maquina, pondremos el nombre `localhost` y en `127.0.1.1`, pondremos el nombre de la maquina. Ademas eliminaremos otras lineas en las que guardemos la ip de otras maquinas, ya que ahora sera el servidor DNS el encargado de resolver esos nombres.

Primeras lineas de /etc/hosts:

```
127.0.0.1       localhost
127.0.1.1       <nombre_maquina>

```

Las ultimas lineas no las modificaremos.

### Configuración de las Interfaces de Red
#### En Todas las Maquinas
Al conectar a nuestras maquinas un nuevo adaptador, aparecera una nueva interfaz de red en el sistema operativo encargada de gestionar esa conexión. Esta interfaz de red tendremos que configurarla en el archivo /etc/network/interfaces. Podemos identificar la nueva interfaz de red creada con el comando `ip a`, normalmente sera `enp0s8`.

En el archivo `/etc/network/interfaces`, añadiremos la siguiente configuración para que obtenga una dirección IP estática:

```
auto enp0s8
iface enp0s8 inet static
    address 192.168.56.X
    netmask 255.255.255.0
```

Donde `X` sera un numero de la máquina, `192.168.56.1` para `debian1`, `192.168.56.2` para `debian2`, `192.168.56.3` para `debian3` y `192.168.56.4` para `debian4`.

Después de realizar estos cambios, reiniciaremos el servicio de red con el comando `sudo systemctl restart networking` o reiniciaremos la maquina para que los cambios se apliquen correctamente.

### Configuración del Servidor DNS (debian1)
#### EN  debian1
Primero instalaremos dnsmasq, un software ligero que proporciona servicios de DNS. Podemos instalarlo utilizando el siguiente comando:

```
sudo apt update
sudo apt install dnsmasq
```

Una vez instalado, configuraremos dnsmasq para que actúe como nuestro servidor DNS. Editaremos el archivo de configuración principal de dnsmasq ubicado en `/etc/dnsmasq.conf`. Añadiremos las siguientes líneas al final del archivo:

```
# /etc/dnsmasq.conf

# Dominio local que gestionará dnsmasq
domain=midominio.local

# Dirección IP que se asignará a cada nombre
address=/debian1/192.168.56.1
address=/debian2/192.168.56.2
address=/debian3/192.168.56.3
address=/debian4/192.168.56.4

# Interfaz en la que dnsmasq escuchará (opcional pero recomendable)
interface=eth0

# Evita que escuche en otras interfaces (opcional)
bind-interfaces
```

Después de realizar estos cambios, reiniciaremos el servicio de dnsmasq para que los cambios se apliquen correctamente:

```
sudo systemctl restart dnsmasq
```

### Configuración de los Clientes DNS (debian2, debian3, debian4)
#### EN debian2, debian3, debian4
En cada una de las maquinas cliente, configuraremos el resolver DNS para que utilice nuestro servidor DNS (debian1) para resolver los nombres de dominio.
Editaremos el archivo `/etc/resolv.conf` y **añadiremos** la siguiente línea al principio del archivo:

```
nameserver 192.168.56.1
```

Es importante añadir esta línea al principio del archivo para asegurarnos de que el sistema utilice nuestro servidor DNS antes que cualquier otro servidor configurado. Tambi
