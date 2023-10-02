# Did We Really Desegregate?: Predicting School Zones with Demographic Data
## A model to determine how predictive demographic features are of elementary school zones

Charlottesville, Virginia, like every other town in the United States, has a checkered history with race relations and public education. The city school district has sought to remedy historic wrongs by updating its school zones and eliminating maps that were drawn to keep black kids out of historically white schools. This project looks at the current map and investigates the degree to which race still informs assigned school zone. Using census data about race, economic status, education levels, age spread, and details about housing, I was able to build a model that could predict a block's assigned school district with 88.8% accuracy. My model that relied only on racial makeup predicted the correct school only 31.6% of the time, hardly better than a dummy model.
 
![swings](images/aaron-burden-ob6O_xd67O0-unsplash.jpg)
Photo by <a href="https://unsplash.com/@aaronburden?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Aaron Burden</a> on <a href="https://unsplash.com/photos/ob6O_xd67O0?utm_source=unsplash&utm_medium=referral&utm_content=creditCopyText">Unsplash</a>
 
GitHub Repository: https://github.com/LydiaCuffman/cville_school_zones

Presentation: Link


## Business Understanding and Data Understanding
Charlottesville City Schools integrated under duress. Initially the superintendent closed the schools rather than integrate them. While the schools did eventually reopen and ostensibly integrated, what followed were decades of less overt segregation. <a href="https://www.nytimes.com/2018/10/16/us/charlottesville-riots-black-students-schools.html">The New York Times</a> reported on this history of discrimination against black students in a 2018 article. One illustrative example is Venable Elementary School, the school closest to the University of Virginia and the school cited in the article as having the highest test scores in the division. Students in a predominantly black neighborhood a half mile from the school were zoned for a school three miles away. That racist choice was only fully rectified in 2022, when the school board voted to adjust the school zoning map. The school division also issued an apology to community members for <a href="https://www.cvilletomorrow.org/after-half-a-century-bussing-kids-from-a-historically-black-public-housing-community-away-from-their-neighborhood-school-city-schools-votes-to-rezone-venable/">"historic and recent mistreatment."</a>

This project seeks to determine how equitable the new zoning map is. Now that an obviously racially motivated choice has been fixed, to what degree does the racial makeup of a neighborhood predict the elementary school its students are assigned to?

I used data from opendata.charlottesville.org as well as data collected by the Virginia Equity Center. Both data sets pull from the United States Census, but I found them easier to use than the direct Census Bureau portal. The Census breaks its data down on a variety of scales, with the smallest being Block. I overlaid the Charlottesville City Schools elementary school zone map with the Census blocks to build my data set. My racial data was at the Block level and my other demographic details were at the Block Group (one level up) level. My non-racial demographic data was largely focused on economic status, including features like median household income, percentage of population with health insurance, households receiving public health insurance and/or SNAP benefits, home-ownership rates, and the number of cost-burdened renters. Additionally I included the age breakdown of each Block Group along with details about number of housing units and how many of those units are vacant. 

![school zones](images/school_zones)

## Modeling and Evaluation

I began with two dummy models. A model that randomly predicts one of the six elementary schools each time would be accurate 17.3% of the time. A model that always predicts the school that covers the most census blocks would be right 32.1% of the time.

After cleaning my data and running it through a process of principal component analysis (PCA) to address issues of multicollinearity, I tried both a logistic regression, a decision tree, and a random forest. After running a grid search to avoid overfitting, my random forest model performed the best, and it ultimately resulted in an accuracy score of 88.8% on testing data. The top ten feature importances for this model were all non-racial features, so it appears that demographics are very predictive of school zone, but race alone may not be. My next model tested this hypothesis.

I removed all features that were not describing the racial makeup of the block and tried the same models. Again, the random forest with grid searched hyperparameters was the best model, but even it only predicted correctly 31.6% of the time on testing data.

Socioeconomic factors are often blamed in conversations about educational equity, so I was curious to see what happened if I constructed a similar model but with only the non-racial demographic data. That model performed almost as well as overall model, accurately predicting school zone in 85.7% of the testing data.

It appears that you cannot say much about school zone based solely on race, but other demographic factors can be quite predictive.

![school_zone_predictions](data/school_zone_predictions)

## Conclusion
This model does not serve an immediately practical purpose, and it was never intended to. If someone wants to know their school district, the city schools division offers an address lookup tool that is always right.

Instead, this model is intended to spark continued conversation. It appears that the school district has largely succeeded in drawing a map that is no longer explicitly racist. The map does still reflect a city dramatically divided by economic factors. These are not issues likely to be solved by redrawing the map, as they reflect the geography of housing in the city. If truly heterogenous schools were the ultimate goal, then students would have to travel all over town at random rather than attending their closest school. In addition to being a logistical nightmare, such a solution would surely be intolerable to the community.

The takeaway from this project is that the school map is no longer the place to direct our efforts towards increasing equity. School zoning was merely the first line of attack in efforts to tacitly keep schools segregated. While this project suggests that particular obstacle has been removed, the NYTimes article outlines many other areas of persistent discrimination, including access to advanced courses, gifted education, and a two-tiered diploma system. The public school system is no longer assigning students to schools in a directly racist way, but there's plenty of work still to be done.

## Repository Navigation

├── data
├── images
├── .gitignore
├── LICENSE
├── README.md
├── [notebook](notebook.ipynb)
└── [presentation](presentation.pdf)