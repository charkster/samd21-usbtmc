# samd21-usbtmc
SAMD21's ADC, DAC and GPIO are controllable with custom SCPI commands. World's smallest lab equipment.
The seeeduino_xiao_usbtmc.uf2 file was created using the tinyusb usbtmc device example. I just made some minor changes to the main.c, usbtmc_app.c and usbtmc_app.h files to create this proof of concept. The DAC pin in PA02, ADC pin is PA04 and GPIO pin is PA10. A Seeeduino Xiao or Adafruit QT PY can be flashed with the included UF2 file and they should just work.
Here are the supported SCPI commands:
*IDN
*RST        (clears the GPIO to a low value and DAC to a zero value)
SENS1:VOLT? (to query the ADC's PA04 pin)
GPIO1:LEV 0 (to drive a low value to PA10)
GPIO1:LEV 1 (to drive a high value to PA10)
SOURC1:VOLT:LEV 1.2 (drive the DAC pin PA02 to a value of 1.2V)

The DAC has some sort of issue when the USB is activel. I have tried giving it a separate GLCK and enabled it while in sleep, but there is either something in the tinyusb code or a hardware bug in the SAMD which creates this issue. I saw online another person who was using the SAMD21 to send USB data to be output on the DAC and they had a similar issue. I have tried the DAC hardware register writes separate to the usbtmc example and it works just fine.

My C string parsing is very crude so the SCPI command must match what I have listed above (or be in lowercase).
All the major credit goes to the tinyusb usbtmc author, and my contribution was helping to find a bug in the code to allow the SAMD MCUs to properly run the example. 
