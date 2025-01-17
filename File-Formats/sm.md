# About
 
In StepMania 5, `.sm` files have been superseded by [.ssc](ssc) files, which are similar in format but contain additional tags and allow newer features (example: the BPM splitted across difficulties).  New charts created with StepMania 5 will be exported to the `.ssc` format, though the program still supports reading the `.sm` format.
 
 
# `.sm` files
A `.sm` file is primarily composed of two major sections: the **header tags**, and the **chart data**.
 
## Header Tags #
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
Sets the offset between the beginning of the song and the start of the note data in seconds.
 
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
Determines if the song is selectable from the MusicWheel under normal conditions. Valid values are `YES` and `NO`.  

Players can ignore the \#SELECTABLE tag by setting `HiddenSongs=0` in [Preferences.ini](../Preferences.ini) which will result in all songs always being selectable.  The `HiddenSongs` preference is set to `0` by default with fresh installs of StepMania.

Earlier versions (and forks) of StepMania supported `ROULETTE`, `ES` (Extra Stage), `OMES` (One More Extra Stage) and integers (`1` = FINAL STAGE) as valid values, but these are not supported in SM5 and will have the same effect as `YES`.
 
### \#BGCHANGES

The BGCHANGES line is used to control what backgrounds, BG Animations or videos are loaded by the simfile and when they appear. You can create, view, and modify BGChanges in the editor by pressing the `b` key while at the desired beat. 

For example, to view, edit, or create a BGChange at Beat = 25, navigate to beat 25 in the editor and press `b`.


An example BGCHANGES line in the SM file might look like:
 
```
#BGCHANGES:0.000=springbn.png=1.000=1=0=1===CrossFade==;
```

Multiple background changes can be set by separating them with commas like:

```
#BGCHANGES:0.000=springbn.png=1.000=1=0=1===CrossFade==,
25.000=flash=1.000=0=0=1====#FFFFFF=;
```

Other example BGCHANGES lines if the song have a video and you did not change the BG at the last note:
```
#BGCHANGES:0=(video file).avi=1.000=0=0=0,
99999=-nosongbg-=1.000=0=0=0 // don't automatically add -songbackground-
;
```
Another example BGCHANGES lines for stage videos (Dance Phenomena is used as example):

```
#BGCHANGES:
-40=(stage video).avi=0.000=0=1=0, // Init stop before beat 0
0=(stage video).avi=1.000=0=0=0, // Start video
35=(stage video).avi=2.000=0=0=0, // BPM change is doubled
35.5=(stage video).avi=0.500=0=0=0, // BPM change is halved
35.75=(stage video).avi=1.000=0=0=0, // BPM change reverted to normal
83=(stage video).avi=2.000=0=0=0, // BPM change is doubled
83.5=(stage video).avi=0.500=0=0=0, // BPM change is halved
83.75=(stage video).avi=1.000=0=0=0, // BPM change reverted to normal
180=(stage video).avi=0.000=0=0=0, // Stop
180.001=(stage video).avi=1.000=0=0=0, // End stop
180.5=(stage video).avi=0.000=0=0=0, // Stop
180.501=(stage video).avi=1.000=0=0=0, // End stop
181=(stage video).avi=0.000=0=0=0, // Stop
181.001=(stage video).avi=1.000=0=0=0, // End stop
183=(stage video).avi=0.000=0=0=0, // Stop
183.001=(stage video).avi=1.000=0=0=0, // End stop
183.5=(stage video).avi=0.000=0=0=0, // Stop
183.501=(stage video).avi=1.000=0=0=0, // End stop
184=(stage video).avi=0.000=0=0=0, // Stop
184.001=(stage video).avi=1.000=0=0=0, // End stop
186=(stage video).avi=0.000=0=0=0, // Stop
186.001=(stage video).avi=1.000=0=0=0, // End stop
186.5=(stage video).avi=0.000=0=0=0, // Stop
186.501=(stage video).avi=1.000=0=0=0, // End stop
187=(stage video).avi=0.000=0=0=0, // Stop
187.001=(stage video).avi=1.000=0=0=0, // End stop
224=(stage video).avi=2.000=0=0=0, // BPM change is doubled
224.5=(stage video).avi=0.500=0=0=0, // BPM change is halved
224.75=(stage video).avi=1.000=0=0=0, // BPM change reverted to normal
257=(stage video).avi=2.000=0=0=0, // BPM change is doubled
99999=-nosongbg-=1.000=0=0=0 // don't automatically add -songbackground-
;
```

The set of entries is between the colon and the semicolon.
Each entry is separated from the next by a comma.
Each entry is composed of 1 to 11 values separated by equals.
 
![image](https://user-images.githubusercontent.com/30600688/202782605-9bd6b076-31d4-4193-8d5e-43dd38e53d1a.png)

The meanings of the values are as follows:
 
1. start beat (can be negative if you edit with ani text editor)
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
 
The file names (values 2 and 8) and the colors (values 10 and 11) are passed to the effect file as thread variables. Most effects do not use the second file. Most SM files use 6 values per each BGCHANGES line.

TODO: Add more information about BGChanges in the editor
 
### \#FGCHANGES
Defines the foreground changes for this song. Format is the same as `#BGCHANGES`, except only the start beat and first file are used (values 1 and 2).
 
## Chart Tags
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
 
Note data is defined in terms of "measures" where a measure is several lines of text, terminated by a comma. The final measure in a chart is terminated by a semicolon instead. Each line consists of a set of characters representing each playable column in the chart type.
 
Valid note types are 4th, 8th, 12th, 16th, 24th, 32nd, 48th, 64th, and 192nd. Each measure consists of a number of lines that corresponds to one of these numbers. The total number of beats covered by any given measure is 4, and each line represents a portion of that. If a measure has 64 lines, for example, each line represents 1/64th of those 4 beats, or 1/16th of a beat, with the first line representing beat 0 within the measure. The note type of a given line can be determined by taking said beat value, dividing by 4, and then simplifying the fraction as much as possible and looking at the denominator. If the denominator is 96, 192 is used as the note type instead.
 
### Note Values
These are the standard note values:
 
* `0` – No note
* `1` – Normal note
* `2` – Hold head
* `3` – Hold/Roll tail
* `4` – Roll head
* `M` – Mine (or other negative note)
 
Later versions of StepMania accept other note values which may not work in older versions:
 
* `K` – Automatic keysound
* `L` – Lift note
* `F` – Fake note
 
### Non-Standard Tags
You might run into some .sm files with some non-standard tags. Though these aren't supported by StepMania, they're (maybe) good to know.
 
### \#MENUCOLOR
Defines the color of the song on ScreenSelectMusic. Origin is StepMania 3.9 Plus?  Not supported in SM5.
