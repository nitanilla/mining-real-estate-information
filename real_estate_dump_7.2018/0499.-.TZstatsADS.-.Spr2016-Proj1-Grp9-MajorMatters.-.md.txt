# Project 1: Major Matters

by Group 9 
Eric Ho, Husam Abdul-Kafi, Jingying Zhou, Yuhan Sun, Ziyue (Zac) Wu

### Research Questions
####To what extent does one's major determine his/her career?
#####To stay or to betray? That is a (serious) question.  

* Do people work in fields different from their college majors? How does this tendency vary across majors?  
Do certain fields favor certain majors? 
* Let's say, how many computer scientists have Bachelor’s Degrees in CS? <br /> *Income?*



### Preprocess Datasets

1. To account for survey weights, each observation is replicated the number of times specified in the **PWGTP** column. The expanded dataset is in the file totaldat.expanded.RDS.


2. Occupations Categories
 * Data: **OCCP** column (Occupation Code)
 * Categories assigned according to the code list released by the U.S. Census Bureau
 * 16 categories in total 


	Management Occupations               | Business and Financial Operations Occupations
	-------------------------------------| ---------------------------------------------------
	MGR-CHIEF EXECUTIVES AND LEGISLATORS | BUS-TRAINING AND DEVELOPMENT SPECIALISTS
	MGR-GENERAL AND OPERATIONS MANAGERS  | FIN-APPRAISERS AND ASSESSORS OF REAL ESTATE
	MGR-MARKETING AND SALES MANAGERS     | FIN-CREDIT ANALYSTS
	MGR-ADMINISTRATIVE SERVICES MANAGERS | FIN-FINANCIAL EXAMINERS
	...       ...       ...       ...    |...       ...       ...       ...       ...       ...


3. Major Categories

 * Data: **FOD1P** column (Field of Degree 1st Entry)
 * Classification standard comes from the U.S. Census Bureau 
 * 15 categories in total 
 * We then track the outflow of majors into different occupations.


	Engineering                          | Education
	-------------------------------------| ---------------------------------------------------
	AEROSPACE ENGINEERING                | GENERAL EDUCATION
	BIOLOGICAL ENGINEERING               | ELEMENTARY EDUCATION
	ARCHITECTURAL ENGINEERING            | SPECIAL NEEDS EDUCATION
	BIOMEDICAL ENGINEERING               | ART AND MUSIC EDUCATION
	...       ...       ...       ...    |...       ...       ...       ...       ...       ...


### Visualization

#### BiPart Graph 

<a href="http://qacprojects.wesleyan.edu/visualizations/test/bigPartite.html">(Click me!)</br>![Screen Shot](https://raw.githubusercontent.com/TZstatsADS/cycle1-9/master/output/image/ScreenShot1.png?token=AKN9cU9GaFIwejKfkUzVaqLcxsGX9OY_ks5WuROFwA%3D%3D) </a>

![Screen Shot](https://raw.githubusercontent.com/TZstatsADS/cycle1-9/master/output/image/ScreenShot2.png?token=AKN9cShEtuC4-MfggxyMDMq-rLsKLkFXks5WuRaUwA%3D%3D)

#### Circular Graph

<a href="http://qacprojects.wesleyan.edu/visualizations/test/coffee-from-files.html">(Click me!)</br>![Screen Shot](https://raw.githubusercontent.com/TZstatsADS/cycle1-9/master/output/image/circle.png?token=AKN9cTMC83FRHNiK-izup2aqdQbcY2xXks5Wu4FvwA%3D%3D)</a>


#### Bar Plots

![Screen Shot](https://raw.githubusercontent.com/TZstatsADS/cycle1-9/master/output/image/hist2.png?token=AKN9caexboNF0gwZqok1z65H0MYivr7Dks5WuqWTwA%3D%3D)

![Screen Shot](https://raw.githubusercontent.com/TZstatsADS/cycle1-9/master/output/image/hist.png?token=AKN9ccV9okD7KkPQ-0NELht_ZwPRLHq4ks5WunfCwA%3D%3D)



###T-test Result


![Screen Shot](https://raw.githubusercontent.com/TZstatsADS/cycle1-9/master/output/image/income.png?token=AKN9ccCULz1mkr6BFK03x9WnOrGitwQGks5WuqWVwA%3D%3D)

From the graph we can see computer science and engineering majors are tempted to have higher salaries.
In order to get a more statistical view of our topic, we take people with occupations in CS fields as an example. We conduct a t-test for computer science related majors versus non-computer science related majors.


```
#x:computer science related majors
#y:non-computer science related majors

Welch Two Sample t-test
 
data:  wage.com and wage.non
t = 102.34, df = 1776000, p-value < 2.2e-16
alternative hypothesis: true difference in means is not equal to 0
95 percent confidence interval:
7565.648 7861.103
sample estimates:
mean of x mean of y 
84165.30  76451.92
```

Therefore, the small p-value indicates that having a computer science related degree helps one to earn more in the CS fields ! 

###References
Major Classification Standard:[View Here](http://www.census.gov/prod/2012pubs/acsbr11-04a.pdf) <br />
Occupation Codelist and Classification:[Download Here](https://www.census.gov/people/io/files/2013 ACS 1-year and 2014 SIPP PUMS Occupation code list.xlsx)  <br />
Visualization Inspirations:
[BiPartite](http://bl.ocks.org/NPashaP/9796212)   <br />
[Chord Diagram](http://www.delimited.io/blog/2013/12/8/chord-diagrams-in-d3 ) <br />


Most of the javascript coding credits to http://bl.ocks.org/NPashaP/9796212


###Coding Scripts
All coding scripts are located in folder lib. 

#THANK YOU
