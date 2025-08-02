These are my prusaslicer configs for my printer, which includes the start/toolchange/end gcode which will do a few things:
- Start by moving from home to a "midway" point over the purge bin (PURGE_POS_X, PURGE_POS_Y, PURGE_POS_HIGH_Z)
- Move down to the purge bin
- Prime the first extruder into the bucket for the brush holder
- Run both heads through the brush to clean off any leftover filament that was leaking.
- When switching filaments it does:
  - Move to the purge tower so that any "leak" from the last active toolhead goes into the purge tower
  - Cool the last active toolhead while warming the next active toolhead
  - Move to the X/Y of the purge bucket
  - Move to the Z of the puge bucket (e.g. it lowers the toolhead at the front of the bed, so don't put tall prints there)
  - Rub off any leaks in the brushes
  - Raise back up to the current layer height
  - Purge into the purge tower with the now active head
  - And finally move onto the next layer
- When changing to the second filament for the first time, it will heat and prime the second extruder in the brush bin, and run over the brush again, at the end of the first tool change.

The variables at the top of the start g-code can be configured if you want to put a brush/purge bin somewhere else (but don't forget to update the template gcode if you move the brush).

It's a bit tricky how it works because it relies on the layer number/starting toolhead to figure out how to put stuff together.

Note that I typically put my support material in the right extruder (`T1` in the gcode), I don't remember if I made it so it'd work with support in the left extruder (`T0`), but I see no reason why that wouldn't.

I tried to set it up so that you can also print with only the left or right extruder, and it will only pre-heat/prime the extruder in use.

I included my print profiles, but they could probably use some work, so use them or don't (they work well for matterhackers PETG, I never bothered tuning the PLA one because I only use PLA as a support material, and the TPU one is leftover from when I was using the single extruder).

I also attached F3D and step files for the brush holder, but it does not quite fit on the bed (the screw hole doesn't line up right, but it works if you just kinda wedge it in). I had always planned to come back and modify it to fit better, but never did. It uses one of the wire brushes you can get off amazon (like [this one](https://www.amazon.com/Aokin-Printer-Nozzle-Cleaning-Toothbrush/dp/B0B1ZWG9CG/)), just cut the head off and then feed some filament through the holes (and between the bristles) to hold it in place.
