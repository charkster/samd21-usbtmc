# samd21-usbtmc
![picture](https://cdn-learn.adafruit.com/assets/assets/000/095/173/large1024/adafruit_products_QTPy_top.jpg)


**SAMD21's ADC, DAC and GPIO** are controllable with custom **SCPI** commands. **World's smallest lab equipment.**
The seeeduino_xiao_usbtmc.uf2 file was created using the tinyusb usbtmc device example. I just made some minor changes to the main.c, usbtmc_app.c and usbtmc_app.h files to create this proof of concept. The **DAC pin is PA02, ADC pin is PA04 and GPIO pin is PA10**. A Seeeduino Xiao or Adafruit QT PY can be flashed with the included UF2 file and they should just work (please note that PA04 and PA10 are on different board pins for the Xiao and QT PY).

https://learn.adafruit.com/assets/95390

https://files.seeedstudio.com/wiki/Seeeduino-XIAO/res/Seeeduino-XIAO-v1.0-SCH-191112.pdf

Here are the supported SCPI commands:

***IDN?** (query the instrument name, returns 'SAMD21')

***RST** (clears the GPIO to a low value, GPIO direction is output, and DAC set to a zero value)

**SENS1:VOLT?** (query the ADC's PA04 pin)

**GPIO1:LEV 0** (drive a low value to PA10)

**GPIO1:LEV 1** (drive a high value to PA10)

**GPIO1:LEV?** (query the level on PA10)

**GPIO1:DIR IN** (configure PA10 as an input)

**GPIO1:DIR OUT** (configure PA10 as an output)

**GPIO1:DIR?** (query the PA10 direction)

**SOURC1:VOLT:LEV 1.2** (drive the DAC pin PA02 to a value of 1.2V)

**SOURC1:VOLT:LEV?** (query the DAC pin PA02 voltage)

My C string parsing is very crude so the **SCPI** command **must match** what I have listed above (or be in lowercase).
All the major credit goes to the **tinyusb usbtmc author**, and my contribution was helping to find a bug in the code to allow the SAMD MCUs to properly run the example. 

The "test_tinyusb.py" **Python** file demonstrates all the **SCPI** commands.

![picture](https://media-cdn.seeedstudio.com/media/catalog/product/cache/b2267b506d4e4594666ef83a79896a9a/s/e/seeeduino-xiao-size-1.jpg)
