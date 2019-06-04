My Geeetech A30 came with a 3.2" touch TFT LCD (my printer says Hardware rev. 3.5 your Situation may be differen)
I think it is a flavour of this one:
http://www.geeetech.com/wiki/index.php/3.2TFT_LCD
with custom firmware preinstalled.

The display communicates via serial connection with the board. It sends common Gcodes as well as custom Gcodes. The original smartto firmware on the board sends different messages to the display to update its status, send SD-filelist etc.

The goal is to make marlin able to talk to the display via extensible-ui. So you can use marlin without changing the display or reprogram it with a new firmware.


To "intercept" communication between board and lcd i connected to the lcd with a USB2Serial plug to send and receive commands via terminal program.

  +---------+      +-----+
  | USB2Ser |<---->| LCD |
  +---------+      +-----+

In this first step I tried to find out all messages send from the LCD on button pushes, value changes etc.



I then connected the board via USB2Ser and connecting the display-interface to another USB2Ser.

  +---------+      +-------+      +---------------------+
  | USB2Ser |<---->| GTM32 |<---->| USB2Ser on LCD_CONN |
  +---------+      +-------+      +---------------------+

This made me able to see what is send in a more production-like situation.
In raw are all logs of the communication I recorded.

I'm shure I still didn't cover all situations yet, so consider this a work in progress.

