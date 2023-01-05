# Temperature and humumidity sensor
This project is about building a temperature and humidity measuring machine using DHT22 sensor and raspberry pi
This machine will facilitate us with atmospheric conditions 
By connecting LCD you can present data on LCD
This machine will give time to time data with date so it makes easy to keep data.
# additions
Can built a robot which can be controlled by this machine and we can use this machine as a sensor.
Adding other sensors which can be used for more information of climate.
We can use temperature sensor in different machines to make them work automatically e.g. Air conditioning system or heating system (if temperature of room increases some
limit machine turn on or if decreases some limit it turns off automatically)
MS8607 sensor can be used instead of dht22 as it is much more accurate as well as it can also measure pressure.
Can be used to help different behaviour of robot work
# difficulties
DHT22 has slower sample rate and sometimes there will be Inconsistencies in the readings.
You can’t measure any other value e.g. (pressure, rainfall, etc) so that’s a drawback of this sensor if you are making any machine to measure weather conditions.

This project is related to a small and affordable machine consisting of sensor, raspberry pi, Lcd, resistor and some other components. This machine should measure temperature and humidity of the surrounding and presents its measurements on a small Lcd connected to it. Time and date when these measurements are taken should also be shown so it can be helpful to keep data. Sensors such as Doppler Radar, gauge sensor to measure pressure, wind speed, rainfall can be used to make this machine a proper weather updating machine which can give data about different aspects of environment. Moreover, anyone can wish to work further on this project to control robots, controlling air conditioning and heating system by using this temperature sensor.  

# final code
import os
import time
import Adafruit_DHT

DHT_SENSOR = Adafruit_DHT.DHT22
DHT_PIN = 4

try:
    f = open('/home/pi/humidity.csv', 'a+')
    if os.stat('/home/pi/humidity.csv').st_size == 0:
            f.write('Date,Time,Temperature,Humidity\r\n')
except:
    pass

while True:
    humidity, temperature = Adafruit_DHT.read_retry(DHT_SENSOR, DHT_PIN)

    if humidity is not None and temperature is not None:
        f.write('{0},{1},{2:0.1f}*C,{3:0.1f}%\r\n'.format(time.strftime('%m/%d/%y'), time.strftime('%H:%M'), temperature, humidity))
    else:
        print("Failed to retrieve data from humidity sensor")

    time.sleep(30)
