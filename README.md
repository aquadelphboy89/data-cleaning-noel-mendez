
### 1) Objetivo
- Analizar y visualizar un dataset de demostración para entender el proceso de limpieza de datos, transformación (construcción de caracteristicas) y análisis exploratorio (EDA) de datos usando Python y Pandas.

### 2) Dataset
- Fuente: El CSV data_act_01.csv recoge los crimenes reportados en San Francisco en el periodo de una semana (entre 30 de marzo del 2016 y 5 de abril del 2016)
- Nº filas/columnas: 10051 filas y 12 columnas
- Variables clave: 
 CrimeId                Entero                               Identificador del crimen
 OriginalCrimeTypeName  String                               Tipo de delito reportado
 OffenseDate            DateTime (original string)           Fecha del delito
 CallTime               String                               Hora que se reportó el delito
 CallDateTime           DateTime (original string)           Fecha que se reportó el delito
 Disposition            String                               Resolución del delito
 Address                String                               Dirección del delito
 City                   String                               Ciudad del delito  
 State                  String                               Estado del delito 
 AgencyId               String                               Identificador de la agencia
 Range                  Float                                Rango de dirección
 AddressType            String                               Tipo de ubicación (intersección, edificio, etc.)

### 3) Preguntas
Este dataset presentan muchas preguntas. Algunas de ellas podrían ser:
- ¿Cuáles son los tipos de crimen más frecuentes?
- ¿En qué horas del día ocurren más incidentes?
- ¿Qué disposiciones policiales son más comunes (REP, GOA, etc.)?
- ¿Qué zonas/direcciones concentran más delitos?
- ¿Hay diferencias entre tipos de dirección (Premise vs Intersection)?
- ¿Cómo varía el crimen por fecha o día?
- ¿Qué porcentaje de incidentes queda sin resolver?
- ¿Qué tipos de delitos ocurren más en intersecciones vs edificios?
- ¿Existen patrones temporales entre tipos de delitos?

### 4) Data issues & fixes
- Valores faltantes → Limpieza y imputación en "JupyterNotebook/data_cleaning.ipynb"
- Datos inconsistentes → Limpieza y imputación en "JupyterNotebook/data_cleaning.ipynb"
- Formatos incorrectos → Limpieza y imputación en "JupyterNotebook/data_cleaning.ipynb"

### 5) Pipeline
- raw → clean → features → export a "Data/Cleaned/"

### 6) Hallazgos

- Insight 1: Defecto sistémico en la hora del incidente (OffenseTime).
Se identificó un sesgo crítico en la captura de datos: todos los registros marcan las 00:00 como la hora en que ocurrió el delito. Este valor no representa la realidad, lo cual provoca que invalide cualquier análisis basado en el "momento del crimen".

- Insight 2: Inconsistencia técnica en el ReportingDelay.
Como consecuencia directa del punto anterior, la variable de retraso en el reporte (ReportingDelay) pierde su valor analítico. Al calcularse como la diferencia entre la hora de la llamada (CallTime) y una hora de incidente ficticia (00:00), el resultado es simplemente una traslación de la hora de la llamada a segundos. Por tanto, el dataset no permite medir la eficiencia en el reporte ciudadano, sino únicamente el flujo de llamadas recibidas.

- Insight 3: Sesgo por ventana temporal reducida y falta de representatividad.
El análisis está limitado a una única semana (del 30 de marzo al 5 de abril de 2016). Esta muestra tan pequeña genera anomalías estadísticas, como la ausencia casi total de registros los miércoles. Este dato no implica que no ocurran delitos ese día en San Francisco, sino que evidencia una falta de datos por el corto alcance del tiempo analizado, lo que impide extraer conclusiones sobre estacionalidad o patrones semanales reales.

- Insight 4: Predominancia de la resolución directa en el lugar.
A pesar de las limitaciones técnicas, el EDA muestra una tendencia clara en la operativa policial: la mayoría de los incidentes se resuelven mediante la gestión directa del oficial (HAN) o citaciones (CIT), ocurriendo principalmente en domicilios (Premise Address) e intersecciones. Esto sugiere que el grueso de la actividad policial registrada corresponde a intervenciones de proximidad y resolución inmediata.

### 7) Estructura del proyecto
- "JupyterNotebook/data_cleaning.ipynb" contiene todo el proceso de limpieza de datos, incluyendo valores faltantes, filas duplicadas, datos incosistentes, formatos incorrectos, creación de nuevas variables para un estudio más exhaustivo, etc
- "JupyterNotebook/eda.ipynb" contiene todo el proceso del EDA con el dataset ya limpio. De esta manera respondemos a diferentes preguntas que salen de este dataset.

### 8) Cómo ejecutar
- `pip install -r requirements.txt`
- Abrir y ejecutar todas las celdas de "JupyterNotebook/data_cleaning.ipynb"
- Abrir y ejecutar todas las celdad de: "JupyterNotebook/eda.ipynb"
