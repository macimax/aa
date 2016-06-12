# About

In StepMania 5, `.sm` files have been superseded by [.ssc](file-formats/ssc) files, which are similar in format but contain additional tags and allow newer features.  New charts created with StepMania 5 will be exported to the `.ssc` format, though the program still supports reading the `.sm` format.


# `.sm` files
A `.sm` file is primarily composed of two major sections: the **header tags**, and the **chart data**.

##Header Tags
The header tags contain information that should be shared between all charts, such as `#TITLE:` and `#ARTIST:`.  Most header tags follow the format `#TAG:VALUE;`, though some tags have their own format.

### \#TITLE
Sets the primary title of the song.

### \#SUBTITLE
Sets the subtitle of the song.

### \#ARTIST
Sets the artist of the song.

### \#TITLETRANSLIT
Sets the transliterated primary title of the song, which is used when `ShowNativeLanguage=0`.

### \#SUBTITLETRANSLIT
Sets the transliterated subtitle of the song, which is used when `ShowNativeLanguage=0`.

### \#ARTISTTRANSLIT
Sets the transliterated artist of the song, which is used when `ShowNativeLanguage=0`.

### \#GENRE
Sets the genre of the song.

### \#CREDIT
Defines the simfile's origin (author or pack/mix).

### \#BANNER
Sets the path to the banner image for the song. Banner images are typically rectangular, with common sizes being 256x80 (DDR), 418x164 (ITG), and 512x160 (DDR doubleres).

### \#BACKGROUND
Sets the path to the background image for the song. Background images are typically 640x480 or greater in resolution.

### \#LYRICSPATH
Sets the path to the lyrics file (`.lrc`) to use.

### \#CDTITLE
Sets the path to the CD Title, a small image meant to show the origin of the song. The recommended size is around 64x48.

### \#MUSIC
Sets the path to the music file for this song.

### \#OFFSET
Sets the offset between the beginning of the song and the start of the note data.

### \#BPMS
Sets the BPMs for this song. BPMS are defined in the format `Beat=BPM`, with each value separated by a comma.

### \#STOPS
Sets the stops for this song. Stops are defined in the format `Beat=Seconds`, with each value separated by a comma.

### \#SAMPLESTART
Sets the start time of the song sample used on ScreenSelectMusic.

### \#SAMPLELENGTH
Sets the length of the song sample used on ScreenSelectMusic.

### \#DISPLAYBPM
This can be used to override the BPM shown on ScreenSelectMusic. This tag supports three types of values:

* A number by itself (e.g. `#DISPLAYBPM:180;`) will show a static BPM.
* Two numbers in a range (e.g. `#DISPLAYBPM:90:270;`) will show a BPM that changes between two values.
* An asterisk (`#DISPLAYBPM:*;`) will show a BPM that randomly changes.

### \#SELECTABLE
Determines if the song is selectable under normal conditions. Valid values are `YES` and `NO`.

### \#BGCHANGES
The BGCHANGES line is used to control what backgrounds are loaded by the simfile and when they appear.

An example BGCHANGES line might look like:

```
#BGCHANGES:0.000=springbn.png=1.000=1=0=1===CrossFade==,
25.000=flash=1.000=0=0=1====#FFFFFF=;
```

The set of entries is between the colon and the semicolon.
Each entry is separated from the next by a comma.
Each entry is composed of 1 to 11 values separated by equals.

The meanings of the values are as follows:

1. start beat
2. file or folder name
3. play rate
4. Backward compatible transition type. CrossFade is used if this is not 0.
5. Backward compatible effect flag. StretchRewind is used if this is not 0.
6. Backward compatible effect flag. StretchNoLoop is used if this is not 0.
7. Name of the effect file to use. The BackgroundEffects folder will be searched for a match.
8. Name of the second file.
9. Name of the transition file to use. The BackgroundTransitions folder will be searched for a match.
10. Color string in either "1.0^0.5^0.75^0.25" or "#ff7fcf3f" form. The fourth channel is optional.
11. Second color string, same format.

The file names (values 2 and 8) and the colors (values 10 and 11) are passed to the effect file as thread variables.  Most effects do not use the second file.

### \#FGCHANGES
Defines the foreground changes for this song. Format is the same as `#BGCHANGES`, except only the start beat and first file are used (values 1 and 2).

##Chart Tags
The .sm format only contains a single tag for a chart, unlike the (later) .ssc format.

### \#NOTES
The Notes tag contains the following information:

* Chart type (e.g. `dance-single`)
* Description/author
* Difficulty (one of `Beginner`, `Easy`, `Medium`, `Hard`, `Challenge`, `Edit`)
* Numerical meter
* Groove radar values, generated by the program
* and finally, the note data itself.

The first five values are postfixed with a colon. Groove radar values are separated with commas.

Note data itself is a bit more complex; there's one character for every possible playable column in a chart type. Note types (e.g. 4th, 8th, etc.) are determined by how many rows exist before the comma (which separates measures).

### Note Values
These are the standard note values:

* `0` – No note
* `1` – Normal note
* `2` – Hold head
* `3` – Hold/Roll tail
* `4` – Roll head
* `M` – Mine

Later versions of StepMania accept other note values which may not work in older versions:

* `K` – Automatic keysound
* `L` – Lift note
* `F` – Fake note

### Non-Standard Tags
You might run into some .sm files with some non-standard tags. Though these aren't supported by StepMania, they're (maybe) good to know.

### \#MENUCOLOR
Defines the color of the song on ScreenSelectMusic. Origin is StepMania 3.9 Plus?