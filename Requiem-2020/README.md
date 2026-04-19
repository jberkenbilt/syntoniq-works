# Requiem 2020 by Dolores Catherino

## Syntoniq Cover by Jay Berkenbilt

Original work © 2021 Dolores Catherino

* Original [Requiem 2020](https://youtu.be/U4_Fae9uGfc)

[Syntoniq](https://syntoniq.cc) transcription and cover © 2026 Jay Berkenbilt

Licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/)

* Source: [Requiem-2020.stq](./Requiem-2020.stq)
* Csound instrument: [voicelike-1.csd](./voicelike-1.csd)

This Syntoniq transcription of _Requiem 2020_ was done entirely by ear; I have not looked at a score or used spectrum analysis or other analysis tools to get the pitches. The notes, dynamics, and tempos are close to the original, but they are not identical. There may be some unintentional deviation from the original work. The Syntoniq transcription spells the notes using the Syntoniq _generated scale_ notation, which represents pitches using the harmonic sequence. The wave form used was created using Csound and consists of a mixture of Sawtooth, Triangle, and Pulse waves with a low-pass filter, panning, reverberation, and 4.5¢ of detuning.

I have rendered two videos:
* [72-EDO](https://youtu.be/_MUaXThrpUM)
* [Just Intonation](https://youtu.be/EAnaRtWx69s)

You can find audio files directly in this repository. If you are viewing this in GitHub, you will probably have to download the raw version and play it locally as GitHub does not provide an interface for playing audio as of this writing.

* [audio-72-EDO.mp3](./audio-72-EDO.mp3)
* [audio-just-intonation.mp3](./audio-just-intonation.mp3)

To create the just intonation audio, all I did was comment out the `divisions=72` line in the source and modify the resulting csound file to change the detune amounts to 0.

To me, the 72-EDO and just intonation renderings of this transcription have the same "feel" to them, though the pure just intonation version lacks the "shimmer" and complex beat interactions between pitches that are a wonderful part of the original piece. This suggests that the representation of the notes and chords by harmonic structure is largely accurate.

By-ear transcription of 72-EDO is challenging. I used `syntoniq-kbd prompt` to play pitches, matched against the audio played in a looping mode in short sections. Still, it's possible that I may be off a 72-EDO step here and there or have missed notes or inserted extra notes. I believe it is very close.

# Analysis

This transcription uses the [Syntoniq](https://syntoniq.cc) [generated scale](https://syntoniq.cc/manual/microtonality/generated-scales/) notation, which you can find in detail in the Syntoniq documentation. Here's an abridged summary of how it's used in this piece. The documentation describes additional capabilities of the notational system. The manual describes the overall syntax, but in a nutshell, each note is a duration and a note name. If the duration is omitted, it is taken from the previous note.

* A note consists of multiple letters. Each letter is a ratio. A note's value is the product of the ratios.
* When a number of divisions is specified, the resulting note is "snapped to the grid" of the equally divided scale.
* `A` is the tonic of scale.
* `B` through `Y` represent _n/n-1_, where _n_ is the ordinal position in the alphabet; i.e., B=2/1, C=3/2, D=4/3, ..., Y=25/24.
* `b` through `y` are the reciprocals of their uppercase counterparts; i.e., b=1/2, c=2/3, d=3/4, ... y=24/25.

To notate microtonal works using generated scales in Syntoniq, you define a pitch by "locating" it through a path of intervals. This piece uses mostly simple intervals. We are able to "spell" all the notes in the piece using at most two letters. An aspect of using this system is that it spells notes in a manner that is _independent of the tuning system_. Creating a just intonation version of this piece is as simple as just removing the `divisions=72` parameter to the scale definition.

Consider the pitches playing at the end of the first score block: `A`, `J`, `Ck`, `CK`. These have the ratios `1`, `10/9`, `3/2*10/11 = 15/11`, and `3/2*11/10 = 33/20`. Take a look at some of the intermediate ratios. The second and third notes, `10/9` and `15/11`, have the ratio of `15/11 * 9/10` = `27/22`, which is 354.547¢, a very close neutral third. You can actually use `syntoniq calc` to get this directly. Remembering that flipping the case of a note makes it into its reciprocal ratio, `Ck` ÷ `J` = `Ckj`. Note that `jk` itself is 9/11, also a very good neutral third. When snapped to the 72-EDO grid, you have

```
% syntoniq calc pitch 'Ckj!72'
Ckj!72       ^7|24
final pitch  ^7|24
frequency    1.224
octaves      0.292
cents        350.000¢
```

This is as close as you can get to a neutral third in 72-EDO.

Syntoniq has enharmonics in that you can spell a note in an infinite number of ways. If you decide you want the 10/9 whole tone instead of the 9/8 whole tone (these are the 11th and 12th degrees, counting from 0, of 72-EDO), you can use `J`. If you want a fourth above that, you don't have to calculate anything. Just knowing that a fourth is 4/3, which is `D`, you can write `JD`.

I have made an effort in this transcription to capture the harmonic meaning of the notes whenever possible. I did this transcription by using an audio program (I used REAPER because I have a license, but audacity would also have worked) to loop short sections of the audio, then I used `syntoniq-kbd prompt` to help me find the pitches. This piece consists mostly of reasonably consonant chords, sometimes superimposed polytonally. As such, once you figure out the starting pitches, it's fairly easy to use Syntoniq notation to spell out the chords.

There were several instances when I was unsure of exactly which step to use. Steps are very close together in 72-EDO (just 16.667¢, about the amount of flatness in a 12-EDO minor third), and with some choral detuning in the wave form, being off by one step sometimes is barely noticeable in the overall texture. For the most part, I chose exact pitches by going for the same overall chord feel. Varying by just one step in the opening chord makes the chord feel too "major" or too "minor" to my ear. The pitches I chose, to my ear, give the chord the exact same neutral third sound as the original. There are a few places where there are intervals that are off a pure interval by one step, for example, `J` and `I'` (where `'` goes up an octave) appear together, creating an octave + a 72-EDO step. This creates a slightly stretched octave, but it's not really that different from what a choir (or brass ensemble) might do intentionally to create an expansive quality to a chord. Sometimes, when superimposing two chords, the overall effect is more consonant to have the individual chords separately in tune even if there are some odd intervals between the chords. These are the kinds of places where I may have missed a note by a step.

Another challenge is handling difference tones. When you have a rich, complex chord with lots of harmonics, your auditory perceptual system sometimes fills in notes that aren't there. There were a few places where I heard a specific pitch in the chord but wasn't sure whether it was a difference tone or a real note. My decision about whether to include the note was entirely based on whether its presence or absence was more effective for the overall voice leading. It's entirely possible that I may have added phantom notes or have omitted notes that were present but also strongly implied by the harmonic structure. I have listened to the piece many, many times, and to me, the transcription's harmonies achieve the same emotional effect as the original...albeit without the beauty of live performance or the choral timbre that is used in the original work. Still, I think the result is pleasant to listen to, and I hope it does justice.
