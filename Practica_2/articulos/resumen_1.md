# Resumen del Artículo: "Cuando México tiembla: la historia contada por los datos"



**1. Qué problema aborda y por qué importa**

México es un país con una alta exposición sísmica debido a su ubicación en el Cinturón de Fuego del Pacífico y a la compleja interacción de cinco placas tectónicas en su territorio[cite: 1]. Aunque instituciones como el Servicio Sismológico Nacional (SSN) registran una enorme cantidad de datos históricos, esta información suele ser muy técnica, visualmente poco amigable y difícil de interpretar para la población general, tomadores de decisiones o investigadores[cite: 1]. El problema central que aborda este trabajo es la dificultad para aprovechar y comprender de forma práctica la información sísmica[cite: 1]. Esto importa porque, al carecer de herramientas accesibles para visualizar y correlacionar los sismos con la realidad social y económica del país, se desaprovecha la oportunidad de mejorar la prevención, la gestión gubernamental ante desastres y la educación pública sobre el riesgo latente[cite: 1].

##

**2. De dónde provienen los datos, en qué formato estaban y qué tuvo que hacerse para poder usarlos**

* **Origen:** Los datos provienen de fuentes oficiales principales: el Servicio Sismológico Nacional (SSN), que proporciona un catálogo histórico con más de 300,000 sismos registrados en México desde el año 1900, y el Instituto Nacional de Estadística y Geografía (INEGI), que aporta información demográfica y económica a través de los Censos de Población y Vivienda 2020 y los Censos Económicos[cite: 1].
* **Formato y procesamiento:** Ambos conjuntos de datos se obtuvieron originalmente en **formatos tabulares tipo CSV** (valores separados por comas)[cite: 1]. Para poder utilizarlos de forma limpia y estructurada, los autores desarrollaron un programa en Python encargado de un proceso de validación: este script lee los archivos CSV, detecta y depura campos vacíos, corrige coordenadas inconsistentes o formatos incompatibles, elimina los registros inválidos y genera un código en lenguaje SQL estructurado para ser integrado en una base de datos[cite: 1].

##

**3. Cómo se modeló la información: qué entidades o dimensiones se identificaron, qué hechos se miden y cómo se relacionan**

Para estructurar la información de manera eficiente, la base de datos se diseñó bajo un esquema de almacén de datos (*data warehouse*) utilizando el manejador **PostgreSQL**[cite: 1]. En este modelo se identifican claramente los siguientes componentes:

* **Entidades y Dimensiones Principales:**
    * **Sismo:** Representa cada evento telúrico registrado. Sus **atributos** principales son: *fecha/hora, magnitud, profundidad, latitud y longitud (coordenadas del epicentro)*[cite: 1].
    * **Localidad / Población:** Representa los asentamientos humanos y centros urbanos. Sus **atributos** incluyen: *nombre de la localidad, número de habitantes (ej. poblaciones con 50,000 o más habitantes) y ubicación geoespacial*[cite: 1].
    * **Economía / Producción:** Contiene datos económicos y censales asociados a las regiones. Sus **atributos** abarcan indicadores de producción económica y datos censales por zona[cite: 1].
* **Hechos que se miden:** Se cuantifican métricas clave como el **total de sismos** en un periodo o región, la **magnitud máxima**, la **profundidad**, la **población potencialmente afectada** y las **correlaciones estadísticas** entre la magnitud del sismo y la profundidad o el impacto poblacional[cite: 1].
* **Relaciones:** Las entidades se relacionan de forma geoespacial y relacional. Mediante las coordenadas geográficas y los identificadores territoriales, el sistema vincula la entidad *Sismo* con la entidad *Localidad/Población* y los datos económicos del *INEGI*, permitiendo calcular distancias desde el epicentro hacia las zonas pobladas y determinar el cruce entre la actividad sísmica y el impacto socioeconómico en un estado o municipio específico[cite: 1].

##

**4. Qué preguntas concretas puede responder el sistema resultante**

Gracias al sistema de visualización interactivo y su base de datos integrada, es posible responder a diversas interrogantes prácticas, tales como:

* ¿Cuáles han sido los sismos de mayor magnitud registrados en un estado específico (por ejemplo, Jalisco) en un año determinado y cuál fue su distribución mensual[cite: 1]?
* ¿Qué localidades densamente pobladas (con más de 50,000 habitantes) se encuentran dentro del radio de afectación o cercanas a los epicentros de sismos con magnitudes superiores a cierto rango[cite: 1]?
* ¿Cuál es la correlación directa entre la magnitud de los sismos y la profundidad a la que ocurren, así como el volumen de población potencialmente afectada en esa zona[cite: 1]?
* ¿Cómo se distribuyen geográficamente los riesgos a través de mapas de calor y reportes personalizados ajustados por periodos de tiempo, rangos de profundidad o actividad económica[cite: 1]?

##

**5. Qué limitaciones reconocen los autores y qué trabajo futuro proponen**

* **Limitaciones:** Los autores señalan que la implementación y el despliegue de sistemas analíticos y bases de datos complejas pueden resultar difíciles o inaccesibles para usuarios con poco o nulo dominio técnico de las herramientas involucradas[cite: 1]. Para mitigar esto, recurrieron al uso de contenedores virtuales independientes con Docker Compose y distribuyeron el código en un repositorio público de GitHub, facilitando su ejecución mediante comandos simplificados[cite: 1].
* **Trabajo futuro:** Como siguientes pasos para evolucionar el proyecto, proponen habilitar **visualizaciones tridimensionales (3D)**, integrar **nuevas fuentes de datos oficiales** y conectar la plataforma con **sistemas de alerta temprana** para potenciar su utilidad en la prevención de desastres[cite: 1].

##

**Bibliografía**
