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
- **Registros de Dominios**: Son organizaciones responsables de la administración técnica y operativa de un TLD específico. Por ejemplo, Verisign es el registro para el TLD .com y .net, mientras que Nominet gestiona el TLD .uk. Los registros mantienen las bases de datos de nombres de dominio y aseguran que las solicitudes de resolución se dirijan correctamente a los servidores DNS correspondientes.
- **Propietarios de Dominios**: Son los individuos o entidades que registran y poseen nombres de dominio bajo un TLD o SLD específico. Los propietarios son responsables de mantener la información de contacto y configuración técnica asociada con su dominio.

## Delegación de Dominios
La delegación de dominios es el proceso mediante el cual la autoridad para gestionar un dominio se transfiere a otra entidad. Esto permite que los propietarios de dominios deleguen la administración de sus subdominios a otros servidores DNS. Por ejemplo, un dominio de nivel superior (TLD) puede delegar la gestión de un dominio de segundo nivel (SLD) a un registrador de dominios, que a su vez puede delegar la gestión de subdominios a otros servidores.

Por ejemplo, si tienes el dominio `example.com`, puedes delegar la gestión del subdominio `blog.example.com` a un servidor DNS diferente al que gestiona `example.com`. Esto se logra mediante la creación de registros NS (Name Server) en el servidor DNS principal, que indican qué servidores son responsables de resolver los nombres dentro del subdominio delegado.

## Funcionamiento de DNS

### Name Servers

### Resolvers