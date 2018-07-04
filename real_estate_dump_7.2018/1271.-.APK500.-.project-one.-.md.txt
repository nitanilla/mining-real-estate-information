

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
```


```python
# Quality of Life Rankings
qol_rankings = pd.read_csv("Adam/Final QOL Rankings.csv")

# Rename cities to get similar labels
qol_rankings.set_value(10, 'City', "Montgomery County")
qol_rankings.set_value(14, 'City', "Northern Virginia")
qol_rankings.set_value(17, 'City', "Raleigh")
qol_rankings
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>State</th>
      <th>crime_score</th>
      <th>hosp_score</th>
      <th>Total Score</th>
      <th>QOL Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Atlanta</td>
      <td>GA</td>
      <td>2.4</td>
      <td>4.3</td>
      <td>6.7</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Austin</td>
      <td>TX</td>
      <td>8.1</td>
      <td>3.2</td>
      <td>11.3</td>
      <td>8.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Boston</td>
      <td>MA</td>
      <td>5.6</td>
      <td>2.2</td>
      <td>7.8</td>
      <td>5.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chicago</td>
      <td>IL</td>
      <td>2.3</td>
      <td>3.7</td>
      <td>6.0</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Columbus</td>
      <td>OH</td>
      <td>7.2</td>
      <td>1.4</td>
      <td>8.6</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Dallas</td>
      <td>TX</td>
      <td>5.1</td>
      <td>3.2</td>
      <td>8.3</td>
      <td>5.8</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Denver</td>
      <td>CO</td>
      <td>6.0</td>
      <td>2.0</td>
      <td>8.0</td>
      <td>5.6</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Indianapolis</td>
      <td>IN</td>
      <td>0.0</td>
      <td>1.1</td>
      <td>1.1</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Los Angeles</td>
      <td>CA</td>
      <td>5.5</td>
      <td>4.5</td>
      <td>10.0</td>
      <td>7.2</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Miami</td>
      <td>FL</td>
      <td>4.1</td>
      <td>4.1</td>
      <td>8.2</td>
      <td>5.7</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Montgomery County</td>
      <td>MD</td>
      <td>8.7</td>
      <td>4.8</td>
      <td>13.5</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Nashville</td>
      <td>TN</td>
      <td>2.3</td>
      <td>4.2</td>
      <td>6.5</td>
      <td>4.4</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Newark</td>
      <td>NJ</td>
      <td>3.7</td>
      <td>4.2</td>
      <td>7.9</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>13</th>
      <td>New York</td>
      <td>NY</td>
      <td>6.7</td>
      <td>5.2</td>
      <td>11.9</td>
      <td>8.7</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Northern Virginia</td>
      <td>VA</td>
      <td>10.0</td>
      <td>1.8</td>
      <td>11.8</td>
      <td>8.6</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>3.2</td>
      <td>1.8</td>
      <td>5.0</td>
      <td>3.1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Pittsburgh</td>
      <td>PA</td>
      <td>5.0</td>
      <td>1.8</td>
      <td>6.8</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Raleigh</td>
      <td>NC</td>
      <td>5.4</td>
      <td>2.1</td>
      <td>7.5</td>
      <td>5.2</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Washington</td>
      <td>DC</td>
      <td>2.0</td>
      <td>6.8</td>
      <td>8.8</td>
      <td>6.2</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Business Envrionment Rankings
biz_env_rankings = pd.read_csv("forrest/Rankings_gdp_tax.csv")
biz_env_rankings.set_value(11, "City", "Montgomery County")
biz_env_rankings
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>State_x</th>
      <th>Tax_score</th>
      <th>GDP_score</th>
      <th>Unemp_score</th>
      <th>Total Score</th>
      <th>Biz Env Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Atlanta</td>
      <td>GA</td>
      <td>2.7</td>
      <td>4.4</td>
      <td>4.6</td>
      <td>11.7</td>
      <td>4.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Raleigh</td>
      <td>NC</td>
      <td>7.1</td>
      <td>7.5</td>
      <td>4.6</td>
      <td>19.2</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Indianapolis</td>
      <td>IN</td>
      <td>6.6</td>
      <td>5.0</td>
      <td>8.9</td>
      <td>20.5</td>
      <td>9.3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Columbus</td>
      <td>OH</td>
      <td>5.6</td>
      <td>3.3</td>
      <td>3.9</td>
      <td>12.8</td>
      <td>4.8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Dallas</td>
      <td>TX</td>
      <td>4.0</td>
      <td>6.4</td>
      <td>6.4</td>
      <td>16.8</td>
      <td>7.1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Nashville</td>
      <td>TN</td>
      <td>2.0</td>
      <td>7.2</td>
      <td>8.9</td>
      <td>18.1</td>
      <td>7.9</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Pittsburgh</td>
      <td>PA</td>
      <td>6.6</td>
      <td>3.9</td>
      <td>3.6</td>
      <td>14.1</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Austin</td>
      <td>TX</td>
      <td>4.0</td>
      <td>10.0</td>
      <td>1.0</td>
      <td>15.0</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>4.5</td>
      <td>1.9</td>
      <td>3.6</td>
      <td>10.0</td>
      <td>3.1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Miami</td>
      <td>FL</td>
      <td>6.6</td>
      <td>2.8</td>
      <td>6.8</td>
      <td>16.2</td>
      <td>6.8</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Denver</td>
      <td>CO</td>
      <td>5.3</td>
      <td>6.4</td>
      <td>10.0</td>
      <td>21.7</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Montgomery County</td>
      <td>MD</td>
      <td>8.6</td>
      <td>1.9</td>
      <td>6.1</td>
      <td>16.6</td>
      <td>7.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Washington</td>
      <td>DC</td>
      <td>9.1</td>
      <td>3.6</td>
      <td>0.0</td>
      <td>12.7</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Chicago</td>
      <td>IL</td>
      <td>0.0</td>
      <td>1.1</td>
      <td>3.6</td>
      <td>4.7</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Northern Virginia</td>
      <td>VA</td>
      <td>10.0</td>
      <td>0.0</td>
      <td>7.9</td>
      <td>17.9</td>
      <td>7.8</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Newark</td>
      <td>NJ</td>
      <td>6.8</td>
      <td>2.8</td>
      <td>3.9</td>
      <td>13.5</td>
      <td>5.2</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Los Angeles</td>
      <td>CA</td>
      <td>2.0</td>
      <td>5.0</td>
      <td>5.0</td>
      <td>12.0</td>
      <td>4.3</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Boston</td>
      <td>MA</td>
      <td>8.1</td>
      <td>1.9</td>
      <td>8.2</td>
      <td>18.2</td>
      <td>7.9</td>
    </tr>
    <tr>
      <th>18</th>
      <td>New York</td>
      <td>NY</td>
      <td>2.8</td>
      <td>2.8</td>
      <td>3.9</td>
      <td>9.5</td>
      <td>2.8</td>
    </tr>
  </tbody>
</table>
</div>




```python
# RE Costs & Cost of Living rankings
re_col_rankings = pd.read_csv("jake/Final Rankings RE, COL, & GEO.csv")
re_col_rankings = re_col_rankings[['City/Region', 'State', 'RE & COL Score']]
re_col_rankings.columns = [['City', 'State', 'RE & COL']]
re_col_rankings
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>State</th>
      <th>RE &amp; COL</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Atlanta</td>
      <td>GA</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Austin</td>
      <td>TX</td>
      <td>8.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Boston</td>
      <td>MA</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chicago</td>
      <td>IL</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Columbus</td>
      <td>OH</td>
      <td>8.8</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Dallas</td>
      <td>TX</td>
      <td>8.8</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Denver</td>
      <td>CO</td>
      <td>5.3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Indianapolis</td>
      <td>IN</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Los Angeles</td>
      <td>CA</td>
      <td>0.8</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Miami</td>
      <td>FL</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Montgomery County</td>
      <td>MD</td>
      <td>5.6</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Nashville</td>
      <td>TN</td>
      <td>8.3</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Newark</td>
      <td>NJ</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>New York</td>
      <td>NY</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Northern Virginia</td>
      <td>VA</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>6.7</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Pittsburgh</td>
      <td>PA</td>
      <td>8.2</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Raleigh</td>
      <td>NC</td>
      <td>9.4</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Washington</td>
      <td>DC</td>
      <td>5.7</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Transport Rankings
transport_rankings = pd.read_csv("sara/rankings_trasport_driving.csv")
transport_rankings = transport_rankings[['City', 'State', 'Degree_score']]
transport_rankings['City'] = transport_rankings['City'].str.capitalize()
transport_rankings.set_value(8, 'City', 'Los Angeles')
transport_rankings.set_value(10, 'City', 'Montgomery County')
transport_rankings.set_value(13, 'City', 'New York')
transport_rankings.set_value(14, 'City', 'Northern Virginia')
transport_rankings.columns = [['City', 'State', 'Transport']]
transport_rankings
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>State</th>
      <th>Transport</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Atlanta</td>
      <td>GA</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Austin</td>
      <td>TX</td>
      <td>1.8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Boston</td>
      <td>MA</td>
      <td>6.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chicago</td>
      <td>IL</td>
      <td>3.3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Columbus</td>
      <td>OH</td>
      <td>6.2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Dallas</td>
      <td>TX</td>
      <td>4.3</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Denver</td>
      <td>CO</td>
      <td>5.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Indianapolis</td>
      <td>IN</td>
      <td>6.3</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Los Angeles</td>
      <td>CA</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Miami</td>
      <td>FL</td>
      <td>5.7</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Montgomery County</td>
      <td>MD</td>
      <td>1.8</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Nashville</td>
      <td>TN</td>
      <td>1.5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Newark</td>
      <td>NJ</td>
      <td>3.3</td>
    </tr>
    <tr>
      <th>13</th>
      <td>New York</td>
      <td>NY</td>
      <td>3.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Northern Virginia</td>
      <td>VA</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Pittsburgh</td>
      <td>PA</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Raleigh</td>
      <td>NC</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Washington</td>
      <td>DC</td>
      <td>3.5</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Twitter sentiment rankings
twit_sent_rankings = pd.read_csv("sara/Finalrank.csv")
twit_sent_rankings = twit_sent_rankings[['City', 'Final Degree Score']]
twit_sent_rankings['City'] = twit_sent_rankings['City'].str.capitalize()
twit_sent_rankings.set_value(7, "City", "Montgomery County")
twit_sent_rankings.set_value(9, "City", "Los Angeles")
twit_sent_rankings.set_value(10, "City", "Northern Virginia")
twit_sent_rankings.set_value(16, "City", "New York")
twit_sent_rankings.columns = [['City', 'Twit Sent Score']]
twit_sent_rankings
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>Twit Sent Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Miami</td>
      <td>9.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Pittsburgh</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Nashville</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Atlanta</td>
      <td>9.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Denver</td>
      <td>8.2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Indianapolis</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Austin</td>
      <td>8.3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Montgomery County</td>
      <td>9.1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Newark</td>
      <td>7.9</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Los Angeles</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Northern Virginia</td>
      <td>4.7</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Raleigh</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Columbus</td>
      <td>8.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Boston</td>
      <td>5.1</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Dallas</td>
      <td>8.5</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Philadelphia</td>
      <td>6.1</td>
    </tr>
    <tr>
      <th>16</th>
      <td>New York</td>
      <td>4.3</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Chicago</td>
      <td>7.8</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Washington</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Combine QOL and Twit Sentiment Rankings to get one QOL Score

qol_combined = pd.merge(qol_rankings, twit_sent_rankings, how='left', left_on='City', right_on='City')
qol_combined = qol_combined[['City', 'State', 'crime_score', 'hosp_score', 'Twit Sent Score']]
qol_combined['Total Score'] = qol_combined['crime_score']+qol_combined['hosp_score']+qol_combined['Twit Sent Score']

# set variables and rank total quality of life scores
tot_max = max(qol_combined['Total Score'])
tot_min = min(qol_combined['Total Score'])
tot_range = tot_max - tot_min
qol_combined['Quality of Life'] = 2.0

for index, row in qol_combined.iterrows():
    score = (abs(row['Total Score'] - tot_min))/tot_range*10
    score = round(score, 1)
    qol_combined.set_value(index, 'Quality of Life', score)

qol_combined
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City</th>
      <th>State</th>
      <th>crime_score</th>
      <th>hosp_score</th>
      <th>Twit Sent Score</th>
      <th>Total Score</th>
      <th>Quality of Life</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Atlanta</td>
      <td>GA</td>
      <td>2.4</td>
      <td>4.3</td>
      <td>9.0</td>
      <td>15.7</td>
      <td>5.9</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Austin</td>
      <td>TX</td>
      <td>8.1</td>
      <td>3.2</td>
      <td>8.3</td>
      <td>19.6</td>
      <td>8.2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Boston</td>
      <td>MA</td>
      <td>5.6</td>
      <td>2.2</td>
      <td>5.1</td>
      <td>12.9</td>
      <td>4.2</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Chicago</td>
      <td>IL</td>
      <td>2.3</td>
      <td>3.7</td>
      <td>7.8</td>
      <td>13.8</td>
      <td>4.8</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Columbus</td>
      <td>OH</td>
      <td>7.2</td>
      <td>1.4</td>
      <td>8.0</td>
      <td>16.6</td>
      <td>6.4</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Dallas</td>
      <td>TX</td>
      <td>5.1</td>
      <td>3.2</td>
      <td>8.5</td>
      <td>16.8</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Denver</td>
      <td>CO</td>
      <td>6.0</td>
      <td>2.0</td>
      <td>8.2</td>
      <td>16.2</td>
      <td>6.2</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Indianapolis</td>
      <td>IN</td>
      <td>0.0</td>
      <td>1.1</td>
      <td>4.7</td>
      <td>5.8</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Los Angeles</td>
      <td>CA</td>
      <td>5.5</td>
      <td>4.5</td>
      <td>5.1</td>
      <td>15.1</td>
      <td>5.5</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Miami</td>
      <td>FL</td>
      <td>4.1</td>
      <td>4.1</td>
      <td>9.2</td>
      <td>17.4</td>
      <td>6.9</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Montgomery County</td>
      <td>MD</td>
      <td>8.7</td>
      <td>4.8</td>
      <td>9.1</td>
      <td>22.6</td>
      <td>10.0</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Nashville</td>
      <td>TN</td>
      <td>2.3</td>
      <td>4.2</td>
      <td>10.0</td>
      <td>16.5</td>
      <td>6.4</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Newark</td>
      <td>NJ</td>
      <td>3.7</td>
      <td>4.2</td>
      <td>7.9</td>
      <td>15.8</td>
      <td>6.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>New York</td>
      <td>NY</td>
      <td>6.7</td>
      <td>5.2</td>
      <td>4.3</td>
      <td>16.2</td>
      <td>6.2</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Northern Virginia</td>
      <td>VA</td>
      <td>10.0</td>
      <td>1.8</td>
      <td>4.7</td>
      <td>16.5</td>
      <td>6.4</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>3.2</td>
      <td>1.8</td>
      <td>6.1</td>
      <td>11.1</td>
      <td>3.2</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Pittsburgh</td>
      <td>PA</td>
      <td>5.0</td>
      <td>1.8</td>
      <td>8.4</td>
      <td>15.2</td>
      <td>5.6</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Raleigh</td>
      <td>NC</td>
      <td>5.4</td>
      <td>2.1</td>
      <td>6.1</td>
      <td>13.6</td>
      <td>4.6</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Washington</td>
      <td>DC</td>
      <td>2.0</td>
      <td>6.8</td>
      <td>0.0</td>
      <td>8.8</td>
      <td>1.8</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge all dataframes into the final rankings
final_merge1 = pd.merge(re_col_rankings, biz_env_rankings, how='left', left_on='City', right_on='City')
final_merge1 = final_merge1[['City', 'State', 'RE & COL', 'Biz Env Score']]
final_merge2 = pd.merge(final_merge1, qol_combined, how='left', left_on='City', right_on='City')
final_merge2 = final_merge2[['City', 'State_x', 'RE & COL', 'Biz Env Score', 'Quality of Life']]
final_merge3 = pd.merge(final_merge2, transport_rankings, how='left', left_on='City', right_on='City')
final_merge3 = final_merge3[['City', 'State', 'RE & COL', 'Biz Env Score', 'Quality of Life', 'Transport']]
final_merge3.columns = [['City/Region', 'State', 'Real Estate & Cost of Living', 'Business Environment', 'Quality of Life', 'Transportation']]
final_merge3['Total Score'] = final_merge3['Real Estate & Cost of Living']+final_merge3['Business Environment']+final_merge3['Quality of Life']+final_merge3['Transportation']
final_merge3 = final_merge3.sort_values('Total Score', ascending=False)
rank_index = np.arange(1,20,1)
final_merge3.set_index(rank_index, inplace=True, drop=True)
final_merge3
plt.legend((p1[0], p2[0], p3[0], p4[0]), ('Real Estate & Cost of Living', 'Business Environment', 'Quality of Life', 'Transportation'))
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>City/Region</th>
      <th>State</th>
      <th>Real Estate &amp; Cost of Living</th>
      <th>Business Environment</th>
      <th>Quality of Life</th>
      <th>Transportation</th>
      <th>Total Score</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>Raleigh</td>
      <td>NC</td>
      <td>9.4</td>
      <td>8.5</td>
      <td>4.6</td>
      <td>8.5</td>
      <td>31.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Pittsburgh</td>
      <td>PA</td>
      <td>8.2</td>
      <td>5.5</td>
      <td>5.6</td>
      <td>10.0</td>
      <td>29.3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Dallas</td>
      <td>TX</td>
      <td>8.8</td>
      <td>7.1</td>
      <td>6.5</td>
      <td>4.3</td>
      <td>26.7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Denver</td>
      <td>CO</td>
      <td>5.3</td>
      <td>10.0</td>
      <td>6.2</td>
      <td>5.0</td>
      <td>26.5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Columbus</td>
      <td>OH</td>
      <td>8.8</td>
      <td>4.8</td>
      <td>6.4</td>
      <td>6.2</td>
      <td>26.2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Miami</td>
      <td>FL</td>
      <td>6.1</td>
      <td>6.8</td>
      <td>6.9</td>
      <td>5.7</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Atlanta</td>
      <td>GA</td>
      <td>10.0</td>
      <td>4.1</td>
      <td>5.9</td>
      <td>5.1</td>
      <td>25.1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Montgomery County</td>
      <td>MD</td>
      <td>5.6</td>
      <td>7.0</td>
      <td>10.0</td>
      <td>1.8</td>
      <td>24.4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Austin</td>
      <td>TX</td>
      <td>8.2</td>
      <td>6.1</td>
      <td>8.2</td>
      <td>1.8</td>
      <td>24.3</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Indianapolis</td>
      <td>IN</td>
      <td>8.5</td>
      <td>9.3</td>
      <td>0.0</td>
      <td>6.3</td>
      <td>24.1</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Nashville</td>
      <td>TN</td>
      <td>8.3</td>
      <td>7.9</td>
      <td>6.4</td>
      <td>1.5</td>
      <td>24.1</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Boston</td>
      <td>MA</td>
      <td>2.5</td>
      <td>7.9</td>
      <td>4.2</td>
      <td>6.2</td>
      <td>20.8</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Philadelphia</td>
      <td>PA</td>
      <td>6.7</td>
      <td>3.1</td>
      <td>3.2</td>
      <td>6.5</td>
      <td>19.5</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Northern Virginia</td>
      <td>VA</td>
      <td>5.1</td>
      <td>7.8</td>
      <td>6.4</td>
      <td>0.0</td>
      <td>19.3</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Newark</td>
      <td>NJ</td>
      <td>4.0</td>
      <td>5.2</td>
      <td>6.0</td>
      <td>3.3</td>
      <td>18.5</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Washington</td>
      <td>DC</td>
      <td>5.7</td>
      <td>4.7</td>
      <td>1.8</td>
      <td>3.5</td>
      <td>15.7</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Los Angeles</td>
      <td>CA</td>
      <td>0.8</td>
      <td>4.3</td>
      <td>5.5</td>
      <td>5.1</td>
      <td>15.7</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Chicago</td>
      <td>IL</td>
      <td>5.1</td>
      <td>0.0</td>
      <td>4.8</td>
      <td>3.3</td>
      <td>13.2</td>
    </tr>
    <tr>
      <th>19</th>
      <td>New York</td>
      <td>NY</td>
      <td>0.0</td>
      <td>2.8</td>
      <td>6.2</td>
      <td>3.0</td>
      <td>12.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Create stacked bar chart of final results
plt.style.use('ggplot')

N = len(final_merge3.index)
RE_COL = final_merge3['Real Estate & Cost of Living']
Biz_Env = final_merge3['Business Environment']
QOL = final_merge3['Quality of Life']
Trans = final_merge3['Transportation']
ind = np.arange(N)
width = 0.5

plt.figure(figsize=(15,10))
p1 = plt.bar(ind, RE_COL, width)
p2 = plt.bar(ind, Biz_Env, width, bottom=RE_COL)
p3 = plt.bar(ind, QOL, width, bottom= np.array(RE_COL)+np.array(Biz_Env))
p4 = plt.bar(ind, Trans, width, bottom=np.array(RE_COL)+np.array(Biz_Env)+np.array(QOL))


plt.ylabel('Total Scores')
plt.xticks(ind, final_merge3['City/Region'], rotation=45, ha='right')
plt.yticks(np.arange(0, 40, 5))
plt.legend((p1[0], p2[0], p3[0], p4[0]), ('Real Estate & Cost of Living', 'Business Environment', 'Quality of Life', 'Transportation'))
plt.title('Amazon HQ2 Location Final Rankings')
plt.savefig('Amazon HQ2 Location Final Rankings.png')
plt.show()

```


![png](output_8_0.png)

