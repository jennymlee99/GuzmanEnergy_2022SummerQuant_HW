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
  
### Note:   
There's some difference between the reference () and the results of my function. It is due to the difference date of some holidays.
For example, the reference calendar gives 416 for December, 2022 but my function returns 432. It is due to the reference sets Chrismas on 12/26/2022 and my Chrismas is defined on 12/25/2022.
