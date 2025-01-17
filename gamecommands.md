GameCommands are constructed from subcommands separated by semicolons.
Subcommands are constructed from a command name and its arguments, separated by commas.
Each command takes its arguments and interprets them to set a property of the GameCommand.

Most of the things that can be done through GameCommands can be done better through other means.  GameCommand is kept around for compatibility with older versions and because ScreenOptionsMaster based screens often don't have the ability to use the better ways of doing things for their choices.

Example command:
"name,Example;screen,ScreenInit"
This example creates a GameCommand with the name "Example" and its screen property set to "ScreenInit".

When a GameCommand is applied, its properties are used to change things about the game.

The various properties that can be set for a GameCommand are listed below, with their effects when applied.

# announcer
Sets the name of the announcer.  The argument must be the name of the directoory of the announcer.

# applydefaultoptions
Applies the default options to the player.  No argument.

# clearcredits
Clears any credits that have been inserted.  No argument.

# course
Sets the current course to the argument.

# difficulty
Sets the preferred difficulty for both players.
Acceptable args are:
Beginner, Easy, Medium, Hard, Challenge, Edit

# fademusic
Must have 2 args:  The volume to fade out to and the seconds to spread the fade over.

# goalcalories
Sets the calorie goal of the player.

# goaltype
Sets the goal type of the player.  Types are:  Calories, Time, None.

# insertcredit
Inserts a credit.  No arguments.

# lua
Sets a lua function to be run when this GameCommand is applied.

# mod
Sets a modifier to be applied to the player(s).

# name
Sets the name of this GameCommand.  For GameCommands used in option rows as choices, this is used to set the text that is shown on screen for the choice.

# playmode
The "playmode" game command controls what mode of play the game is in.  This is a choice between the normal play mode and the various course or battle modes.  The noral effects of the different playmodes are described in playmods.txt, though a theme can check the current playmode and do anything it pleases with that information.
Acceptable args are:
Regular, Nonstop, Oni, Endless, Battle, Rave

# preparescreen
Prepares the screen named by the argument when the command is applied.  PrepareScreen takes time and blocks graphics, so this should not be used for screens that load a lot of data.

# profileid
Sets the default local profile ID of the player.

# screen
Sets the screen that will be transitioned to when this GameCommand is applied.

# setenv
Arguments are "key,value" pairs of environment variables to be set.  Only capable of setting string values.

# setpref
Must have 2 args:  The preference and the value to set it to.  Preferences are listed in Preferences.ini.

# song
Sets the current song.  The argument should be of the form "Group/SongName".

# songgroup
Sets the preferred song group.  Does not immediately change the group on the music wheel, but the preferred group is the group that will be open when ScreenSelectMusic starts.

# sort
Sets the sort order.  Does not immediately change the sort on the music wheel, but the sort is the sort that will be used when ScreenSelectMusic starts.
Sort names are:
Preferred, Group, Title, BPM, Popularity, TopGrades, Artist, Genre, BeginnerMeter, EasyMeter, MediumMeter, HardMeter, ChallengeMeter, DoubleBeginnerMeter, DoubleEasyMeter, DoubleMediumMeter, DoubleHardMeter, DoubleChallengeMeter, ModeMenu, AllCourses, Nonstop, Oni, Endless, Length, Roulette, Recent.

# sound
Plays the sound at the path once.

# stagemod
Sets a modifier to be applied to the stagemods.

# steps
Sets the current steps to the steps at the specified difficulty for the current song.  Emits an error if the song or the style is not already set when the GameCommand is parsed.

# stopmusic
Stops the music that is currently playing.  No argument.

# style
The "style" command is used to set the style of the game.  The style of the game controls how many pads/players are used.  Acceptable args depend on the game type.
For dance:  single, versus, double, couple, solo, couple-edit, threepanel, routine
For pump:  single, versus, halfdouble, double, couple, couple-edit, routine
For kb7:  single, versus
For ez2:  single, real, versus, versusReal, double
For para:  single, versus
For ds3ddx:  single
For beat:  single5, versus5, double5, single7, versus7, double7
For maniax:  single, versus, double
For techno:  single4, single5, single8, versus4, versus5, versus8, double4, double5, double8
For popn:  popn-five, popn-nine
For lights:  cabinet

# text
Sets the text property of the GameCommand.  This is an alternative to the name field used by some screens.

# trail
Sets the current trail to the trail at the specified difficulty for the current course.  Emits an error if the course or the style is not already set when the GameCommand is parsed.

# url
Exits the game and launches a browser to visit the url.

# urlnoexit
Launches a browser to visit the url.

# weight
Sets the weight of the player.