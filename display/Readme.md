Disclaimer:
I only describe my findings here and cannot held responsible for damages you may do to your hardware!
You may have a different hardware revision or another board which just looks similar.
My Geeetech A30 came with GTM32 PRO VD board, the menu says hardware revision 3.5.
There is the similar looking GTM32 PRO VB in the wild, so doublecheck! A continuity tester is your friend.


My Geeetech A30 came with a 3.2" touch TFT LCD (about page says Hardware rev. 3.5 yours may be differen)
I think it is a flavour of this one:
http://www.geeetech.com/wiki/index.php/3.2TFT_LCD
with custom firmware preinstalled.



The display communicates via serial connection with the board. It sends common Gcodes as well as custom Gcodes. The original smartto firmware on the board sends different messages to the display to update its status, send SD-filelist etc.

The goal is to make marlin able to talk to the display via extensible-ui. So you can use marlin without changing the display or reprogram it with a new firmware.


To "intercept" communication between board and lcd i connected to the board and the lcd with a USB2Serial plug to send and receive commands via terminal program.

MAKE SHURE THE USB2SER CONVERTER IS CONFIGURED/JUMPERED TO 3.3V !
baudrate seems to be hardcoded to 115200
If you can't connect try to interchange RX and TX.
RX on the board/LCD has to connect to TX on the USB2Ser, TX on the board/LCD goes to RX on the USB2Ser.


In this first step I tried to find out all messages send from the LCD on button pushes, value changes etc.

  +------+      +---------+      +-----+
  | COM1 |<---->| USB2Ser |<---->| LCD |
  +------+      +---------+      +-----+



I then connected the board via USB and connected the display-interface to another USB port via USB2Serial plug.
The board is supplied with 5V via connector S1(see pictures or schematics)

  +------+      +-------+      +---------------------+      +------+
  | COM1 |<---->| GTM32 |<---->| USB2Ser on LCD_CONN |<---->| COM2 |
  +------+      +-------+      +---------------------+      +------+

This made me able to see what is send in a more production-like situation.

I tried to assemble an overview of what is sent on different events.
In raw are all logs of the communication I recorded.
setup contains some pictures of my setup described above.

I'm shure I still didn't cover all situations yet, so consider this a work in progress.

