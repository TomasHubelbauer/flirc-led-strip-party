# Flirc LED Strip Party

This repository contains a shell script for changing the colors of an LED strip
using a Flirc USB transceiver device.

[Flirc USB](https://flirc.tv/more/flirc-usb)

The LED strip I am using is an LnLED brand, but I am pretty sure all cheap IR
controlled LED strips use the same generic remote, so this should work with all
of them.

Flirc provides both a GUI program and a CLI tool for recording and replaying IR
commands. I have captured the commands of the remote using the device log found
in the Flirc GUI. Go to File > Device Log and check Enable IR Debugging.

Pressing a key results into multiple lines being written into the device log.
The IR command is the line with numbers separated by commas starting with zero.

Replaying the key is done by using the Flirc CLI and its `sendir` command. It
takes a `--pattern` argument whose value should be set to the capture sequence.

The script cycles the colors I have decoded so far (red, green, blue and white)
in the quickest possible succession. Which is not very quick.

To run the script the first time, remember to first run `chmod +x party.sh`. To
run the script, run `./party.sh`. Ensure Flirc GUI is closed before running the
script as the device can only be used by the GUI or the CLI exclusively, not at
the same time.

To kill the script, kill the terminal window running it. Ctrl+C will be caught
by `flirc_util` but due to the lack of delay between the invocations, it does
not seem to kill it fast enough.

## Non-Color Codes

```sh
# on
0,9376,4440,640,478,636,478,641,478,636,478,640,478,636,482,636,478,636,483,636,1586,641,1586,640,1598,629,1587,640,480,634,1586,641,1586,641,1586,641,1587,640,1587,636,478,640,478,636,478,636,478,644,475,636,478,636,478,640,478,636,1587,640,1586,641,1586,643,1584,641,1586,641,1586,636
# off
0,9358,4445,632,482,636,478,637,478,636,478,636,478,636,478,636,478,636,478,636,1591,636,1587,636,1591,632,1590,655,459,636,1587,636,1591,632,1590,636,478,636,1586,636,478,636,478,636,478,636,478,636,478,632,482,632,1591,636,479,631,1591,636,1587,636,1591,632,1590,637,1586,636,1586,637
# light+
0,9391,4415,666,450,665,451,641,474,675,439,667,451,641,474,666,448,641,478,666,1556,681,1546,645,1583,666,1561,666,448,667,1560,667,1556,671,15
# light-
0,9394,4415,664,452,640,473,667,447,645,473,667,447,640,478,640,474,666,448,644,1582,666,1560,667,1555,671,1555,645,474,640,1582,644,1582,666,1560,667,1555,645,474,640,473,667,447,666,448,666,452,640,474,666,447,667,447,666,1555,671,1555,667,1559,666,1555,671,1555,666,1560,666,1556,671
# flash
0,9400,4414,666,452,641,473,667,451,637,477,667,511,581,474,666,452,641,473,667,1560,666,1579,648,1560,666,1561,666,452,667,1555,671,1556,671,1556,671,1556,644,1597,630,474,667,1560,666,452,640,474,667,447,640,478,667,447,667,452,666,1556,671,447,667,1560,666,1560,667,1556,671,1555,671
# strobe
0,9380,4440,641,478,641,473,641,478,640,474,640,478,641,473,641,478,640,474,640,1586,641,1586,641,1586,641,1586,645,474,640,1586,646,1581,641,1586,640,1587,640,1586,641,1586,641,1586,645,474,640,474,645,473,641,473,645,474,640,478,641,473,641,477,641,1586,641,1586,640,1587,640,1587,644
# fade
0,9385,4445,636,478,640,478,641,478,640,478,641,478,640,478,614,504,636,478,641,1586,614,1617,640,1586,641,1591,636,478,640,1587,644,1578,640,1587,640,1587,636,1591,636,478,610,504,640,1591,614,504,637,477,641,478,614,504,619,500,644,1587,640,1587,640,478,641,1586,645,1586,640,1587,640
# smooth
0,9388,4440,641,478,640,473,641,478,640,474,640,478,641,473,641,477,641,473,641,1586,640,1586,641,1586,640,1586,640,474,640,1586,641,1586,640,1586,641,1586,640,1587,640,1582,641,477,641,1582,640,478,640,474,641,473,641,478,636,478,640,474,640,1587,640,474,640,1587,640,1586,641,1582,640
```

## Code Accuracy

The codes will vary slightly between presses, presumably due to the noise in the
environment between the IR transmitter in the remote and the IR receiver in the
Flirc USB device.

There seems to be tolerance for this in the LED strip receiver logic. Individual
numbers of the code seem to vary by as much as a few dozen between presses and
that's with the remote 5 cm away from the Flirc. I would not be surprised to see
the LED strip IR receiver accept numbers in the sequence that vary by a hundred
or more.

Presumably the most important aspect of the code is the relative difference
between the numbers and their order of magnitude. I might play around with
seeing how far I can go with changing the code and still have it decode to the
same action by the LED strip.

## To-Do

### Decode the IR protocol and see if R, G, B and W can be precision-tweaked

### Attach a video of the proof of concept in action

### Chart the codes to see relative differences between the numbers

This should help decode the IR protocol between the remote and the LED strip.

### Investigate how imprecise the sequence can be before rejected or misdecoded
 