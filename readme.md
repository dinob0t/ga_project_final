# Investigating the relationship between solar magnetic activity and coronal mass ejections

## Summary

An coronal mass ejection (CME) is an energetic event in which the sun ejects a large body of plasma along with a frozen in magnetic field configuration into the solar wind. A so called 'halo' event occurs when this ejection appears primarily along the Earth-Sun field of view. It is these events in particular which pose risk to Earth because of the strong association with space weather and geomagnetic storms arising from the CME's magnetic interaction with the Earth's magnetic field. This poses problems for astronauts, satellites, high frequency communications, and may induce currents in any long conductors near the Earth's poles (pipelines, powerlines etc.) It is clearly of interest to understand and predict these events.

Because of the strong association of CMEs and the solar magnetic field configuration, a natural place to start looking at predictors is the sun spot cycle (sun spots occur because the twisted magnetic configurations inhibit heat convection and hence the plasma cools appearing dark, especially in hydrogen-alpha line images of the sun). Excellent data on sun spot numbers exists as far back as the 1800s, and more recently the latitude and longitude of sun spot areas on the sun is documented daily. Other indicators of solar activity include the solar irradiance or radio flux (akin to the power output of the sun) which can be observed at the Lyman Alpha line or 10.7cm Hydrogen line, respectively.  Even better are the vector magnetograms that directly image the magnetic field configuration on the sun's surface for which we have images produced every 15 minutes since 2010. Furthermore to train our classifiers we have the LASCO catalogue of CMEs which has documented every (observerable/detectable) CME since 1997.

## Project files
### Analysis
`cmes.ipynb` - looks at the association of more qualitative sun activity measures on predicting CMEs.

`magnetograms.ipynb` - uses vector magnetogram data from 2010-2013 to analyse solar activity and attempt to predict CMEs.

### Feature data
`issn.md` - international sunspot number record.

`daily_area.txt` - daily area of the sun covered in sunspots.

`lyman_alpha.txt` - daily solar irradiance.

`f10.7.txt` - daily radio flux.

`g*.txt` - Greenwich sunspot grouping data (tracks groups of sunspots).

`/data/all_256` - (Not included here) 3.4GB of vector magnetogram data from 2010-2013.

### Target data
`cme_catalogue.md` - List of times and other attributes for all CMEs since 1997. Objective is to predict the number of CMEs in a given time interval.

![alt text](https://github.com/dinob0t/ga_project_final/blob/master/monthly_mean_cmes.png)<br>
(Fig 1: Mean CMEs per month grouped by year)

## Part 1 - Proxies for solar activity - analysis and prediction

### Known features that correlate with solar activity
1. The number of sun spots

![alt text](https://github.com/dinob0t/ga_project_final/blob/master/monthly_mean_ssn_clip.png)<br>
(Fig 2: Mean CMEs per month grouped by year)

2. The area of the solar disc covered by sun spots

![alt text](https://github.com/dinob0t/ga_project_final/blob/master/monthly_mean_ssa.png)<br>
(Fig 3: Mean area of solar disc covered per month grouped by year)

3. The solar irradiance 

![alt text](https://github.com/dinob0t/ga_project_final/blob/master/monthly_mean_lyman.png)<br>
(Fig 4: Mean solar irradiance grouped by year)

4. The solar radio flux

![alt text](https://github.com/dinob0t/ga_project_final/blob/master/monthly_mean_10.7.png)<br>
(Fig 5: Mean F10.7 radio emission by year)

Figures 2-5 show that all these measures are highly correlated with each other and are likely to be related to the same variation that we are trying to model. We require additional independent features.

### Tracking sun spot groups

The Greenwich sunspot grouping data tracks information about any number of sunspots that exist on the solar disc at one time - sometimes there are no sunspots and sometimes there are many. In order to incorporate the sunspot information as additional features we can choose a number (N) of sunspots to track, chosen by sorting on a particular aspect of the sunspot group (i.e. size, position, etc). In the absence of any sunspots, the columns representing the parameters of the sunspot data are set to zero.

### Lagging previous CME information

The information required to predict the number of CMEs on a particular day is likely to be related to CME activity on the day before. Therefore a number of CME parameters such as size, velocity, onset hour etc., are lagged by one day and added as additional features. In the case that there are multiple CMEs the day before then the average values of the features is used.

### Attempted target

1. Predict the number of CMEs tomorrow based on the information for today. Fig 6 shows 

![alt text](https://github.com/dinob0t/ga_project_final/blob/master/correlation_cme_ssn_daily.png)<br>
(Fig 6: Showing correlation between sunspot number and cme number per day)

2. Predict the number of CMEs next month based on the information for this month (1 month is approximately 1 solar cycle)
![alt text](https://github.com/dinob0t/ga_project_final/blob/master/correlation_cme_ssn_monthly.png)</br><br>
(Fig 7: Showing correlation between sunspot number and cme number per month))

### Classifiers

1. Random Forest for attempted target 1, as the number of categories representing the number of CMEs on any given day is limited to about 10
2. Linear Model Regression for attempted target 2, as there are a large number of CMEs occurring over the course of a month 

## Results
1. Random Forest - predicting for a day
```
R^2 train: 0.340327415264
R^2 test: 0.32688172043
Classification Report
             precision    recall  f1-score   support

        0.0       0.49      0.75      0.59      1079
        1.0       0.27      0.23      0.25       959
        2.0       0.26      0.31      0.28       762
        3.0       0.22      0.35      0.27       583
        4.0       0.00      0.00      0.00       418
        5.0       0.00      0.00      0.00       246
        6.0       0.00      0.00      0.00       152
        7.0       0.00      0.00      0.00        68
        8.0       0.00      0.00      0.00        32
        9.0       0.00      0.00      0.00        24
       10.0       0.00      0.00      0.00         6
       11.0       0.00      0.00      0.00         4
       12.0       0.00      0.00      0.00         2
       13.0       0.00      0.00      0.00         1
       14.0       0.00      0.00      0.00         1

avg / total       0.26      0.34      0.29      4337

             precision    recall  f1-score   support

        0.0       0.47      0.71      0.57       446
        1.0       0.28      0.27      0.27       401
        2.0       0.25      0.29      0.26       347
        3.0       0.21      0.34      0.26       247
        4.0       0.00      0.00      0.00       194
        5.0       0.00      0.00      0.00       101
        6.0       0.00      0.00      0.00        61
        7.0       0.00      0.00      0.00        31
        8.0       0.00      0.00      0.00        18
        9.0       0.00      0.00      0.00         8
       10.0       0.00      0.00      0.00         4
       11.0       0.00      0.00      0.00         1
       13.0       0.00      0.00      0.00         1

avg / total       0.25      0.33      0.28      1860

Feature Importance
(0.10217336393637823, 'L_speed')
(0.093088329644439222, '2nd_o_speed')
(0.092635194989601835, '2nd_o_speed_20R')
(0.075360227964301738, 'F10.7')
(0.075162723733324707, 'hour')
(0.060248208204694925, 'LymanAlpha')
(0.056812832819784748, 'Central_PA')
(0.052773346909765755, 'Width')
(0.042827630101142759, 'CME')
(0.04272818297068276, 'ssn')
```
![alt text](https://github.com/dinob0t/ga_project_final/blob/master/prediction_cmes_vs_ssn_daily.png)<br>
(Fig 8: Sunspots vs CME numbers per day (blue - data, red - predicted))


2. Ridge Regression (2nd degree polynomial)- predicting for a month
```
R^2 train: 0.653400997278
R^2 test: 0.507888792648
MAPE train: 129.544504755
MAPE test: 173.152010099
```
![alt text](https://github.com/dinob0t/ga_project_final/blob/master/prediction_cmes_vs_ssn_monthly.png) </br> <br>
(Fig 9: Sunspots vs CME numbers per month (blue - data, red - predicted))

### Discussion


## Part 2 - Vector magnetogram analysis
### Summary

### Data scraping

### Data preparation

### Dimensionality reduction - PCA

### Dimensionality reduction - PCA

### Dimensionality reduction - PCA

### Target

### Classifier

### Results

### Discussion

## Conclusion





Original dimensionality / all data / no time_since
0.641176799121
0.425937394356

Reduce dimensionality to 100 / all data / no time_since
0.500161009592
0.499918964912
Reduce dimensionality to 100 / all data / time_since
0.568281704901
0.565537872349
Reduce dimensionality to 100 / both data / no time_since
0.500259467213
0.5
Reduce dimensionality to 100 / both data / time_since
0.61490019672
0.615946052001

SSIM / all data / no time_since
0.5
0.5
SSIM / all data / time_since
0.529790037914
0.532229086478

SSIM / both data / no time_since
0.65747489485
0.671255472966
SSIM / both data / time_since
0.592279662576
0.595695772371


RF - SSIM / both / time_since
0.726747974389
0.725100209575
RF - SSIM / both / no_time_since
0.710660681846
0.706026340431

sun_disc_bin_count / all data /  no time_since
0.53994641115
0.538337877738

sun_disc_bin_count / all data /  time_since
0.586106075217
0.58420156092

sun_disc_bin_count + ssim / all data /  time_since
0.592799779234
0.592754552035



