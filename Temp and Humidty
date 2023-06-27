
from machine import Pin    # library for pin access      
import time                # library for making delays between reading
import urequests 
import network 
import dht 
 
HTTP_HEADERS = {'Content-Type': 'application/json'} 
THINGSPEAK_WRITE_API_KEY = 'QHI4DS0XJABRZGZE'  
 
ssid = 'CasA Brizio'
password = 'Hassan123'
 
# Configure Pico W as Station
sta_if=network.WLAN(network.STA_IF)
sta_if.active(True)
 
if not sta_if.isconnected():
    print('connecting to network...')
    sta_if.connect(ssid, password)
    while not sta_if.isconnected():
     pass
print('network config:', sta_if.ifconfig()) 

tempSensor = dht.DHT11(Pin(27))     # DHT11 Constructor 

while True:
    try:
        tempSensor.measure()
        temperature = tempSensor.temperature()
        humidity = tempSensor.humidity()
        print("Temperature is {} degrees Celsius and Humidity is {}%".format(temperature, humidity))
    except:
        pass
    time.sleep(2)

    dht_readings = {'field1':temperature, 'field2':humidity} 
    request = urequests.post( 'http://api.thingspeak.com/update?api_key=' + THINGSPEAK_WRITE_API_KEY, json = dht_readings, headers = HTTP_HEADERS )  
    request.close() 
    print(dht_readings) 
