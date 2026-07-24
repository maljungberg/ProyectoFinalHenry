

<div align="center">
    <img src="https://i.postimg.cc/Xqr82M3R/default.png" alt="logo">
  <h1>Data Engineering</h1>
</div>




Esta documentación tiene como objetivo presentar y explicar el proceso de Data Engineering realizado por el equipo. La ingeniería de los datos consistió en una serie de pasos que permitió obtener, transformar y almacenar datos para los análisis posteriores. Este proceso es esencial para garantizar la calidad y disponibilidad de los datos necesarios para el análisis y la toma de decisiones. A continuación, se describirán las etapas y su ejecución.<br><br>



## I. Recopilación de requisitos: 
A partir de una reunión preliminar, se definieron y documentaron los requisitos del proyecto en colaboración con el product owner. Se determinaron los objetivos comerciales, y el equipo definió las fuentes de datos requeridas, los tipos de datos necesarios, el stack tecnológico y cualquier consideración especial, y se planificaron las tareas y duración de las mismas. 

Todo el proceso I se documentó oportunamente, se presentó la propuesta del proyecto nuevamente con el PO durante el primer sprint, y la misma fue aprobada.<br> 

Los pasos siguientes fueron:<br><br> 



## II. Análisis exploratorio: 
Se obtuvieron resultados positivos luego de un análisis exhaustivo de calidad realizado sobre los datasets a utilizar. El objetivo del análisis fue evaluar la completitud, consistencia, precisión y otros aspectos clave de los datos, con el fin de identificar posibles problemas y proponer soluciones para mejorar la calidad de los mismos. El análisis reveló calidad y confiabilidad suficiente para avanzar a la etapa siguiente.<br>  



## III. Definición del flujo de la extracción y carga / definición del tipo de almacenamiento: 
Para los fines del presente trabajo, se optó por un flujo de tipo Extracción-Transformación-Carga,  ya que se trabajaría principalmente con datos estáticos, provenientes de fuentes definidas, y serían únicamente datos estructurados. Al tratarse de datos de gran volúmen, se decidió darles tratamiento y demás transformaciones antes de la carga, para eliminar todo aquello que no fuese de utilidad y optimizar los recursos. Por otra parte, a partir del análisis exploratorio inicial, se determinó que los datos no iban a requerir transformaciones complejas, por lo que resultó viable realizarlas antes de la carga. En relación al tipo de almacenamiento, se decidió la creación de un datawarehouse para alojar los datos que usaríamos en nuestro análisis, habiendo evaluado que no contábamos con datos desestructurados o semiestructurados, que no habría modificaciones significativas en la velocidad del flujo de carga de los datos, y que sería el diseño adecuado para cargar los datos ya transformados, como se detalló anteriormente.<br>


## IV. Extracción: 
Se procedió a recopilar los datos de las fuentes definidas durante la etapa de requisitos. Se seleccionaron las herramientas y técnicas adecuadas para extraer los datos de las fuentes, que fueron archivos CSV, parquet y datos obtenidos desde una API. Para la extracción de los datos de la API se diseñó un código de Python que obtuviese la temperatura máxima, media y mínima diaria de la ciudad de Nueva York, desde 2013 hasta 2023. Estos datos son luego ingresados en un Dataframe de Pandas y luego parseados a un archivo CSV para su posterior consumo. Luego, mediante la implementación de Airflow, se generó un código que permite correr el script de manera diaria para la actualización de los datos, logrando la completa automatización del proceso.<br>


## V. Transformación de Datos: 
Esta etapa implicó la limpieza de datos, el filtrado, la normalización, discretización y cualquier otra manipulación necesaria para cumplir con los requisitos establecidos. Se leyeron los datos a través de Pandas, primero descargando los datos para disponerlos on premise; en el caso de los datos del set 'TLC Trip Record Data', se accedieron directamente desde la web. Se eliminaron las columnas que no serían utilizadas. Se encontraron registros con datos nulos, al contabilizarlos y resultar un cantidad pequeña, se determinó que la eliminación de esos registros no tendría un impacto significativo. Con el mismo criterio fueron eliminados los campos que presentaban outliers. Se crearon las columnas necesarias para los análisis propuestos. 
En estas etapas se utilizó Python como lenguaje en conjunto con la librería Pandas para los análisis exploratorios y las transformaciones, y Mysql como lenguaje para la creación de las bases de datos a utilizar y para efectuar las queries necesarias.<br> 


## VI. Integración: 
Creación del modelo relacional: A partir de los datos extraídos, se realizó el diseño conceptual de los mismos. Se utilizaron herramientas como diagramas de entidad-relación (DER) para representar las entidades, relaciones y atributos. Se establecieron las primary and foreign keys, así como las restricciones de integridad referencial. Se determinó ejecutar la normalización de los datos en los casos que fuese requerido, para eliminar redundancias y garantizar la integridad de los datos. Se utilizan las formas normales (1NF, 2NF, 3NF, etc.) para descomponer las tablas en entidades más pequeñas y definidas.<br> 
 
Luego se procedió a crear el diseño lógico del modelo relacional. Se definieron las tablas y sus columnas, se asignaron los tipos de datos y se establecieron las relaciones y restricciones. Las tablas de las bases de datos definidas para los fines específicos del análisis fueron creadas en Workbench en conexión con un servidor Mysql en la nube. Para esta instancia, el equipo optó por las soluciones brindadas por Azure.<br>


`<Diagrama de flujo de trabajo>` : <https://github.com/Rowinelle/ProyectoFinalHenry/blob/rp_DEng/images/Pipeline%20ETL.png>

# Fundamentación de los datos: 
- TLC Trip Record Data: datos provenientes del gobierno de la ciudad de Nueva York en su subdirección de Comisión de Taxis y Limosinas (TLC) desde el 2015 al 2023. 
- Urban Gis and Charging Station Data: los datos generados se utilizan para la generación del modelo de Machine Learning, misma base de datos fue utilizada para el desarrollo de un modelo de predicción de popularidad en Predicting Popularity of Electric Vehicle Charging Infrastructure in Urban Context de Straka en 2020. Los datos están disponibles en IEEE Data Port que es el sitio de bases de datos asociado a la Institución de Ingenieros Eléctricos y Electrónicos ( IEEE), una organización que reúne información técnica profesional de libre acceso en la Web.
- Percentage_EV_per_year: Esta tabla fue creada con base en la información disponible de la venta de vehículos eléctricos (considerando también híbridos) a nivel mundial disponible en Electric Vehicles standards, charging infrastructure, and impact on grid integration: A technological review de Das en 2019.
- EV: Datos ElectricCarData_nom.csv de la carpeta de bases de datos disponibles proporcionadas por el instructor.
- ICEV: Base de datos de Kaggle que especifica modelos de autos, marca y año con su consumo de gasolina en ciudad y en autopista en galones por kilómetro. Kaggle es una comunidad virtual que agrupa recursos enfocados en ciencia de datos para la generación de proyectos.
- Fuel_cost: Datos recopilados de U.S. Energy Information Administration desde 05 de abril de 1993, también referida a ella como DIA es la agencia de estadística del Departamento de Energía de los Estados Unidos, que provee información para pronósticos, análisis y promoción de políticas públicas asociadas a la demanda energética nacional. 
- Electricity_cost: Datos recopilados de la EIA en su apartado de Electricity Data. 
- Emission_vehicles: Es una tabla que mantiene la proporción de emisión de CO2 en kg/km recorrido de autos eléctricos y de combustión. Los datos puestos en esta tabla provienen del informe realizado por Polestar y Rivian en su Pathway Report que congrega información de la emisión de CO2 a futuro y la comparación con la electrificación de los medios de transporte. 
- Open-meteo: Se optó por los datos brindados por la API de la plataforma open-source de Open-meteo para la recopilación de la temperatura máxima, media y mínima diaria de la ciudad de Nueva York.<br><br>



#  Modelo Entidad Relación: 
[![Modelo-ER-fondo-transparente.png](https://i.postimg.cc/tJJ1gQ9S/Modelo-ER-fondo-transparente.png)](https://postimg.cc/2LpjHtbh)


`<Diagrama Entidad Relación (datos y columnas)>` : <https://github.com/Rowinelle/ProyectoFinalHenry/blob/rp_DEng/images/Diagrama%20Entidad%20Relaci%C3%B3n%20(Tipo%20de%20datos%20y%20columnas).jpg>

#  Diccionario de columnas: 

[![Diccionario-de-columnas.jpg](https://i.postimg.cc/KcnQnH3H/Diccionario-de-columnas.jpg)](https://postimg.cc/143pSMHG)

`<Link al diccionario>` : <https://github.com/Rowinelle/ProyectoFinalHenry/blob/rp_DEng/images/Diccionario%20de%20columnas.jpg>

