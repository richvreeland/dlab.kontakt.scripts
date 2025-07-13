```
ntet.ksp | a multisample ensembler
v1.00    | ©2023 dlab
```

Looking to stretch the utility of the libraries and patches you already have? Breathe weird life into your Kontakt instruments with ntet.

ntet is a quick and amusing way to add intrigue to an old instrument, whether it’s simulating additional harmonics, changing timbre and timing, or all of the above. It’s a pretty weird and nifty little sound design tool that is equally useful for effects as it is for re-contextualizing your favorite Kontakt patch and morphing it into something completely different.

It especially excels at manipulating simpler instruments that use multisampling.

---

## Installation

Please use the loose .nkp file. For legacy users (Kontakt 5), there is a version compiled with Kontakt 5.8.1 that should work in most Kontakt 5 versions.

**On Mac**
1. Place the .nkp file anywhere in `/~/Native Instruments/Kontakt/presets/Scripts/`. If using Kontakt 5 the folder will be `Kontakt 5` instead. The next time you open the application, it should show up in the load scripts window of the scripts tab in the Kontakt instrument backend.
2. You can use the script from either the front-end or back-end of the instrument. Load the script up from the backend of (almost) any Kontakt instrument and enjoy !

**On PC**
Same as above, except the folder paths will be different.

---

## Known Issues / Troubleshooting

**Common Setup Things**
- To use the Seek module, you need to either set your S.Mod values or your source engine to something other than DFD. If the seek amount is too high, nTet will simply play the sample at the beginning of the sample. This is a limitation of the scripting language.
- Set the Sample Range (found under the _General_ menu) to avoid triggering keyswitches, silent keys, undesirable sounds, fret noises, and whatever else irks you.
- Specifically when using the Neighborize module :
	- Sometimes issues with tuning can arise, because of other scripts loaded onto the instrument. While not always possible, you may be able to alleviate the problem by changing the load order of the script ... earlier in the load order is generally better.
	- Some note offs may be ignored until all notes have been released. This can be due to multiple keys trying to borrow the same sample, and is a limitation of the design.
- If things sound eerily quiet, the most common culprits are the settings in the Volume, Delay, Attack, and Seek modules. Delayed voices will not sound if you release the key before the desired delay time has been reached.

**General Weirdness**
	- ntet will not play nice with certain instruments/scripts. But with a little bit of love, it will work in most cases. Them's the breaks in Kontakt land!
	- Injecting scripts into pre-existing instruments is by its very nature somewhat experimental. When used with more complicated instruments that use multiple groups, release samples, etc., you may get some weird results!
	- This script can very quickly use up lots of voices, and you may hear artifacts if reach the instrument's limit. Of course, if your CPU allows, you could always add more voices ...

**Limitations**
	- Some instruments, such as the more recent ones by companies like Spitfire, have started locking users out of the backend and as a result cannot be edited to inject scripts :(
	- If you're using an instrument with a non-standard mapping (ie. samples only on white or black keys), you will likely experience silent playback and/or missing voices in certain instances.

---

## Features

### Ensemble Module
How many voices this script should generate every time you play a key. This is the flagship feature of ntet as you can create variations with each additional tone. The more the merrier!

---

### Volume Module
Controls the volume of each voice in the ensemble.

**Dry**
How loud the incoming notes you play should sound against the affected tones.

---

### Pitch Module
Controls the pitch (in semitones) of each voice in the ensemble. Values above zero will go upwards in pitch, and values below will do the opposite.

**Octaves +/-**
This changes the range of the pitch module's table in octaves. For instance, +/- 1 gives the table a 2 octave span.

**Musical Scale**
Changes the type of pitches that the pitch module will use. Found in the _Pitch_ menu.

**Spelling**
Whether the pitches in the table go above and below the root, or just one of those. Found in the _Pitch_ menu.

**Tame**
When enabled, reduces the volume of voices the further they are from the root pitch. This works well for instance when using a large number of octaves with the Harmonics scale.

---

### Detune Module
Controls the pitch (in cents) of each voice in the ensemble. Values above zero will go upwards in pitch, and values below will do the opposite.

---

### Pan Module
Controls the pan value of each voice in the ensemble. Below is left, above is right.

---

### Delay Module
Controls the onset timing of each ensemble voice.

---

### Neighborize Module
This module borrows neighboring samples and re-pitches them to the notes you're actually playing. This technique can radically alter the timbre of an instrument and opens up tons of possibilities.

This technique works best with multi-sample instruments.

**Above & Below**
Depending on how this menu is set, the module will either borrow only voices that are mapped to higher pitches, or lower pitches, or both.

---

### Seek Module
This module controls the sample start position of each voice. If the start position is too high a value, the voice's sample will simply start from the zero position.

---

### Attack Module
This module controls the amplitude attack time of each voice in the ensemble.

---

### Release Module
This module controls the amplitude release time of each voice in the ensemble.

---

### Shared Module Features

**Modes**
Many modules have a pulldown menu which features different types of modes, which manipulate the module's output in different ways. There are stationary modes, which don't change the table values but may change how they are interpeted. There are autopilot modes, in which the table's values are taken over and change in a destructive manner. Finally, there are destructive modes, which are functions that change the values of the table every time you press a key.

**Strength**
If the module has this setting, it will control the range of the module's output. More strength = a greater range of output.

---

### Settings

**Flux**
How much random fluctuation to introduce to the output of nTet. Does not generally affect modules that are in an autopilot mode.

**Seed**
Each seed is its own thoughtfully randomized preset.

**Sample Range**
the range of keys to use in borrowing samples. Be sure to set this to avoid keyswitches, silent keys, etc.

**Playable Range**
the range of keys that are affected by ntet. The rest pass through "dry", ie. won't be affected by the script.

**Tablefunk Module**
Accessible from the _Settings_ menu, allows you to destructively edit the table values using things like shapes and random functions.

**Presets**
Save, Load and Initialize presets from the contextual menu in the bottom left corner.

---

### Automation
It requires a few steps, but ntet does support automation for many of the parameters!

To enable parameter automation, after loading the ntet preset:
1. click the `edit 🔒` button in the bottom left hand corner.
2. You should see a script editor appear.
3. In the center of the editor's panel you should see a pulldown menu, `Apply from...` - select `...Editor/Patch` from this menu.
4. Now press the `Apply` button at the far right. 
5. Voila! ntet uses host parameters between 200 - 330 or so. This range should be high enough to avoid overlapping most of the pre-existing automation of the built-in scripting of commercial libraries, but we can't promise this will always be the case.

Kontakt scripts do not officially support automation for some types of UI (such as menus and tables), but we did the best we could to work around it. It may be a little janky !