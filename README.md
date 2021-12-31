# Flirc LED Strip Party

This repository contains a shell script for changing the colors of an LED strip
(LnLED brand in this case, but I am pretty sure all of the cheap LED strips use
the same generic IR remote and so the same commands will work for all of them).

The colors are changed in random order between red, green, blue and white. The
remote contains more colors, but for a proof of concept, I have not recorded all
of them yet.

To kill the script, kill the terminal it runs in. I have not added any sleep
delay so the script will not respond to Ctrl+C fast enough to clean up and end
itself most of the time.

## To-Do

### Record all of the buttons on the remote

### Decode the IR protocol and see if R, G, B and W can be precision-tweaked

### Attach a video of the proof of concept in action
