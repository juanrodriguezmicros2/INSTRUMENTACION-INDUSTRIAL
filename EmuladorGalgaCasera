from machine import Pin, I2C, ADC
import ssd1306
import time
led = machine.Pin("LED", machine.Pin.OUT)
# Pines I2C para la Raspberry Pi Pico W
i2c = I2C(0, scl=Pin(17), sda=Pin(16))
#Definicion del boton de la Tara
button = Pin(22, Pin.IN, Pin.PULL_UP)
# Inicializar el ADC en el pin 28
sensor_value = ADC(28)
# Dirección I2C de la pantalla OLED y tamaño
oled_width = 128
oled_height = 64
oled = ssd1306.SSD1306_I2C(oled_width, oled_height, i2c)
#Inicializacion del boton de la Tara
Tara=0
while True:
    # Leer valor del sensor analógico
    adc_value = sensor_value.read_u16()
    #Aplicacion del emulador
    voltage =( ((adc_value * 3.3 / 65535)-0.802)/0.00285)
    #Actuacion de la tara
    Salida=voltage-Tara
    #Aplicacion de la tara
    if button.value() == 0:
        print('Button is pressed')
        Tara=voltage
        led.on()
    else:
        print('Button is not pressed')
        led.off()
    print(Tara)

    # Limpiar la pantalla
    oled.fill(0)

    # Mostrar texto
    oled.text("Peso:""{:.3f} g".format(Salida),0, 30)
    oled.show()

    # Esperar antes de la siguiente lectura
    time.sleep(0.5)
