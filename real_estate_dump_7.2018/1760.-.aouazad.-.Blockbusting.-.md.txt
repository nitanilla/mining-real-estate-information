# Blockbusting

This repository includes R code for the paper ["Blockbusting: Brokers and the Dynamics of Segregation", in the May 2015 edition of the Journal of Economic Theory.](http://www.sciencedirect.com/science/journal/00220531/157)

> The paper presents a dynamic model of neighborhood segregation where fee motivated real estate brokers match sellers optimally either to minority or to white buyers. In an initially all-white neighborhood, real estate brokers thus either keep the neighborhood in a steady-state white equilibrium or trigger racial transition by matching sellers to minority buyers, a process called blockbusting. Racial transition leads to a higher rate of property turnover in the neighborhood once the fraction of minorities has reached a tipping point—but racial transition also leads to lower prices, and this is the trade-off faced by a broker. The model shows that with multiple brokers, blockbusting profit per broker is lower as brokers free ride on each other's groundbreaking efforts. The model predicts that racial transition will happen in the neighborhood when (i) the number of brokers is limited, (ii) racial preferences lie in an intermediate range, (iii) the arrival rate of offers is intermediate. Otherwise, real estate brokers steer white households toward white buyers.

Using this code allows replication of the figures, as well as testing the impact of the parameters on the model's dynamic equilibrium.

## Files

- _howard-one-broker.R_ Finds the unique Markov Perfect Equilibrium for the main model (Section 2)
- _howard-continuum.R_ Code for Appendix B - A Continuum of Brokers
- _blockbusting.R_  Starting from an all-white neighborhood, assuming the broker blockbusts, finds profit at each time t, valuations, prices at each time t (Sections 3.2 and 4)

## More

Personal research website at [www.ouazad.com/research.html](http://www.ouazad.com/research.html).
