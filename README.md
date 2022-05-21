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
![plot](/output/Daily Consumptions.png)
##### 4.1.1 Summer season
The plot shows, during Jun 7th to Aug 4th, the total consumption is extremely high. Further explore the houly pattern of this period, the peak is around 11pm. So we can assume it's due to the consumption of air conditioning in the hot days.    
The extreme consumption is of the newly added appliance.
##### 4.1.2 Sep 12th
The peak of Sep 12th is during 7am to 10am and also due to the consumption of the newly added appliance.

#### 4.2 Hourly pattern
##### 4.2.1 Summer season
In the summer season(Jun-Aug), the peak of a day is around 11pm.
##### 4.2.2 Other seasons
The peak values are in the morning(6am - 9am) and in the early night(18pm-22pm).

#### 4.3 Weekly pattern
Average consumption of a week is getting lower in the weekdays(Mon-Fri), and reaches the peak in weekends.
