# 6XD_to_Yaskawa_Breakout

![Model](/Images/6XD-SGD7S-Breakout.png)

This is a PCB breakout board designed for connecting Yaskawa servo drives to Duet3D control boards.  Specifically, it was developed to simplify connection between a Duet 3 6XD board and a pair of Yaskawa Sigma-7 SGD7S-****00A series servo drives—i.e., step/dir-capable drives.  These drives range from 50W to 15kW, with the 50W to 400W versions (10-400W motors) being available in 100VAC or 200VAC single-phase.

This should currently be considered in alpha!  Use at your own risk!

## The board serves the following functions:
-	Correct voltage mismatch in Step/Direction signal.  The 6XD drives these signals at 5V, the SGD7S wants 3.3V
-	Allow enabling “Servo On” from the 6XD’s Dx_EN(-) pin.  The SGD7S uses a 24V enable signal which the 6XD enable pins cannot drive directly.  Set 6XD's enable jumper to "active disable".
-	Combines the torque-limit enable for forward and reverse (these are 2 separate inputs) and from both drives, to allow a single optoisolated output to trigger torque limiting for both drives, in both directions (e.g., during homing or moves prior to homing).
-	Combine the alarm reset signal for both drives to use a single optoisolated output
-	Combine the P-control enable signal for both drives to use a single optoisolated output
-	Provide a jumper to select two outputs between P-Control and two open terminal block connect (i.e., you can connect 2 of the 3)
- Block terminals and jumper allow reconfiguration of various inputs/outputs from default if desired.

### Do I need this to connect to a SGD7S servo drive?
No.  None of the connections made on the board are particularly bulky or complex; the necessary components could be joined directly into the wiring between the 6XD and SGD7S’s CN1 connector if preferred.

### Could I use this to connect a 1XD or other Duet board to a SGD7S drive?
Not recommended.  Other boards could be used, but not with the circuitry on this breakout board.  While it may seem that the 1XD would be a simple stand-in for the 6XD, it cannot directly handle the step/dir signal current for the SGD7S and would need line-driver type setup. Additionally, it cannot directly interface with the necessary inputs via IO pins (though OUT_0 and OUT_1 could), as the 6XD’s optoisolated outputs can.

### What if I want to connect more than two drives?
You could use multiple breakout boards (up to three) on a 6XD.  The opto-isolated outputs could be daisy-chained, however, you may need to ration them carefully.  The 6XD has four, with current limits of 50mA.  Each alarm-reset, P-Control, and torque-limit input takes 5mA.  So, six drives is not a problem for parallel outputs in most cases, however torque-limit signals from a single output would be maxed out at 5 drives. 

### Where do I find you if I blow up my drives/Duet?
You don’t, this is currently beta-version at best.  The SGD7S manual is nearly 650 pages.  I’ve tried to make it simple here, but it isn’t.  Your drive connections are at your own risk.

### Can it interface to drives other than the SGD7S drives?
Probably.  Good luck, we all believe in you.
