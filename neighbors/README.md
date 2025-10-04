```
neighbors.ksp | a borrowing resampler
v1.00         | ©2025 dlab
```

Neighbors opens up a wealth of timbral options for your old multi-sample instrument. Have you ever transposed the MIDI going into your sampler up some number of semitones, and then pitched the audio down by the same amount? This script essentially recreates that timbral shifting effect, but with many more options. By intelligently playing neighboring samples instead of the samples that are assigned to each key you play by default, Neighbors allows you to dramatically change the sound of your old sampler patches.

# Installation

Please use the loose .nkp file. This script was compiled for Kontakt v7.10.7. If there is enough demand, support for legacy versions may come in the future.

## On Mac

1. Place the .nkp file anywhere in `/~/Native Instruments/Kontakt 7/presets/Scripts/`. The next time you open the application, it should show up in the load scripts window of the scripts tab in the Kontakt instrument backend.
2. You can use the script from either the front-end or back-end of the instrument. Load the script up from the backend of (almost) any Kontakt instrument and enjoy!

## On PC

Same as above, except the folder paths will be different.

# Known Issues / Troubleshooting

- Injecting scripts into pre-existing instruments is by its very nature somewhat experimental. When used with more complicated instruments that use multiple groups, release samples, etc., you may get some weird results!

- Some instruments, such as the more recent commercial offerings have started locking users out of the backend and as a result cannot be edited to inject scripts :(

- If you're using an instrument with a non-standard mapping (ie. samples only on white or black keys), you will likely experience silent playback and/or missing voices in certain instances.

# Features

## Global Controls

The **Mode** menu allows you to switch between the script's main operational modes. You can choose from `Setup`, `Tile`, `Honky Tonk`, `Shift`, or `Patterns` to tailor the behavior of the instrument to your needs.

The **HUD** is your central display for incoming note information, helping you monitor how the script is interacting with your input.

You’ll also find a **Bypass** button to quickly disable the script if needed.

## Setup Mode

Define the range of your sample map by using the **Map Lo** and **Map Hi** parameters to set the lowest and highest notes, respectively, ensuring that the instrument responds within your desired range. Be sure to set this to avoid keyswitches, silent keys, etc.

## Tile Mode

Limit your sample borrowing to a single sample, regardless of what you play. The **Location** knob lets you specify which part of the sample map to focus on.

## Mode > Honky Tonk

Simulate wear and tear the way you might hear it on an old piano by deterministically adding effects, borrowing samples, tripling and detuning "strings", messing with attacks and letting notes decay early. Some keys may be missing a "string" or two, just like an old piano!

### Age

As age is increased, the script borrows samples from further away, increases detuning, and adds chorusing by adding up to 2 extra voices. It also adds the likelihood of notes having softer attacks, ending prematurely, or getting stuck and playing a bit longer. The effect of this is not unlike preparing a piano.

### Model

Changes the deterministic set of data that each key uses to generate its sound. Sort of like trying a different model of the same instrument.

### Randomize

Will randomly pick an age and a model.

## Mode > Shift

Shift mode simply lets you adjust the **Timbre** uniformly of all incoming samples. It can effectively turn a guitar into a harpsichord, or a brittle sounding piano into a lofi treat. Go down a few octaves and the sound gets very dark and muddy with long decays, because it's borrowing from near the top of your instrument's sample range and pitching those samples back down. Go up a few octaves and the sound will typically get very thin and bright with short decays, as it's doing the opposite.

Try **Advanced** mode to reveal a very powerful ensembler (exposed by default in **Patterns** mode).

## Mode > Patterns

Builds upon what **Shift** can do, and offers more control over how the sample borrowing algorithm can work.

This mode offers a variety of ways in which to change sample borrowing over time, in predictable sequences.

`Walk` moves across the sample range in a consistent size increment controlled with the `Gait` parameter, before repeating with the `Limit` setting.

`Seeded Walk` uses the `Model #`'s random generation to deterministically choose samples to borrow in a repeatable sequence. Meanwhile, `Velocity Map` effectively allows you to let the timbre of your instrument change dramatically depending on how loud or quietly you play. Finally `Pitch Map` lets you do things like "flip" the sample range. It allows you to alter the pitch to sample relationship in an algorithmic way as you move across the keyboard. So instead of having the sample borrowing go from low to high alongside pitch (which is the traditional method), you can have it go low to random, or from high to the most recently played note. These are a bit esoteric for sure, but fun to experiment with !

## Mode > Shift/Patterns (Shared)

### Staging Panel

The **Mix** knob lets you control the balance between dry and wet signals, while the **Voices** knob determines how many voices play per key. You can also use **Delay** here to add up to 2000ms of pre-delay to the wet signal, perfect for creating interesting relationships between dry and wet.

The **Timbre** knob allows you to offset the sample borrowing in semitones, while **Map Size** adjusts the percentage of the sample map to use.

### Differentiate Panel

This panel allows you to control how the **Fate** system works, by constraining how the random generation is grouped. For instance, differentiating by **Roots** gives you a different "fate" for each key regardless of octave, so all C's have the same effect, as do all C#'s, and so forth. **Voices Only** will apply the same fate to every key, but each voice is different (ie. having more than one voice play the same key, each has a different fate). All other Differentiate Modes build upon this behavior. Differentiating by **Semitones** gives you the behavior of **Honky Tonk** mode, which also gives a different reproducible effect (fate) to each key across the entire keyboard. The **Model #** is the base seed for generation, so changing this will essentially "re-roll" the fate of every key.

### Fate Panel

In case we didn't hammer it home, Fate is our spin on traditional "humanization", but in a way that is deterministic and reproducible. The text heading mutates alongside the changes in determinism, to help communicate when fate has changed. This panel introduces parameters that control the upper limits of the script’s effects. With **Distance**, you can specify the maximum borrowing distance as a percentage, while **Detune** sets the +/- limit for pitch detuning, in cents. Similarly, **Delay** determines the maximum playback delay for each "wet" voice, up to 2000ms.

### Flux Panel

The Flux panel lets you humanize the performance of each note without the determinism. In other words, good old-fashioned randomness. **Shift** adds variability to sample borrowing distances, while **Detune** and **Delay** do the same for pitch and timing, respectively. These all operate within maximum ranges determined by the **Fate** panel.

## Automation

It requires a few steps, but this script does support automation for many of the parameters!

To enable parameter automation, after loading the script:

1. Make sure you're in the backend view for the patch (wrench icon)
2. click the `edit 🔒` button in the bottom left hand corner of the Script Editor view.
3. You should see a text editor appear.
4. In the center of the text editor's panel you should see a pulldown menu, `Apply from...` - select `...Editor/Patch` from this menu.
5. Now press the `Apply` button at the far right. 
6. Voila! If you go to `Automation > Host Automation` in the left hand pane, you'll see that the script uses host parameters starting at `#0400`. This range should be high enough to avoid overlapping most of the pre-existing automation of the built-in scripting of commercial libraries, but we can't promise this will always be the case.

Kontakt scripts do not officially support automation for some types of UI (such as menus and tables), but we did the best we could to work around it. It may be a little janky!