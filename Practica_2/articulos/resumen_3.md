# Resumen del Artículo: Territorial Information Retrieval from Heterogeneous Open Data through the Construction of a Data Warehouse for Water Management in Mexico City

## 

**1. Qué problema aborda y por qué importa**

La Ciudad de México enfrenta una grave crisis hídrica provocada por la sobreexplotación de los mantos acuíferos, las fugas en la red hidráulica y el crecimiento poblacional[cite: 22]. Aunque existen datos abiertos sobre el consumo de agua proporcionados por el Sistema de Aguas de la Ciudad de México (SACMEX), estos se encuentran en formatos poco accesibles y carecen de herramientas de consulta, lo que limita su utilidad para la toma de decisiones basada en evidencias[cite: 22, 23]. El problema central que aborda este trabajo es la dificultad para extraer, consolidar y consultar de forma práctica datos abiertos heterogéneos[cite: 23, 25]. Esto importa porque, al transformar registros dispersos en un repositorio dimensional consultable, se facilita el diagnóstico urbano, la investigación y el monitoreo ciudadano transparente sobre la gestión del agua[cite: 22].

## 

**2. De dónde provienen los datos, en qué formato estaban y qué tuvo que hacerse para poder usarlos**

* **Origen de los datos:** Los datos provienen del portal de datos abiertos de la Ciudad de México publicados por SACMEX, específicamente el recurso "Consumo Agua (1er Semestre 2019)", además de series meteorológicas complementarias obtenidas de Open-Meteo y bases cartográficas de OpenStreetMap[cite: 25, 26, 27].
* **Formato y procesamiento:** Los datos originales se encontraban en archivos tabulares de tipo CSV con problemas de dispersión y falta de estandarización[cite: 22, 25]. Para poder utilizarlos, los autores desarrollaron un proceso ETL (Extracción, Transformación y Carga) en Python y SQL estructurado en cuatro fases: extracción de los archivos CSV, validación y limpieza (descartando registros con campos vacíos o coordenadas inconsistentes), carga a tablas temporales para poblar dimensiones, y consolidación final en las tablas de hechos del almacén[cite: 25].

## 

**3. Cómo se modeló la información: qué entidades o dimensiones se identificaron, qué hechos se miden y cómo se relacionan**

Para estructurar la información de manera eficiente, el sistema se diseñó bajo un esquema de estrella en un almacén de datos (*data warehouse*) implementado en PostgreSQL[cite: 25, 28]. En este modelo se identifican los siguientes componentes:

* **Entidades y Dimensiones Principales:**
    * `dim_tiempo`: Representa el componente temporal, abarcando fechas, años y bimestres[cite: 25]. Sus **atributos** incluyen el periodo de lectura y las marcas temporales compartidas con las series climáticas[cite: 25, 28].
    * `dim_ubicacion`: Representa la dimensión espacial y territorial[cite: 25]. Sus **atributos** principales son la alcaldía, la colonia, así como las coordenadas de latitud y longitud[cite: 25].
    * `dim_indice_des`: Contiene los niveles del índice de desarrollo urbano[cite: 25]. Sus **atributos** abarcan los cuatro niveles ordinales publicados oficialmente (*ALTO, MEDIO, BAJO y POPULAR*)[cite: 25, 26].
* **Hechos que se miden:** Se estructuran a través de dos tablas de hechos principales: `fact_consumo_agua` (con un grano equivalente a una manzana o bloque urbano por periodo de facturación, consolidando 70,886 registros limpios) y `fact_clima` (con registros meteorológicos diarios)[cite: 22, 25, 26, 28]. Las métricas cuantificadas incluyen el consumo total de agua, consumos promedio y variables climáticas asociadas[cite: 25, 28].
* **Relaciones:** Las tablas de hechos se vinculan mediante claves con las dimensiones conormadas (`dim_tiempo`, `dim_ubicacion` y `dim_indice_des`)[cite: 25]. Adicionalmente, el esquema relacional se proyecta de manera declarativa mediante mapeos R2RML hacia un grafo de conocimiento RDF (*RDF Data Cube*), donde las observaciones se conectan mediante propiedades geométricas y de vecindad espacial (como el cálculo de proximidad entre centroides urbanos)[cite: 22, 29, 30].

## 

**4. Qué preguntas concretas puede responder el sistema resultante**

Gracias a la integración del almacén dimensional, las consultas parametrizadas y la interfaz geoespacial interactiva, el sistema permite responder a diversas interrogantes prácticas, tales como:

* ¿Cuáles son las alcaldías y colonias que registran los mayores volúmenes de consumo total y promedio de agua en la Ciudad de México[cite: 22, 27, 32]?
* ¿Cómo varía el consumo de agua a lo largo de los bimestres disponibles en el repositorio analítico[cite: 22, 27]?
* ¿Qué zonas o manzanas específicas presentan patrones de consumo atípico en comparación con el resto de las colonias de su misma alcaldía, sirviendo como filtro exploratorio para revisiones prioritarias[cite: 22, 27, 28, 29]?
* ¿Qué zonas vecinas o adyacentes a una ubicación seleccionada comparten características de consumo hídrico mediante la navegación directa sobre el grafo de conocimiento territorial[cite: 22, 27, 30, 31]?

## 

**5. Qué limitaciones reconocen los autores y qué trabajo futuro proponen**

* **Limitaciones:** Los autores reconocen que la cobertura temporal está acotada al primer semestre de 2019 publicado originalmente por la fuente, por lo que la variación estacional se restringe a una comparación intra-semestral[cite: 26, 32]. Asimismo, señalan que el módulo de detección de anomalías opera de manera exploratoria con perturbaciones sintéticas (sin datos reales etiquetados de fugas), que las vecindades se representan mediante centroides geográficos en lugar de polígonos exactos, y que la asociación con el índice de desarrollo es puramente descriptiva[cite: 28, 29, 32].
* **Trabajo futuro:** Proponen materializar el grafo de conocimiento en un almacén de tripletes persistente con un punto de acceso SPARQL público, sustituir la proximidad por centroides utilizando polígonos oficiales de vecindades para refinar las relaciones topológicas, alinear los identificadores territoriales con otras fuentes externas para mejorar la interoperabilidad y transferir la metodología ETL a otros dominios de datos urbanos abiertos como movilidad o calidad del aire[cite: 32].

## 

**Bibliografía**

* Velázquez Arrieta, E. U., Pulido Morales, O. F., García López, E., Hernández Martínez, C. A., y Hurtado Avilés, G. (en prensa). Territorial Information Retrieval from Heterogeneous Open Data through the Construction of a Data Warehouse for Water Management in Mexico City[cite: 22]. Escuela Superior de Cómputo (ESCOM), Instituto Politécnico Nacional (IPN), Ciudad de México, México[cite: 22].