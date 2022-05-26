# GuzmanEnergy_2022SummerQuant_HW

## Assignment 1: Power Calendar Function

### logistics
iso: In the areas where an ISO is established, it coordinates, controls, and monitors the operation of the electrical power system, usually within a single US state, but sometimes encompassing multiple states.
* WECC and CAISO takes Saturday as a weekday.
* Isos other than MISO have the **DST**: 
  * The second Sunday in March has only 23 hours; the first Sunday in November has 25 hours.
  * It influences offpeak, flat and 7x8.
         
peak.type: five methods to count the time.         
* onpeak: **16h / weekday (also not a NERC holiday)**, interpreted as when a large amount of energy is needed.        
* offpeak: **(24h - onpeak) / day** .       
* flat: **24h / day**.
* 2x16H: **16h / weekend or NERC holiday**.
* 7x8: **8h / day**.

### functions
1. get_hours_daily(iso, peak_type, date, eastern)
returns the number of hours of the day and mark if it's the peak day (non-NERC holiday weekday).
2. get_hours_monthly(iso, peak_type, year, month, eastern)
returns the number of hours of the month and calculate its number of peak days.
3. get_hours(iso, peak_type, period)
returns the number of hours of the period and calculate its number of peak days.
  
### note:   
There's some difference between the reference () and the results of my function. It is due to the difference date of some holidays.
For example, the reference calendar gives 416 for December, 2022 but my function returns 432. It is due to the reference sets Chrismas on 12/26/2022 and my Chrismas is defined on 12/25/2022.

### references:
https://www.nerc.com/comm/OC/RS%20Agendas%20Highlights%20and%20Minutes%20DL/Additional_Off-peak_Days.pdf
https://en.wikipedia.org/wiki/Daylight_saving_time
https://www.geeksforgeeks.org/python-holidays-library/
https://en.wikipedia.org/wiki/Regional_transmission_organization_(North_America)



## Assignment 2: Meter Data formatting

### 1. Loading Datasets with Pandas
Load two csv files into dataframe.

### 2. Merge the data by hour

### 3. Merge two datasets and output with a sum column
Assume the date in the first dataset is in 2013 as well.

### 4. Visualization and Analysis

#### 4.1 Extreme Values
![](/output/Daily%20Consumptions.png)

##### 4.1.1 Summer season
The plot shows, during Jun 7th to Aug 4th, the total consumption is extremely high. Further explore the houly pattern of this period, the peak is around 11pm. So we can assume it's due to the consumption of air conditioning in the hot days.    
The extreme consumption is of the newly added appliance.         
![](/output/Average%20consumptions%20of%20each%20hour%20in%20summer.png)

##### 4.1.2 Sep 12th
The peak of Sep 12th is during 7am to 10am and also due to the consumption of the newly added appliance.

#### 4.2 Hourly pattern
##### 4.2.1 Summer season
In the summer season(Jun-Aug), the peak of a day is around 11pm.
##### 4.2.2 Other seasons
The peak values are in the morning(6am - 9am) and in the early night(18pm-22pm).            
![](/output/Average%20consumptions%20of%20each%20hour%20in%20other%20seasons.png)

#### 4.3 Weekly pattern
Average consumption of a week is getting lower in the weekdays(Mon-Fri), and reaches the peak in weekends.          
![](/output/Average%20consumptions%20of%20each%20weekday.png)


## Assignment 3: EDA and forecast model

### 1. EDA

#### 1.1 Data Cleaning
* Drop the duplicates;
* Replace Nans with 0;
* Encode `PeakType` and `MONTH`.

#### 1.2 Data insights and statistcs
* The dataset comprises of 14986 observations and 12 characteristics.
* There are three types of peak: weekday, weekend, off-peak.
* `HB_NORTH (RTLMP)`: There is notably a large difference between 75% quantile and max value, suggesting that there are extreme value, Outliers.
* `ERCOT (GENERATION_SOLAR_RT)`: Not only there's a large difference between max and 75% q, but also the mean value is much larger than median value, indicating there are outliers.

#### 1.3 Data Visualization
(Here shows just some informative plots. For more details, plz check the jupyter notebook!)
<br/><br/>

![](/output/Monthly%20trend%20of%20rt%20price%20in%202017%20and%202018.png)
* Clearly, the pattern repeats within both 2017 and 2018.
* Generally, the price increases from 2017 to 2017.
<br/><br/>

![](/output/Trend%20in%20different%20time%20frames.png)
* Hour: From 5am to 18pm, the price is increasing and reach the peak at 18pm.
* Peaktype: 'weekday' has the highest price and 'offpeak' has the lowest.
* Month: From January to March and from August to November, the price is decreasing and reach the lowest price of the year in March; From April to July, it's increasing. The price is relatively high in Summer and reaches the highest in July.
* Year: The average price grows from 2017 to 2018.
<br/><br/>

![](/output/Monthly%20and%20Yearly%20outliers.png)
* There are some outliers in January, February, April, October, November and December.
* There are outliers in 2017, but not in 2018.

### 2. Forecast model to predict RTLMP

#### 2.1 Trend
![](/output/365-Day%20Moving%20Average%20of%20Prices.png)

#### 2.2 Seasonality
![](/output/Seasonality.png)
![](/output/Frequency%20Components.png)

#### 2.2 With `lag` feature
![](/output/lags%20plot.png)
With this plot shows, choose **`lags` = 1**.

#### 2.4 Linear Regression
![](/output/Rt%20and%20Predicted%20Prices%20with%20lr%20and%20lags.png)
We can tell from the plot that the lr-predicted prices with `lag` is highly overlapping the real time price.

#### 2.5 Forecasting Model with `lag`
* **Data**: Split data into training and validation sets, with validation having **3000** rows, which is almost 20% of the data.
* **Model**: **LinearRegression(fit_intercept=False)**, to set the y-intercept to 0.
* **Evaluation**: The training RMSLE is **0.068** and validation RMSLE is **0.114**. Both are relatively small, proving that this model gives a good forecasting!!!
![](/output/Forecast.png)

### references:
https://stackoverflow.com/a/49238256/5769929
https://www.kaggle.com/code/maricinnamon/store-sales-time-series-forecast-visualization#3.1.-Linear-Regression
https://www.machinelearningplus.com/time-series/time-series-analysis-python/


## Assignment 4: Learn products of Futures

### Self-learning of market products

#### Product 1: Power Futures - ERN
* Description: 
    * monthly cash settled,
    * based upon the average the peak hourly electricity prices published by ERCOT.
* Settlement Method: Cash settlement
    * **Def of Cash settlement**: upon expiration or exercise, instead of delivering the actual (physical) asset, the seller transfers the associated cash position.
* Contract size: 1 MW
    * **Def of Contract size**: the minimum quantity of an asset that one needs to buy or sell to trade in futures.
* Minimum Price Fluctuation: $0.01 per MWh
    * **Def of Minimum price fluctuation**: the smallest increment of price movement possible in trading a given contract, referred to as a tick. 
        * There are three different types of tick, plus, minus, and zero. A plus tick is when the price of the security is higher than the price it was bought at, a minus tick is when the price of a security is lower than what it was bought at, and a zero tick is when the price is the same. 
* Listing Circle: Up to 50 consecutive monthly Contract Periods
    * **Def of Listing circle**: the period for which the futures contract trades on an exchange.

#### Product 2: Natural Gas Futures - H
Similarly.

#### Product 3: Heat Rate Futures - XPR
* Description: 
    * Firm energy with Liquidated Damages;
    * Physical delivered.
* Schedule: All peak hours, hours ending 0700-2200 in CPT time zone, in non-NERC holiday weekdays.
* sd
    * **Def of daily settlement**: Daily settlement refers to the contract’s settlement price on a daily basis, used to manage daily profit and loss, while final settlement represents the final value of the contract at expiration.



### references:
https://www.businesstoday.in/magazine/basics/story/futures-terms-15618-2010-11-25
https://www.investopedia.com/terms/c/cashsettlement.asp#:~:text=A%20cash%20settlement%20is%20a,transfers%20the%20associated%20cash%20position
https://www.youtube.com/watch?v=LJdC84D97SI
https://www.cmegroup.com/education/courses/introduction-to-equity-index-products/understanding-equity-index-daily-and-final-settlement.html
