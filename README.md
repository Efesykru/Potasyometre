from machine import Pin, SoftI2C,PWM
import time
import hcsr04
import ssd1306

sensor = hcsr04.HCSR04(trigger_pin=16, echo_pin=4,echo_timeout_us=10000)

p21 = Pin(21, Pin.OUT)

buzzer = PWM(p21)

i2c = SoftI2C(scl=Pin(23),sda=Pin(22))
oled = ssd1306.SSD1306_I2C(128,64,i2c)
while True:
    mesafe = sensor.distance_cm()
    print(mesafe)
    oled.text(str(mesafe),32,32)
    oled.show()
    oled.fill(0)
    time.sleep(0.2)
    
