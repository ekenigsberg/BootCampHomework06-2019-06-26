# BootCampHomework06-2019-06-26

[Jupyter Notebook Solution](https://github.com/ekenigsberg/BootCampHomework06-2019-06-26/blob/master/WeatherPy.ipynb)<br/>
to<br/>
[Data Analytics Boot Camp Homework #6](https://github.com/the-Coding-Boot-Camp-at-UT/UTAMCB201904DATA3/tree/master/06-Python-APIs/Homework/Instructions)

# WeatherPy Analysis

* **Temperature does indeed increase as we approach the equator.** 
  * Linear regression shows that, at the time of the analysis, we expect a city's temperature at the equator to be 82.8 degrees Fahrenheit, and that temperature decreases by 0.0062 degrees per mile from the equator:
  * **TempF = -0.0062 × EqtrDistMi + 82.7643**
  * This regression has an **R² of 0.292**, meaning that the model explains a little less than one-third of the variation in Temperatures between cities, using solely Distance from Equator in Miles. Not bad.
  * The **< 0.01% P-stat** for the coefficient of Distance from Equator in Miles means it is highly likely to be significant.
  * Because the original question asked, _"What's the weather like **as we approach the equator**?"_, I opted to transform Latitude into Distance from the Equator using the insight from [Sciencing.com](http://bit.ly/latitudetomiles) that one degree of latitude is equal to about 69.2 miles.
  * The few (four!) cities in my data set that were below freezing testify that the relationship is far from iron-clad: one of them is in Peru (?!). The other three are in all Southern Argentina. A little surprising that nothing from, say, Australia fell into the sample.
  * ![Distance from Equator vs Temperature](https://github.com/ekenigsberg/BootCampHomework06-2019-06-26/blob/master/Dist%20vs%20Temp.png)
  * ![Distance from Equator vs Temperature Regression](https://github.com/ekenigsberg/BootCampHomework06-2019-06-26/blob/master/Dist%20vs%20Temp%20LinReg.png)

* **Neither Humidity, nor Cloud Cover, nor Wind Speed is similarly explained by proximity to the equator.**
  * The graphs for those relationships look random, regardless whether using Latitude or Distance from Equator in Miles.
  * The linear regressions agree: the R²s for those regressions range from 0.000 to 0.003, with coefficient P-stats that can't reject the null hypothesis with confidence.
  * ![Distance from Equator vs Humidity](https://github.com/ekenigsberg/BootCampHomework06-2019-06-26/blob/master/Dist%20vs%20Hum.png)
  * ![Distance from Equator vs Cloudiness](https://github.com/ekenigsberg/BootCampHomework06-2019-06-26/blob/master/Dist%20vs%20Cloud.png)
  * ![Distance from Equator vs Wind Speed](https://github.com/ekenigsberg/BootCampHomework06-2019-06-26/blob/master/Dist%20vs%20Wind.png)

*  For completists: the graphs that use Latitude (not Distance from Equator) are below.

![Latitude vs Temperature](https://github.com/ekenigsberg/BootCampHomework06-2019-06-26/blob/master/Lat%20vs%20Temp.png)
![Latitude vs Humidity](https://github.com/ekenigsberg/BootCampHomework06-2019-06-26/blob/master/Lat%20vs%20Hum.png)
![Latitude vs Cloudiness](https://github.com/ekenigsberg/BootCampHomework06-2019-06-26/blob/master/Lat%20vs%20Cloud.png)
![Latitude vs Wind Speed](https://github.com/ekenigsberg/BootCampHomework06-2019-06-26/blob/master/Lat%20vs%20Wind.png)

# Technical Insights

* Transforming Latitude into Distance from Equator enables running linear regressions. The **ols()** method from the **statsmodels.formula.api** library produces nicely-formatted output from plain-English parameters like **'Y~A+B'**.
* Because all four analyses are essentially the same (just with different variables and graph boundaries), I created a function to spit out the graphs.
* I was tickled to learn that [the documentation tells us](https://matplotlib.org/users/colors.html) that Matplotlib accepts [color names](https://matplotlib.org/users/colors.html) as determined in a survey conducted by the great, nerdy [comic strip xkcd](https://xkcd.com): just name the color with the **xkcd:** prefix and use plain English (eg, **'xkcd:purplish pink'**).
