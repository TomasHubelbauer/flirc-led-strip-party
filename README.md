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

## To-Do

### Record all of the buttons on the remote

### Decode the IR protocol and see if R, G, B and W can be precision-tweaked

### Attach a video of the proof of concept in action
