Below is a list of MessageCommands you can use inside Actors.

Non MessageCommands are located at https://github.com/stepmania/stepmania/wiki/Actor-Definitions

Note: This list is incomplete. All commands are suffixed with MessageCommand when used in an actor, this is omitted for readability.

# Universal MessageCommands
Many more global commands can be found by looking at [MessageManager.cpp](https://github.com/stepmania/stepmania/blob/5_1-new/src/MessageManager.cpp) in the source.

### CodeMessageCommand

Executed when any button is pressed. You must have CodeNames set in the respective screen in metrics.ini for this to function correctly.

| Parameters | Description | Return Type |
| ---------- | ----------- | ----------- |
| Name | the name of the code you specified. So if you have `Codeleft="Left"` in metrics.ini and you press left, params.Name would be "left" | String (CodeName) |
| PlayerNumber | PLAYER_1 or PLAYER_2 | String (PlayerNumber) |


### ScreenChanged
Broadcast when the screen changes, of course. Useful if you use SCREENMAN:AddNewScreenToTop()

### UpdateScreenHeader

### PlayerJoined

### PlayerUnjoined

### MenuSelectionChanged

### CoinsChanged

### PlayModeChanged

### CurrentStyleChanged

### CurrentGameChanged
Since changing the game restarts the theme, this messagecommand is useless.

## Memory Card Related
### StorageDevicesChanged

Executed when the state of a memory card changes. (Refer to the MemoryCardState Enum for more info)

### CardRemovedP1 & CardRemovedP2

## GameSoundManager
(This is mostly global, but it's only really usable during gameplay or if you've configured your theme's audio to align to the beat)

### BeatCrossed

| Parameters | Description | Return Type |
| ---------- | ----------- | ----------- |
| Beat | The current beat. | float? Maybe int? |

# Screen Specific

## ScreenSelectMusic

Note: You can probably find more in ScreenSelectMusic.cpp by checking what is broadcasted to MESSAGEMAN.

### Set
This command also works in Course mode.

Broadcast when a MusicWheelItem is being set with new information, such as when scrolling up and down. Can access parameters using SetMessageCommand=function(self, params)

| Parameters | Description | Variable Type |
| ---------- | ----------- | ----------- |
| Song | An instance of the Song that was just set to the MusicWheelItem. | Song |
| Course | If in course mode, an instance of the Course that was just set to the MusicWheelItem. | Course |
| Index | The index of the MusicWheelItem that was just set. | int |
| HasFocus | If the MusicWheelItem is focused or not. | boolean |
| Text | The name of the song group this MusicWheelItem is from? | String |
| DrawIndex | ??? | int |
| Type | The type of the item, as a string | WheelItemDataType enum? |
| Color | The color of this item. Colors are set by preferred sort or metrics. | ??? |
| Label | The text of this item, using the string translations (ex. en.ini) | String |


### CurrentStepsPXChanged

Replace 'X' with either 1 or 2 (for the player number). Triggered when the currently selected steps change, whether it be by changing the difficulty or selecting another song.

### CurrentSongChanged

Self explanatory.

### PreviousSong or NextSong

Triggered when the player selects a different song in the songwheel by tapping left or right.

### ChangeSteps

Also probably works in ScreenSelectCourse. Triggered when steps are changed. Need to check player & direction using ChangeStepsMessageCommand=function(self, params) then params.Player and params.Direction.

params.Player is always PLAYER_1 or PLAYER_2 and params.Direction is always 1 or -1.

### PreferredSongGroupChanged

### SortOrderChanged
Broadcast when the sort order is changed for any reason.

## TwoPartSelect
(Part of ScreenSelectMusic, but only available if you've turned on TwoPartSelect)
### TwoPartConfirmCanceledMessageCommand
Two part confirm was cancelled. The confirm only shows in multiplayer.
### SongUnchosenMessageCommand
Two Part Select was exited.
### SongChosenMessageCommand
Two part select was opened.

## ScreenSelectCourse

### CurrentCourseChanged

Self explanatory.

### PreferredCourseGroupChanged

### CurrentTrailPXChanged

Replace 'X' with either 1 or 2 (for the player number). Triggered when the Trail is changed. Might work in other screens?
## OptionsList
### OptionsListOpened / OptionsListClosed
Triggered when a player opens/closes the OptionsList.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |

### OptionsListQuickChange
Triggered when a player is in an OptionsList menu, highlights a submenu, then holds start and presses left or right to quickly switch the option.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| Direction | Either 1 or -1. |
| Selection | The index of the currently selected item? |
### OptionsListLeft / OptionsListRight
Triggered when a player presses left/right.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| Selection | The index of the currently selected item, starting at 0 |
### OptionsListStart
The same as OptionsListLeft/Right except the Selection is NOT broadcast.
The selection will always be one more then the number of rows.
To get the number of rows you can add an OptionsMenuChanged listener like in this example.
numRows would be a variable kept outside this function and then accessed inside the OptionsListStartMessageCommand funciton.
This will not work for any lua OptionsList functions, since those don't use metrics and thus do not have an OptionsListMaster entry.
```lua
OptionsMenuChangedMessageCommand=function(self,params)
	if params.Player == pn then
		numRows = tonumber(THEME:GetMetric("ScreenOptionsMaster",params.Menu))
	end;
end;
```


| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
### OptionsMenuChanged
Triggered when the player enters or exits a menu in the OptionsList.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| Menu | The name of the the new menu in the OptionsList, as defined in metrics under ScreenOptionsMaster. |
### OptionsListPop
Unknown, possibly when the player exits from an OptionsList submenu.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
### OptionsListPush
Same as above except when entering a submenu.
### OptionsListReset
Triggered when they press the reset button in the OptionsList, resetting their modifiers to ModsLevel_Preferred.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |

## ScreenOptions
(All children of ScreenOptions class will broadcast these too, ex. ScreenPlayerOptions)

### ChangeValue (Unused)
Triggered... Never. This is inside the function ScreenOptions::ChangeValueInRowAbsolute(), but it's never called.

| Parameters | Description |
| ---------- | ----------- |
| PlayerNumber | PLAYER_1 or PLAYER_2 |
| RowIndex | The current index of the selected item |

### ChangeRow
Triggered when row is changed.

| Parameters | Description | Return Type |
| ---------- | ----------- | ----------- |
| PlayerNumber | PLAYER_1 or PLAYER_2 | String (PlayerNumber) |
| RowIndex | The current index of the newly selected row | int |
| ChangedToExit | If the new row is an exit row | boolean |

### SelectMultiple
Triggered when a selection on a SelectMultiple row is changed.

| Parameters | Description | Return Type |
| ---------- | ----------- | ----------- |
| PlayerNumber | PLAYER_1 or PLAYER_2 | String (PlayerNumber) |
| RowIndex | The current index of the hovered item?? | int |
| ChoiceInRow | ???? | int |
| Selected | If the current selection was just selected or deselected. | boolean |

## ScreenGameplay

### LifeChanged

Activated whenever a player's life changes.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| LifeMeter | Amount of life in a decimal from 0 to 1 |

If the lifebar is type is battery it will also have LivesLeft and LostLife.
### HealthStateChanged

Activated whenever a player's health state changes...

| Parameters | Description |
| ---------- | ----------- |
| PlayerNumber | Either PLAYER_1 or PLAYER_2 |
| HealthState | A HealthState Enum, which is either `HealthState_Hot`, `HealthState_Alive`, `HealthState_Danger`, or `HealthState_Dead`. |
| OldHealthState | self explanatory. |

### PlayerFailed
This one's obvious.

| Parameters | Description |
| ---------- | ----------- |
| PlayerNumber | Either PLAYER_1 or PLAYER_2 |

### ScoreChanged

Activated whenever a player's score changes. Params include PlayerNumber and MultiPlayer, but can also include ToastyCombo in certain cases.

| Parameters | Description |
| ---------- | ----------- |
| PlayerNumber | Either PLAYER_1 or PLAYER_2 |
| MultiPlayer | ??? |
### Judgment
Triggered when a judgment happens, either because a player stepped on a note or they completely missed it.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| MultiPlayer | If they're multiplayer, probably |
| TapNoteSccre | The TapNoteScore |
| Early | True if early, false if late |
| TapNoteOffset | Offset of the judgement |
| HoldNoteScore | The HoldNoteScore |

### ComboChanged

Activated whenever a combo changes.

| Parameters | Description |
| ---------- | ----------- |
| Player | Either PLAYER_1 or PLAYER_2 |
| OldCombo | ??? |
| OldMissCombo | ??? |
| PlayerState | An instance of PlayerState. This may not always be present. |
| PlayerStageStats | An instance of PlayerStageStats. This may not always be present. |

### ToastyAchieved

| Parameters | Description |
| ---------- | ----------- |
| PlayerNumber | Either PLAYER_1 or PLAYER_2 |
| ToastyCombo | ??? |
| Level | ??? |

### ToastyDropped

| Parameters | Description |
| ---------- | ----------- |
| PlayerNumber | Either PLAYER_1 or PLAYER_2 |
### DoneLoadingNextSong

Unknown, might be triggered during course mode

## ScreenNameEntryTraditional

### MenuTimerExpired

Triggered when the timer reaches 0. (Why this even exists is unknown)