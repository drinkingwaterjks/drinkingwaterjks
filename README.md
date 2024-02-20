from machine import Pin, ADC, PWM
from utime import sleep, sleep_ms 
from hcsr04 import HCSR04 

sensor = HCSR04(trigger_pin = 4, echo_pin = 5)
ledv = Pin(19, Pin.OUT)
ledr = Pin(21, Pin.OUT)
servo = PWM(Pin(32), freq = 50)
pot = ADC(Pin(25))

def map_servo(x):
    return int((x - 0) * (125 - 25) / (100 - 0) + 25)

angulos = [0 , 45, 90, 125, 180]



while True: 

    distancia = sensor.distance_cm()
    print("Distancia:{:.0f}cm".format(distancia))
    sleep_ms(50)
    servo

    sensor1 = pot.read_u16()
    print(sensor1) 
    sleep_ms(50)

    if distancia >40:
        ledv.on()
        ledr.off()
        m = map_servo(0)
        servo.duty(m)
    else:
        ledv.off()
        ledr.on()
        m = map_servo(90)
        servo.duty(m)
