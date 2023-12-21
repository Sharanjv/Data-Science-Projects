**Summary**

Home buyers or investors consider not just the features of a home, but also other factors related to the location of the home to make a purchase decision. My model is an attempt to build a price estimator model that is trained with home features, demographics, and features from the satellite imagery of the home.

**Problem Statement**

Making informed decisions in real estate involves considering various elements beyond inherent property features. Prospective home buyers and investors face the challenge of evaluating not just the physical attributes of a house but also contextual factors such as socio-demographic environments, quality of school districts, proximity to recreational and commercial hubs, among other location-based considerations. This project aims to develop a comprehensive price estimation model that synthesizes Demographics and Satellite Imagery alongside home-specific features. By amalgamating these diverse data sources, the goal is to empower home buyers and investors with an advanced price estimator. This tool will provide a holistic view, enabling more informed and accurate estimations for potential properties under consideration, facilitating more confident and prudent decision-making in real estate transactions.

**Project Scope:**

For this estimation model, I focused specifically on the Philadelphia metro area, leveraging my familiarity with the region. The model's boundary was defined within a 25-mile radius around Philadelphia, encapsulating the diverse real estate landscape within this area. To streamline the analysis and ensure dataset consistency, I opted to include only single-family homes. 

**Home Features Dataset:**

The acquisition of home features data involved leveraging the Realty Mole API through a series of API calls. Following an initial exploratory analysis, these selected home features were used to train my model: square footage, bedrooms, bathrooms, zip code, latitude, longitude, year built, and last sale date.

**Demographics Dataset:**

The demographic data was sourced from the American Community Survey Data available on census.gov, gathered specifically at the census tract level. These tracts are structured to maintain homogeneity concerning population characteristics, economic status, and living conditions. After assessing their correlation with sale prices, the chosen variables integrated into the model include median household income, median value of owner-occupied units, percentage of employed population, percentage of minority population, and median age.

![image](https://github.com/Sharanjv/Data-Science-Projects/assets/17241845/39ad9523-472d-43ca-a733-f9167bf54f55)


**Satellite Imagery:**

The satellite imagery for the homes within the dataset was obtained using the Mapbox Static Images API. This API enables the retrieval of satellite imagery based on latitude and longitude inputs. Notably, this API offers images at various zoom levels, providing diverse perspectives of the surroundings. At closer zoom levels, the satellite images show detailed characteristics of the immediate vicinity surrounding a home. Conversely, at lower zoom levels, the satellite images offer a broader perspective, portraying general neighborhood characteristics and attributes. I used two zoom levels for each home in my dataset to train the model.

**Pre-Trained Convolutional Neural Network Model:**

Following the data ingestion procedures, I employed the VGG16 pre-trained deep convolutional neural network to extract features from satellite imagery. Each image yielded an extensive feature set, comprising over 25,000 distinct features. To manage the high dimensionality, a Principal Component Analysis (PCA) transformer was utilized to effectively reduce the feature matrix's dimensions while retaining essential information.

**Ridge Linear Regressor:**

The resulting normalized and reduced feature matrix was merged with the home features and demographic variables dataset. This combined dataset served as the input for a Ridge regressor, leveraging a grid search approach to optimize the PCA components and Ridge alpha parameters. This fine-tuning process aimed to enhance the performance of the linear model.

**Random Forest Regressor:**

Subsequently, the residuals from the linear regressor were utilized to train a Random Forest Regressor. This secondary model served to capture and interpret any non-linear patterns inherent in the data that the linear model might have overlooked.

**Results:** 

The model returned a r-squared value of 0.835 and the mean absolute error of the sales price was $55,850.
