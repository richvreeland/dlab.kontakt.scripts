```
panoram.ksp | a novelty panner
v1.00       | ©2025 dlab
```

panoram is dedicated to novel panning techniques. You can stage your panning as if it were instruments on a stage, as well as having different algorithms for the panning of individual voices. Hocketing, mapping different keys to different positions, moving with velocity ... using this script, these can all be accomplished with ease. You can also send the generated data to Kontakt's source engine, for further use.

# Installation

Please use the loose .nkp file. This script was compiled for Kontakt 7. If there is enough demand, support for legacy versions may come in the future.

## On Mac

1. Place the .nkp file anywhere in `/~/Native Instruments/Kontakt 7/presets/Scripts/`. The next time you open the application, it should show up in the load scripts window of the scripts tab in the Kontakt instrument backend.
2. You can use the script from either the front-end or back-end of the instrument. Load the script up from the backend of (almost) any Kontakt instrument and enjoy !

## On PC

Same as above, except the folder paths will be different.

# Known Issues / Troubleshooting

- Injecting scripts into pre-existing instruments is by its very nature somewhat experimental. When used with more complicated instruments that use multiple groups, release samples, etc., you may get some weird results!
- Some instruments, such as the more recent commercial offerings have started locking users out of the backend and as a result cannot be edited to inject scripts :(

# Features

## Locations

The number of pan positions this script will use. At 1, everything is centered, 2 is hard left or right, and so forth.

## Mode

Each incoming note will be played at the appropriate pan location. Depending on the mode, that means:

### Hocket L2R / R2L

Notes are played at the next available pan location, moving left to right (or vice versa).

### Pitch L2R / R2L

Notes are mapped to the pan locations, based on their pitch, where lowest pitch would be leftmost location, and highest pitch would be rightmost (or vice versa). Use the range button to set your pitch range.

### Velocity L2R / R2L

Notes are mapped to the pan locations, based on their velocity, where lowest velocity would be leftmost location, and highest 
velocity would be rightmost (or vice versa). Use the range button to set your velocity range.

### Fate of Keys

Each key is always panned deterministically to the same location. Use the seed control to change where they go.

### Fate of Velo

Each velocity performance is always panned deterministically to the same location. Use the seed control to change where they go.

### Fate of Both

Each specific key and velocity combo performance is always panned deterministically to the same location (ie. C3 at velocity 60). Use the seed control to change where they go.

### Flux (Mode)

Each key is panned to a random location.

## Tilt

This will the tilt the stereo field left or right.

## Width

The width of the stereo field to use for the pan effect.

## Flux

Adds some randomness to the pan position output. 100% flux is completely random panning.

## Amp Tilt

This will skew volume of the sound stage from left to right, to mimic distance.

## Send ID

Which `From Script` ID to use to send generated data to Kontakt's source engine, for use in other contexts. `-1` is off.

## Automation

It requires a few steps, but this script does support automation for many of the parameters!

To enable parameter automation, after loading the script:
1. click the `edit 🔒` button in the bottom left hand corner.
2. You should see a script editor appear.
3. In the center of the editor's panel you should see a pulldown menu, `Apply from...` - select `...Editor/Patch` from this menu.
4. Now press the `Apply` button at the far right. 
5. Voila! This script uses host parameters starting at `0800`. This range should be high enough to avoid overlapping most of the pre-existing automation of the built-in scripting of commercial libraries, but of course we can't promise this will always be the case.

Kontakt scripts do not officially support automation for some types of UI (such as menus and tables), but we did the best we could to work around it. It may be a little janky!