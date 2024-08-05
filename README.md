# Nearest Object Classification
Team members:
- Sullivan Crouse

## Overview and External Knowledge
This repository contains the complete analysis of the [Nearest Earth Object Dataset](https://www.kaggle.com/datasets/ivansher/nasa-nearest-earth-objects-1910-2024?resource=download). This dataset contains information about Nearest Earth Objects (N.E.O.) which are "comets and astroids that...enter the Earth's neighborhood" ([NASA](https://cneos.jpl.nasa.gov/about/basics.html#:~:text=Near%2DEarth%20Objects%20(NEOs),to%20enter%20the%20Earth's%20neighborhood.)). NASA also classifies N.E.O.s as being "[1.3 astronomical units of the sun](https://www.jpl.nasa.gov/keeping-an-eye-on-space-rocks)". They state that a relatively small number of N.E.O.s are close enough or large enough in size to be closely monitored. The importance of this is, as stated by NASA, is "**knowing the size, shape, mass, composition and structure of these objects helps determine the best way to divert one, should it have an Earth-threatening path.**" These monitored objects are labeled as hazardous in the dataset.

A cool visualization into this from [theskylive.com](https://theskylive.com/near-earth-objects) which has a neat page containging information o fupcoming close approaches as well as a 3d visualization of where the orbits of these objects are in space. One important take away from this is that the names of the space object has a year in it, but it is not hte year of closest approach. Instead it appears to be the year it was discovered.  

## Data and Research Question
The dataset for this problem has the following features (descriptions directly from Kaggle):
- neo_id: unique id for each asteroid
- name: name given by NASA
- absolute_magnitude: describes intrinsic luminosity
- estimated_diameter_min: minimum estimated diameter in kilometres
- estimated_diameter_max: maximum estimated diameter in kilometres
- orbitining_body: planet that the asteroid orbits
- relative_velocity: velocity relative to Earth Kmph
- miss_distance: distance in Kilometres missed
- is_hazardous: Boolean feature that shows whether asteroid is harmful or not


Given that these hazardous N.E.O.s are classified and labeled by NASA, there is not much use for us to try to create a predictive model. Rather a prescriptive model would be a better usecase to help us determine what factors contribute greatly when NASA classifies an object as hazardous. The first thought that comes to mind with this is using a statistical model like Logistic Regression and evaluating the parameters of the model to help identify key components in what makes an object hazardous. We could also do some clustering on the data as well to gleem some more insights. Therefore, the research question for this project is "**what are the key features that make a N.E.O. be classified as hazardous**".

## EDA and Data Prep
EDA and Data Preperation have been done in the notebook already. Some key insights from it are that absolute_magnitude and the natural log of estimated_diameter are 1 to 1 correlated, which means we should remove these features. I also transformed the velocity by taking the square root of it to make it more normalized. The discovered year was extracted from the "name" feature. Additonal data prep that is needed will be to standardize continuous normal features and bin weirdly distributed features like discovery year. 

## Modeling and Tuning
Steps for modeling in this project were first to build a logistic regression model to get an interpretation of the data. An overview of the findings from this methodology (particularly the regression table) was:
- const: on the whole we are more likely to classify a NEO as non hazardous
- absolute magnitude: as the absolute maginitude increases, the likelihood of a NEO being hazardous decreases. This makes sense as this is inverse with e raised to estimated diameter, or the size. So as a the size increases, the likelihood of of a NEO being hazardous increases
- relative velocity: as the relative velocity increases, the likelihood of a NEO being hazardous increases.
- miss_distance: as the miss distance increases, the likelihood of a NEO being hazardous decreases.

After the logisitc regression model did perform super well for preditive power, other models were tested and evaluated primarly on F1 score (since our data set is massively unbalanced). Of the tested models, a Random Forest model was found to be the best default classifier. Parameter and [decision threshold tuning](https://scikit-learn.org/stable/modules/classification_threshold.html) were then performed to optimize the model a little bit more. The results of this final model were:
- Accuracy of 93.48%
- Precision of 72.48%
- Recall of 78.79%
- F1 score of 75.50%

More details on the methodology and findings from the modeling and tuning sections of the project can be found in the ipython notebook in markdown cells.  
