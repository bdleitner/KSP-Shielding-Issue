# KSP-Shielding-Issue
Stores relevant files relating to reporting the [KSP issue](https://forum.kerbalspaceprogram.com/topic/225787-parts-incorrectly-marked-shielded-overwrites-manual-fixes/) with KSP deciding my parts are stowed.

# Craft Files

* `Sarnus Explorer.craft` - the main ship as it was originally launched, with the lander already attached. The lander was added as a subassembly and thus the root of that subtree is the lander's docking port.
* `Sarnus Explorer No Fairings.craft` - a modified version of the main ship to leave out the fairings and start without the lander.
* `Small Science Lander - LCH4.craft` - the lander as a separate craft. In this version the root is the remote guidance unit just under the docking port instead of the docking port itself.

# Experiments / Save Game Files

## Baseline

* `Baseline.sfs` - The starting point from where I originally noticed the problem.
* `Baseline Undocked.sfs` - The same as the starting point excpt I undocked the lander and backed it off a bit before saving.
* `initial shielded parts.txt` - A list of the parts that were shielded on the explorer in the undocked baseline.

## Simple Shielding Removal

* `Shielded Removed.sfs` - A modification of Baseline Undocked where all I did was recursively look through the nodes of the explorer and lander craft and replace all `shielded = True` properties within these `VESSEL`s with `shielded = False`.
* `Simple Undocked Save.sfs` - A save of the game after loading the `Shielded Removed.sfs`, testing that I could move the magnetometer, and then resaving.
* `Simple Redocked Save.sfs` - A save of the game the undocked version, but also redocking the lander.
* `simple undocked shielded parts.txt` - A list of parts on the explorer that were shielded again after the save. Some of these mae sense as there are still fairings in this version, 

All I did here was replace `shielded = True` with `shielded = False` everywhere I found it in thse two vessels. After loading the edited game, I could extend the magnetometer. I saved the undocked game, then docked and sved the docked game. Reloading the undocked game I could still extend it, and I could also extend it after docking but without the reload. But when I loaded the "redocked" game I got the "cannot deploy while stowed" error.

## Full Part Replacement

* `Part Replacement.sfs` - The edited save from this experiment.
* `Part Replacement Undocked Save.sfs` - A resave after loading the edit prior to redocking.
* `Part Replacement Docked Save.sfs` - A resave after loading the edit and then docking the lander.
* `parts replaced initial shielded parts.txt` - A list of the parts that showed up as shielded when doing the initial replace.
* `parts replaced undocked shielded parts.txt` - a list of the parts, by index and name, that had `shielded = True` on the explorer when the undocked save was made. 
* `parts replaced docked shielded parts.txt` - a list of the parts, by index and name, that had `shielded = True` on the explorer when the docked save was made. Note that no parts on the lander were shielded when the game was saved undocked, but when docked the number of shielded parts went from 46 to 65, so 19 parts (out of 43) on the lander became shielded.

This was the most aggressive edit. I created new versions of the crafts (the "No Fairings" and separate lander ones, referenced above). I then created saved games with each on the landing pad and ran code that took the list of parts from each and replaced the part lists from the vessels in the `Baseline Undocked` save with the parts list from the launchpad. In these new crafts all fairings were removed from the explorer and the lander was modified so the docking port was not the root.  There was also a small difference in that the magnetometer, while still attached to the same parent part (the science lab) was in the location I'd originally planned for it. I'd moved earlier after encountering this (or a similar) stowage issue and thought it might have just been cramped.

For this run, after loading the edit I was again able to extend and retract the dock, including after saving and reloading the `Part Replacement Undocked Save` file. But in a deviation from the prior experiment, this time I was unable to extended the magnetometer after docking even without the save/reload cycle.

