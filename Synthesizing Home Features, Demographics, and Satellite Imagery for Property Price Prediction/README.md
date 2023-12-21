**Summary**

Home buyers or investors consider not just the features of a home, but also other factors related to the location of the home to make a purchase decision. My model is an attempt to build a price estimator model that is trained with home features, demographics, and features from the satellite imagery of the home.

**Project Scope:**

For this estimation model, I focused specifically on the Philadelphia metro area, leveraging my familiarity with the region. The model's boundary was defined within a 25-mile radius around Philadelphia, encapsulating the diverse real estate landscape within this area. To streamline the analysis and ensure dataset consistency, I opted to include only single-family homes.


**Data Flow Chart:**


![image](https://github.com/Sharanjv/Data-Science-Projects/assets/17241845/f50c9d90-e0cf-4717-8d29-5cb64455d19c)


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

![image](https://github.com/Sharanjv/Data-Science-Projects/assets/17241845/90efef9d-c673-4313-b6cb-8d79974e0675)


The model returned a r-squared value of 0.835 and the mean absolute error of the sales price was $55,850.
