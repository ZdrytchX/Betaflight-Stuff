# Betaflight CLI example for VTX power level using Smart Audio on BetaFPV Matrix 1S II board
A lot of people are stumped on how to do this and a lot of people run with like 5 power levels, so uh, here you go!  
```
vtx 0 5 0 0 0 900 1100
vtx 1 5 0 0 1 1100 1350
vtx 2 5 0 0 2 1350 1600
vtx 3 5 0 0 3 1600 1800
vtx 4 5 0 0 4 1800 2100
```
Few important things to note: These take up vtx index 0 to 4 (first number), so you may need to change that as required. This first index number doesn't actually matter and can be anything between 0 to 9.  
The important thing is that the second number (here listed as aux index `5` which corresponds to Aux channel 6) is your aux channel used to set the power level. Check your receivers tab, and adjust your VTX switch/potentiometer.  
The middle two numbers refer to frequency band (e.g. raceband) and channel respectively. You generally don't want to touch the first one but the second could be useful at race events to quickly switch channel, in any case leaving them as `0` will mean "use existing setting."
The fifth number is the VTX power level, preconfigurable in betaflight configurator supposidly, not that I've tried. If you are using a vtx with a lot of power levels while having ELRS set to hybrid instead of wide mode, you should use aux 8 (index `7` as it counts from 0), due to optimisation limitations of how [expresslrs](https://www.expresslrs.org/software/switch-config/#summary-of-switch-configuration-modes) works but for most people, the 6 position switch limitation is good enough as most VTXs have 6 or less power levels, in my case, there are 4 (index 1-4) + PIT mode (index 0).  
Lastly, the last two numbers are your switches states between 988 and 2012 (basically 1500 +/- 512 as double that, 1024 is 10bit resolution) but people push to 900/2100 because technically ELRS supports extended range past this.
If you run `vtxtable` you can check the configuration you have available:
```
vtxtable powerlevels 5
vtxtable powervalues 1 2 3 4 0
vtxtable powerlabels 25 100 200 400 PIT
```

One final side note, there's currently an issue with Matrix 1S II board firmwares that prevents them from setting up a custom VTX power level after arming or saving to memory. No clue when/if this will get fixed.
