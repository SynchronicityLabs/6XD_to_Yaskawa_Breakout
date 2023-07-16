# 6XD_to_Yaskawa_Breakout
Board to streamline connection between a Duet3D 6XD and Yaskawa Sigma-7 SGD7S drives

This project is a PCB breakout board designed for connecting Yaskawa servo drives to Duet3D control boards.  Specifically, it was developed to simplify connection between a Duet 3 6XD board and a pair of Yaskawa Sigma-7 SGD7S-****00A series servo drives—i.e., step/dir-capable drives.  Yaskawa drives are extremely common in industry and can be found on the used market.

**The board serves the following functions:**
-	Correct voltage mismatch in Step/Direction signal.  The 6XD drives these signals at 5V, the SGD7S wants 3.3V
-	Allow enabling “Servo On” from the 6XD’s Dx_EN(-) pin.  The SGD7S uses a 24V enable signal which the 6XD enable pins cannot drive directly.
-	Allow SGD7S alarm trigger to be received by the 6XD’s Dx_ERR pin.  Direct connection would overload the 6XD or SGD7S.
-	Combines the torque-limit enable for forward and reverse (these are 2 separate inputs) and from both drives, to allow a single optoisolated output to trigger torque limiting for both drives, in both directions (e.g., during homing or moves prior to homing)
-	Combines the alarm reset signal for both drives
-	Combines the P-control enable signal for both drives
-	Provides a jumper to select output two between P-Control and an assignable/open pin
-	Provides one currently-unassigned output breakout

**Do I need this to connect to a SGD7S servo drive?**
    No.  None of the connections made on the board are particularly bulky or complex; the necessary components could be joined directly into the wiring between the 6XD and SGD7S’s CN1 connector if preferred.

**Could I use this to connect a 1XD or other Duet board to a SGD7S drive?**
  Not recommended.  Other boards could be used, but not with the circuitry on this breakout board.  While it may seem that the 1XD would be a simple stand-in for the 6XD, it cannot directly handle the step/dir signal current for the SGD7S and would need line drivers or similar.  Additionally, it cannot directly interface with the necessary inputs via IO pins (though OUT_0 and OUT_1 could), as the 6XD’s optoisolated outputs can.

**What if I want to connect more than two drives?**
    You could use multiple breakout boards (up to three) on a 6XD.  However, you may need to ration your optoisolated outputs.  The 6XD has four, with current limits of 50mA.  Additionally, each alarm-reset, P-Control, and torque-limit input takes 5mA.  So, six drives is not a problem for parallel outputs in most cases, however torque-limit signals from a single output would be maxed out at 5 drives. 

**Where do I find you if I blow up my drives/Duet?**
    You don’t, this currently beta-version at best.  The SGD7S manual is nearly 650 pages.  I’ve tried to make it simple here, but it isn’t.  Your drive connections are at your own risk.

**Can it interface to drives other than the SGD7S drives?**
    Probably.  Good luck, we all believe in you.
