# BetaFPV Air 75 II (Matrix 1S II) VBAT/CBAT settings for Lava II 1S 480mah

These are just my CLI settings that feels good with reasonable callibration levels for batter drain. These are purposely set to nag you less when punching out a lot, but will still work for indoor gentle flights. Typically, the 480 mah Lava II 1S will sag about 0.2V in indoor flight and will sag up to about 0.5V when full throttle.

Voltage warning threshold settings:
```
vbat_max_cell_voltage = 435
vbat_full_cell_voltage = 405
vbat_min_cell_voltage = 337
vbat_warning_cell_voltage = 345
use_vbat_alerts = ON
vbat_duration_for_warning = 50
vbat_duration_for_critical = 25
```

This changes how your quad behaves. 100 = fully limit throttle to simulate 3.5V state
```
vbat_sag_compensation = 30
```

capacity settings
```
use_cbat_alerts = ON
```

capacity alert percentage, if you have a HV battery like I do but occasionally charge to 4.2V instead, I recommend setting this to the 4.2V equivalency limit difference which is about 15% less capacity than 4.35V charge, so 17 is a good number.
```
cbat_alert_percent = 10
```

ibata is the current callibration scale in mV/A. Default on the matrix II board is 750. Callibration approximated based on motor performance datasheets and amp reading outputs. To get yours without a multimeter, charge a fresh battery with no throttle limiter and then punch out and compare the max amp reading to your motor's datasheet multiplied by four and scale it in ratio across your existing setting.. The lower the number, the higher the new amp reading will take place and consequently the faster your capacity reading will tick over, in my case I'm aiming for 23.6A.
```
set ibata_scale = 570
```

The following feature is not functional yet (due to a betaflight persistant stat bug):
```
set battery_continue = ON
```
battery_continue basically is supposed to prompt you to continue your battery capacity reading form the previous flight, so whenever you disarm it saves the current capacity to memory, so when you power cycle and the new battery is less than `vbat_full_cell_voltage` it will prompt you to add the capacity from the previous flight onto the current one.
