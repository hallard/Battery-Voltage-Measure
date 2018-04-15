# Battery Voltage monitor with no current drain breakout board

Based on previous couple of [voltage divider break out](https://github.com/hallard/R-Divider-Breakout) for ADS1015 ADC board, I needed a simple board being agble to measure battery voltage without draining battery current.
For this I created this little basic board. It's just a basic resistor divider whith a mosfet to enable the measure so it does not drain any current from battery when not enabled. Measure is done using a analog entry of the micro controller (arduino, STM32, ESP8266, ESP32, ...)

## Detailed Description

You only need 3 or 4 wires depending on what you need to achieve

- VBat (connected to + of the battery)
- GND  (connected to - of the battery)
- AN is the analog entry to measure voltage 
- EN is the enable pin

To enable the divider to work, you need to set the EN pin to 0. Leaving this pin floating will disable the divider since there is a pullup on the transistor gate.

Take care of the max voltage value of your analog input pin, some have limited value (IE ESP8266)

Voltage on analog pin (when enabled) is VBat * ( R2 / (R1 + R2) ), so with R1=10K and R2=10K voltage is VBat * 0.5. So 4.2V VBat means 2.1V on analog pin. In this case, with 3.3V devices, it can go up to 6.6V
If you need to divide more increase top resistor value example R1=20K, R2=10K you can go up to 9.9V.
Check Voltage Divider online calculator like this [one][10] or this [one][11] if needed

If you don't want to use enable pin, put some solder paste on JP1 to short the pasd, leave Q1 and R3 unpopulated and you have a basic divider. 
In this case to avoid battery drain (that will occurs every time), increase resistors values (470K + 470K for example)

## Schematic

![schematic](https://raw.githubusercontent.com/hallard/Battery-Voltage-Measure/master/pictures/Battery-Voltage-Measure-zoom-sch.png)  

Q1 can be any SOT23 P-Mosfet so BSS84, BS250, ... are fine. Resistors are 0805 package.

## Boards 

<img src="https://raw.githubusercontent.com/hallard/Battery-Voltage-Measure/master/pictures/Battery-Voltage-Measure-top.png" alt="Top">&nbsp;&nbsp;<img src="https://raw.githubusercontent.com/hallard/Battery-Voltage-Measure/master/pictures/Battery-Voltage-Measure-bot.png" alt="Bottom">


You can order the PCB of this board at [PCBs.io][3]. PCBs.io give me some reward when you order my designed boards from their site. This is pretty good, because I can use these rewards to create and design new boards and order them for free, so if you don't care about PCB manufacturer please use [PCBs.io][3].

## License

You can do whatever you like with this design.

## Misc

See news and other projects on my [blog][2] 
 
[2]: https://hallard.me
[3]: https://PCBs.io/share/zjqg5 
[10]: http://www.ohmslawcalculator.com/voltage-divider-calculator
[11]: http://www.ti.com/download/kbase/volt/volt_div3.htm
