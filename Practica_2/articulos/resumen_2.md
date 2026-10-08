# Resumen del Artículo: A Dimensional Data Warehouse for Geospatial Monitoring of Municipal Public Works, with an Evolution Path Toward a Lakehouse Architecture

1. Qué problema aborda y por qué importa

El crecimiento acelerado de los datos sobre infraestructura pública en los gobiernos municipales genera volúmenes heterogéneos que suelen gestionarse mediante sistemas transaccionales aislados u hojas de cálculo distribuidas, lo que dificulta la trazabilidad histórica, la detección temprana de retrasos y la fiscalización ciudadana[cite: 2]. El problema central que aborda este trabajo es la fragmentación y opacidad en la gestión de las obras públicas municipales (específicamente evaluado en Temascaltepec, Estado de México)[cite: 2]. Esto importa porque la falta de herramientas analíticas integradas impide una supervisión transparente, fomenta la impunidad o ineficiencia administrativa y limita la participación informada de los ciudadanos en la rendición de cuentas gubernamental[cite: 2].

## 2. De dónde provienen los datos, en qué formato estaban y qué tuvo que hacerse para poder usarlos

* **Origen y formato:** Los datos provienen de un escenario sintético sembrado (para proteger la privacidad y evaluar el sistema) que simula la operación real de una administración municipal, estructurando registros de obras públicas, presupuestos, contratos, reportes de supervisión y evidencias multimedia[cite: 2].
* **Procesamiento:** Para su estructuración y uso analítico, los autores desarrollaron generadores en código (scripts en Python con generadores tipo Faker) encargados de poblar de manera consistente las entidades relacionales y transaccionales del sistema[cite: 2]. Asimismo, los elementos multimedia e informes (fotografías y documentos PDF) se organizaron y almacenaron en un repositorio de objetos compatible con S3 (Cloudflare R2) siguiendo una convención de rutas particionadas por año, mes e identificador de obra[cite: 2].

## 3. Cómo se modeló la información: qué entidades o dimensiones se identificaron, qué hechos se miden y cómo se relacionan

Para estructurar la información de manera eficiente, el sistema adoptó un modelo de estrella en un Almacén de Datos (*Data Warehouse*) implementado en PostgreSQL[cite: 2]. En este modelo se identifican claramente los siguientes componentes:

* **Dimensiones (10 en total):** Destacan cinco Dimensiones de Cambios Lentos de Tipo 2 (*Slowly Changing Dimensions Type 2* — SCD 2) que preservan la historia ante modificaciones: `dim_work` (obras), `dim_region` (regiones/comunidades), `dim_company` (contratistas), `dim_staff` (personal) y `dim_budget` (presupuesto)[cite: 2]. Se complementan con tres dimensiones de Tipo 1 y dos de Tipo 0 (catálogos fijos como el tiempo y los tipos de eventos)[cite: 2].
* **Hechos que se miden:** Se estructuran a través de dos tablas de hechos principales[cite: 2]:
    * `fact_audit_events` (grano de un evento de auditoría atómico, particionada por año)[cite: 2].
    * `fact_work_monthly` (instantánea periódica con grano de una obra por mes)[cite: 2]. Las métricas cuantificadas incluyen presupuestos totales, costos acumulados, saldos restantes, porcentajes de avance físico y financiero, número de reportes, días de retraso y desvíos económicos[cite: 2].
* **Relaciones:** Las tablas de hechos se vinculan mediante claves subrogadas con las diez dimensiones del esquema en estrella[cite: 2]. Adicionalmente, el almacenamiento de objetos mantiene un vínculo bidireccional mediante metadatos almacenados en el almacén de datos, asociando las evidencias fotográficas y documentales directamente con sus respectivas obras y periodos de supervisión[cite: 2].

## 4. Qué preguntas concretas puede responder el sistema resultante

Gracias al sistema de visualización interactivo, su almacén dimensional integrado y la API REST, es posible responder a diversas interrogantes prácticas, tales como:

* ¿Cuál es el estado actual, el avance físico y financiero de una obra específica dentro de una comunidad determinada y qué empresa contratista está a cargo[cite: 2]?
* ¿Qué obras registran retrasos significativos en su ejecución cronológica y cuántos días de desfase acumulan respecto a lo planeado[cite: 2]?
* ¿Cuáles son las alertas de auditoría prioritarias clasificadas por categoría (montos elevados, obras canceladas, modificaciones presupuestales o eventos tardíos)[cite: 2]?
* ¿Cómo se distribuyen geográficamente los recursos, los presupuestos ejecutados por fuente de financiamiento y las propuestas de participación ciudadana a lo largo de las distintas regiones del municipio[cite: 2]?

## 5. Qué limitaciones reconocen los autores y qué trabajo futuro proponen

* **Limitaciones:** Los autores reconocen que la arquitectura actual se centra en un esquema clásico de almacén de datos donde el almacenamiento en la nube opera únicamente como repositorio de evidencias binarias sin consultas analíticas directas sobre el lago[cite: 2]. Asimismo, señalan que el control de acceso implementado es ligero (basado en cabeceras y tokens sin expiración robusta para producción), que el despliegue dinámico depende de contenedores locales y que toda la evaluación se realizó sobre conjuntos de datos sintéticos debido a restricciones de privacidad con registros municipales reales[cite: 2].
* **Trabajo futuro:** Proponen evolucionar el almacenamiento hacia una arquitectura de *Lakehouse* abierta utilizando formatos de tablas estandarizados (como Apache Iceberg o Parquet con metadatos transaccionales) consultados directamente mediante motores ligeros (DuckDB o Trino), incorporar un pipeline de visión artificial para clasificar automáticamente el avance de las obras a partir de fotografías, publicar el esquema como un vocabulario OWL en Linked Data compatible con el estándar internacional OC4IDS (*Open Contracting for Infrastructure Data Standard*), implementar votación cuadrática y validar la arquitectura en múltiples municipios[cite: 2].

## Bibliografía

* González Casiano, U., Maldonado Mejía, M. T., y Hurtado Avilés, G. (2026). A Dimensional Data Warehouse for Geospatial Monitoring of Municipal Public Works, with an Evolution Path Toward a Lakehouse Architecture[cite: 2]. Escuela Superior de Cómputo (ESCOM), Instituto Politécnico Nacional (IPN), Ciudad de México, México[cite: 2].# Resumen del Artículo: A Dimensional Data Warehouse for Geospatial Monitoring of Municipal Public Works, with an Evolution Path Toward a Lakehouse Architecture

