#  Assessment of the CO2 emission and economic impact of the electrification of private means of transport for the construction of a new transport mode. prediction of popularity 	
###### Acosta, O., Bellardini, J., Castro, R., Ljungberg, M. and Prestupa, R., 2023	 	
### Machine Learning Model

### Object
Generation of the Mexico City map with the most popular predicted points in the city. 

### Dataset

The dataset for the construction of the tree was taken from a reference work carried out by Straka (2020) where information from the Geographic Information System (GIS) was used to generate a prediction model of the popularity associated with the location. of charging stations in the city of Holland in the Netherlands. The details of the algorithm and optimized hyperparameters were not described in the scientific work, however, they were evaluated in the construction of the model for the current project.

### Characteristics of the gradient-powered tree

XGBoost was used to generate the model, evaluating its performance based on 3 characteristics:
* Accuracy: A metric that measures the proportion of correct predictions made by the model compared to the total number of predictions. A value of 0.87 was obtained, notably higher than the objective accuracy described in specific objectives.
* F-Score: Evaluation metric used in classification problems to evaluate the balance between precision and completeness of the model. It is especially useful when there is an imbalance in the target classes, its application is quite useful in the face of model scalability where this described evaluation system can be used to verify the relevance of the model in Mexico City. The score obtained was 0.70, higher than expected in the specific objectives prior to the generation of the model.

A new measurable evaluation parameter was included, the Matthew Correlation Coefficient (MCC):

* MCC: Metric that measures the general quality of the model's classification, taking into account the four possible results of the classification: true positives, true negatives, false positives and false negatives. It provides a more balanced and robust measure to assess the classification ability of the model, especially in cases of class imbalance and noisy data. Responding to the quality of the data coming from a geographic system, the incorporation of this characteristic allows us to verify the robustness of the model. The score obtained was 0.63, marking a pattern of improvement regarding the scalability of the model.

The training and test samples were 80% and 20% of the data, following conventional instructions.

### Map construction 

The points were chosen based on the results of figure 1. For the construction of the map, an open-source mapping system, Open Street Map, was used because it contains information with great detail about the hotels, wholesale businesses, swimming pools, parking, etc. The construction of Mexico City was carried out by verifying the relevant features and their location by means of an analysis of the Open Street Map.

A table with the information of latitude and longitude of the chosen points with some features such as load capacity) and  PowerBi was used to make an interactive map with the points. On the map, the points can be seen according to the load capacity. (Fig 2.)

[![caracteri-sticas-mas-populares.png](https://i.postimg.cc/8CfMvSrQ/caracteri-sticas-mas-populares.png)](https://postimg.cc/mcRPxKw8)

Fig 1. Most relevant features for the location of charging points in Holland. 


[![CDMX.jpg](https://i.postimg.cc/RCRCHvTb/CDMX.jpg)](https://postimg.cc/nMXt8bgv)

Fig 2. Mexico City map with the most popular predicted location for EV Charging Stations. The size points are according to the load capacity for each station. 

### Conclusions

The evaluation parameters were higher than those expected by the XGBoost algorithm. The model seems to have a behavior capable of predicting the characteristics of the location to increase the popularity of charging stations, being able to extrapolate the conclusions to Mexico City.

### Project prospects

A possible improvement in the MCC is considered, hoping to get closer to the value 1, this would generate greater robustness to the project and would be able to prevent failures when using data from other locations in the world. The implementation of GIS data from Mexico City would provide a quite important enrichment capacity to the project, however, due to limitations in space and data management, the current work only incorporates information from the Netherlands, transferring the conclusions of the tree to a map of Mexico City. It is notable to highlight that the implementation of EV and charging stations in Mexico City are crossed by social perception, so that the response to them will not be evaluated.

## Annexes
#### Abbreviations
CO2= Carbon dioxide
EV=Electric vehicles
MCC= Matthew Correlation Coefficient 

