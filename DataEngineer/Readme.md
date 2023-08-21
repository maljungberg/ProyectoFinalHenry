#  Assessment of the CO2 emission and economic impact of the electrification of private means of transport for the construction of a new transport mode. prediction of popularity 	
###### Acosta, O., Bellardini, J., Castro, R., Ljungberg, M. and Prestupa, R., 2023	 

### Objective
This documentation aims to present and explain the Data Engineering process carried out by the team. Data engineering consisted of a series of steps that obtained, transformed, and stored data for subsequent analysis. This process is essential to guarantee the quality and availability of the data necessary for analysis and decision making. Next, the stages and their execution will be described.<br><br>

## I. Compilation of requirements:
Starting from a preliminary meeting, the project requirements were defined and documented in collaboration with the product owner (PO). Business objectives were determined, and the team defined the required data sources, required data types, technology stack, and any special considerations, and the tasks and duration of the tasks were planned.

The entire process I was timely documented, the project proposal was presented again with the PO during the first sprint, and it was approved.<br>

## II. Exploratory analysis:
Positive results were obtained after an exhaustive quality analysis carried out on the datasets to be used. The objective of the analysis was to evaluate the completeness, consistency, precision and other key aspects of the data, in order to identify possible problems and propose solutions to improve their quality. The analysis revealed sufficient quality and reliability to advance to the next stage.<br>


## III. Definition of the extraction and loading flow / definition of the type of storage:
For the purposes of this work, an Extraction-Transformation-Load type flow was chosen, since it would mainly work with static data, coming from defined sources, and would only be structured data. As it is a large volume of data, it was decided to treat it and other transformations before loading it, in order to eliminate anything that was not useful and optimize resources. On the other hand, from the initial exploratory analysis, it was determined that the data would not require complex transformations, so it was feasible to perform them before loading. Regarding the type of storage, it was decided to create a data warehouse to house the data that we would use in our analysis, having evaluated that we did not have unstructured or semi-structured data, that there would be no significant changes in the speed of the data load flow. , and that it would be the appropriate layout to load the already transformed data, as detailed above.<br>

## IV. Extraction:
We proceeded to collect the data from the sources defined during the requirements stage. The appropriate tools and techniques were selected to extract the data from the sources, which were CSV files, parquet and data obtained from an API. To extract the data from the API, a Python code was designed to obtain the daily maximum, average and minimum temperatures of New York City, from 2013 to 2023. These data are then entered into a Pandas Dataframe and then parsed. to a CSV file for later consumption. Then, through the implementation of Airflow, a code was generated that allows the script to be run daily to update the data, achieving complete automation of the process.<br>


## V. Data Transformation:
This stage involved data cleaning, filtering, normalization, discretization, and any other manipulation necessary to meet the established requirements. The data was read through Pandas, first downloading the data to make it available on premise; in the case of the data from the 'TLC Trip Record Data' set, they were accessed directly from the web. Columns that would not be used were removed. Records with null data were found, when counting them and resulting in a small amount, it was determined that the deletion of those records would not have a significant impact. With the same criteria, the fields that presented outliers were eliminated. The necessary columns for the proposed analyzes were created.
In these stages, Python was used as the language in conjunction with the Pandas library for exploratory analyzes and transformations, and Mysql as the language for creating the databases to be used and for carrying out the necessary queries.<br>

##  VI. Integration:
Creation of the relational model: From the extracted data, the conceptual design of the same was carried out. Tools such as entity-relationship diagrams (DER) were used to represent the entities, relationships and attributes. The primary and foreign keys were established, as well as the referential integrity constraints. It was determined to execute the normalization of the data in the cases that were required, to eliminate redundancies and guarantee the integrity of the data. Normal forms (1NF, 2NF, 3NF, etc.) are used to decompose tables into smaller, more defined entities.<br>
 
Then we proceeded to create the logical design of the relational model. The tables and their columns were defined, the data types were assigned, and the relationships and restrictions were established. The tables of the databases defined for the specific purposes of the analysis were created in Workbench in connection with a Mysql server in the cloud. For this instance, the team opted for solutions provided by Azure.<br>

# ETL Summary 
[![ETL-summary.jpg](https://i.postimg.cc/SK0gqFHm/ETL-summary.jpg)](https://postimg.cc/LJTtB7HW)

# ETL in detail
<img src='/images/Pipeline ETL.png'>

# Justification of the data:

- Electricity_cost: Data compiled from the EIA in its Electricity Data section.
- Emission_vehicles: It is a table that maintains the proportion of CO2 emissions in kg/km traveled by electric and combustion vehicles. The data included in this table comes from the report carried out by Polestar and Rivian in their Pathway Report, which gathers information on future CO2 emissions and the comparison with the electrification of means of transport.
- EV: Data ElectricCarData_nom.csv from the available databases folder provided by the instructor.
- Fuel_cost: Data collected from U.S. Energy Information Administration since April 5, 1993, also referred to as EIA, is the statistical agency of the United States Department of Energy, which provides information for forecasts, analysis and promotion of public policies associated with national energy demand.
- ICEV: Kaggle database that specifies car models, make and year with their gasoline consumption in the city and on the highway in gallons per kilometer. Kaggle is a virtual community that brings together resources focused on data science for the generation of projects.
- Open-meteo: The data provided by the API of the Open-meteo open-source platform was chosen for the collection of the maximum, average and minimum daily temperatures of New York City.<br><br>
- Percentage_EV_per_year: This table was created based on the available information on the sale of electric vehicles (also considering hybrids) worldwide available in Electric Vehicles standards, charging infrastructure, and impact on grid integration: A technological review by Das in 2019.
- TLC Trip Record Data: data from the New York City government at its Taxi and Limousine Commission (TLC) branch from 2015 to 2023.
- Urban Gis and Charging Station Data: the data generated is used for the generation of the Machine Learning model, the same database was used for the development of a popularity prediction model in Predicting Popularity of Electric Vehicle Charging Infrastructure in Urban Context of Straka in 2020. The data is available at the IEEE Data Port, which is the database site associated with the Institution of Electrical and Electronics Engineers (IEEE), an organization that gathers freely accessible professional technical information on the Web.

Also information from National Institute of Statistics and Geography (INEGI, for the letters in spanish) was used for the population in Mexico City and the webpage Electromaps where the number of charging points and location of them was displayed. 



# Entity Relationship Model
[![ER-Diagram.png](https://i.postimg.cc/ZRXqCnc9/ER-Diagram.png)](https://postimg.cc/0Mdv48hx)

# Entity Relationship Diagram and Dicctionary of Columns
[![ER-Model-Dic-of-columns.png](https://i.postimg.cc/xTxZwZ0d/ER-Model-Dic-of-columns.png)](https://postimg.cc/fJd5XBS4)


## Annexes
#### Abbreviations
AEV: All-electric vehicles
API: Application Programming Interface
BEV: battery electric vehicles 	
CO2: Carbon Dioxide
DER: Entity-Relationships Diagrams
EIA: Energy Information Administration
IEEE: Institution of Electrical and Electronic Engineers
INEGI: National Institute of Statistics and Geography of Mexico
PO: Product Owner
TLC: Taxis and Limousine Commission


