# RV3028_RTC Notes
Simple Python class for Pimoroni RV3028 RTC I2C breakout with a Raspberry Pi Pico

# Installation
Copy rv3028_rtc.py into your project

#You'll need to import some libraries
from machine import Pin, I2C
import rv3028_rtc

#Then initialise an I2C object on the Pico
i2c = machine.I2C(1, scl=Pin(27), sda=Pin(26), freq=100000)

Now initialise an RV3028 object. 

The default I2C address for the Pimoroni breakout is 0x52

In this example I've initialised the Backup Switchover Mode to "LSM", Level Switching Mode

Choosing the backup mode is important. Consult the RV3028 datasheet for details.

See RV-3028-C7_App-Manual.pdf

rtc = rv3208_rtc.RV3028(0x52, i2c, "LSM")


# Available methods

rtc.set_12_hr_clk(status=False):

rtc.set_weekday(weekday)

#Weekday value can be one of mon, tue, wed, thu, fri, sat, sun

rtc.set_date(date)

#Date value must be between 1 and 31

rtc.set_month(month)

#Month value must be between 1 and 12

rtc.set_year(year)

#Year value must be between 2000 and 2099

rtc.set_hours(hours, hr_12_24=None, am_pm=None):

#hr_12_24 defaults to 24 and can be set to either 12 or 24

#Hours must be between 0 and 23 for 24hr clock

#Hours must be between 1 and 12 for 12hr clock

#am_pm must be set to either am or pm for 12hr clock

rtc.set_minutes(minutes)

#Minutes value must be between 0 and 59

rtc.set_seconds(seconds)

#Seconds value must be between 0 and 59

rtc.set_rtc_date(current_date)

#current_date is a tuple with 3 or 4 values (four-digit year, two-digit month, two-digit day, "weekday")

#Weekday value can only be one of None, mon, tue, wed, thu, fri, sat, sun

rtc.set_rtc_time(current_time): 

#time is a tuple with 3 or 5 values (hours, minutes, seconds, 24/12, "am"/"pm")

rtc.set_rtc_date_time(current_date_time)

#current_date_time is a tuple with 6, y or 9 values
#(four-digit year, two-digit month, two-digit day, hours, minutes, seconds)
#(four-digit year, two-digit month, two-digit day, hours, minutes, seconds, "weekday")
#(four-digit year, two-digit month, two-digit day, hours, minutes, seconds, "weekday", 24/12, "am"/"pm")

rtc.get_year()

#returns 4 digit year

rtc.get_month(month_type=False)

#month_type can be "long", "short" or boolean False. Default is boolean False.

#default returns month as an integer between 1 and 12

#month_type == "long" returns month in form January etc.

#month_type == "short" returns month in form Jan etc.
            
rtc.get_date(date_type=False)

#date_type can be "ordinal" or boolean False. Default is boolean False.

#default returns date as an integer between 1 and 31

#date_type == "ordinal" returns date in form 1st, 2nd etc.

#month_type == "short" returns month as Jan etc.

rtc.get_weekday(day_type=False)

#day_type can be "long" or "short"

#day_type == "long" returns weekday in form Monday etc.

#day_type == "short" returns weekday in form Mon etc.

rtc.get_12_hr_clk()

#Returns boolean True or False
    
rtc.get_am():

#Returns boolean True or False

rtc.get_hours():

#Returns an integer between 1 and 24

rtc.get_minutes():

#Returns an integer between 1 and 59

rtc.get_seconds():

#Returns an integer between 1 and 59

rtc.get_rtc_time():

#returns a tuple (hours, minutes, seconds)

rtc.get_rtc_date(day_type=False, date_type=False, month_type=False):

#returns a tuple (weekday, date, month, year)

rtc.get_rtc_date_time(day_type=False, date_type=False, month_type=False):

#returns a tuple (year, month, date, weekday, hours, minutes, seconds, am_pm)

