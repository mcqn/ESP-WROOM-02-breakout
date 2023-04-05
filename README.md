# ESP-WROOM-02-breakout

Very simple breakout PCB for the [ESP-WROOM-02](http://espressif.com/en/products/hardware/esp-wroom-02/resources) ESP8266 module.

## Programming

The esptool.py documentation, particularly from the [section on Serial Connections onwards](https://github.com/themadinventor/esptool/#serial-connections) is a useful reference when getting started with programming.

### Wiring

 * Tie the EN (chip enable) high, to 3V3
 * Connect a 3.3V serial-to-USB adapter to GND, TX and RX
 * Tie GPIO0 to GND so it enters serial bootloader mode on startup/reset
 * Pull GPIO15 to GND, preferably with a resistor
 * Pull GPIO2 to 3V3, with a resistor (e.g. 10k)

For easier operation, wire pushbuttons between GPIO0 and GND (rather than tieing it permanently) and Reset and GND.  That allows you to reset the module by pushing the button connected to the Reset line, and put it into serial bootloader mode by holding the GPIO0 pushbutton while pressing the reset button.

### Initial Checks

Once wired up, if you open a serial monitor at the rather odd baud rate of 74880 you'll see some output when the module first powers up (or after a reset).

If you see random garbage data then the baud rate is most likely wrong.  Many serial monitors (including `screen` on Linux) won't recognise the non-standard baud rate of 74880.  If you've got `pyserial` installed (e.g. if you've installed `esptool.py`) then you can use `miniterm.py`.

#### Boot Mode

The output at the odd baud rate will include a message `boot mode:(3,6)` or similar.  The numbers indicate how it's booted up.

The first digit indicates whether or not it's in programming mode.  `3` indicates normal boot, and `1` shows that it's ready for programming over serial.

### Programming With the Arduino IDE

 1. Install the latest version of the Arduino IDE - [https://www.arduino.cc/en/Main/Software](https://www.arduino.cc/en/Main/Software)
 1. Run the Arduino IDE and follow the instructions in [Sparkfun's Thing Guide](https://learn.sparkfun.com/tutorials/esp8266-thing-hookup-guide/installing-the-esp8266-arduino-addon) to install the add-on for the ESP8266.
 1. Put the module into serial bootloader mode
 1. Choose the "Generic ESP8266 Module" board in the `Tools -> Board` menu in the Arduino IDE
 1. Set the `Flash Mode` to `QIO`, `Flash Frequency` to `40MHz`, `Upload Using` to `Serial`, `CPU Frequency` to `80MHz`, `Flash Size` to `2M (1M SPIFFS)`, `Reset Method` to `ck` and `Upload Speed` to `115200`
 1. Choose the right serial port in the `Tools -> Port` menu
 1. Upload the code

