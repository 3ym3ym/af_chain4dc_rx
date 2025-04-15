# af_chain4dc_rx
AF chain for DC receiver
This little project was created to complete the standalone direct conversion (DC) receiver. Other parts of the receiver are:
 - Main board (input filter, quadrature mixer, AF preamps, phasing SSB demodulator). Si5351A board from Adafruit (or Aliexpress clone) is attached to it.
 - Control board. Can be any microcontroller running the qudrature VFO code. I am currently using RP2040 SuperMini, 0.96" SSD1306 OLED display and 360PPI optical encoder.
The idea behind the whole project is to build a high performance SSB/CW receiver using only cheap parts readily available from Aliexpress or other similar sources.

Included files are the KiCAD project (schematic and PCB) which uses SMD footprints. It can be modified to use through hole footprints. All parts are available in TH variants.

The first stage is a simple CE amplifier, also used to set the bias point to the following filter stages. The gain (and the input impedance) is set by R15.

I picked the idea of the low-pass audio filter from Asshar Farhan, VU2ESE. The actual filter design was done using the online Filter Wizard tool from Analog Devices, then tweaked while simulating in LTSpice.The values in the schematic result in -3dB point about 2.0kHz. At 5kHz the attenuation is -50dB.

The final amplifier is a standard TDA2822 circuit, with a jumper to change the gain.

The circuit works down to 3V. I am using a cheap ME6209 LDO, which requires a good output bypass capacitor, otherwise there is a bit of ringing at the maximum volume (because of the feedback from the PA back to the input stage). 100uF aluminum plus 10uF ceramic capacitors is not an overkill.

ME6209 claims to tolerate up to 18V input, which I haven't tested. The dropout is small enough to use a single LiIon cell as the input power source, or 12V if that is what is available in the receiver.
