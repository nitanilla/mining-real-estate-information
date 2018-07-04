# NBAHackathon
NBA Hackathon 2016 - Voronoi Defense Metrics 
A Real Estate Economy Point of View

## Credits
Chengyu Dai, Josh Shifman, Evan Chavis, Danny Vargovich

Michgian Data Science Team, University of Michigan

## Results
[NBViewer](https://nbviewer.jupyter.org/github/jdaaph/NBAHackathon/blob/master/voronoi.ipynb)

Please check out our working code hosted in NBViewer!

![Original Voronoi Tessellation ](orig.png?raw=true "Title" =300x)

![Leave One Out Voronoi Tessellation ](take1out.png?raw=true "Title" =300x)

## Brief Statement of Methodology
#### Not all spots on court is created equal: 
We base our research on one of the previously calculated discretized model based on shot success probability.	![court_value](court_value.png?raw=true "Title" =300x)

#### Voronoi tessellation tells who controls where
And the control weight decays with the increase of distance between the spot and nearest player. The control weighted sum of land value of a player can be readily calculated for any time frame.

#### A Players' "Defensive Value" is the difference between the offensive team's total controlled value
Do Voronoi stuff with the player of interest taken out from the court. Then the offensive team would have a larger total land value. The difference between the value of the opponent team with and without the defensive player is the metric that we define.


#### Entropy!
When viewing the players' controlled domains on the court, we can interpret it naturally as a probability distribution. Defining entropy is natural and simple.


## Data
NBA provided the data specifically for this event and unfortunately not okay to share

## References:
A lot. The major ones are:

1. Cervone, Dan, Luke Bornn, and Kirk Goldsberry. "NBA Court Realty."
2. Adams, Ryan Prescott, George E. Dahl, and Iain Murray. "Incorporating side information in probabilistic matrix factorization with gaussian processes." arXiv preprint arXiv:1003.4944 (2010).
APA	


