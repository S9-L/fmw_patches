# 1.2.6.1a ENG/JPN Hotfix
## TL;DR Repatch your 1.2.6 data.win to the 1.2.6.1a hotfix, and download the missing `addOns/data4/Meko/` folder for Mehko's Thunder Ram MAP attack dialog, if desired.

- Fix gamebreaking bug where the game would crash if a MAP attack killed a unit that had no dialog after being defeated. The instance variable tracking the previous dialog index position was not reset to -1 after the new multi-line dialog handling for MAP attacks. The -1 value indicates that there were no previous lines in a dialog group. However, this variable held a nonnegative value from the previous handling and was carried over to the dialog selection logic for other units on the chapter map, including the cases where dialog should default to nothing.
  - Since the previous dialog index is used to search for dialog that contains multiple lines, the game assumes a multi-line dialog group exists when the dialog selection function is supplied with a nonnegative index. Naturally, because units without defeat dialog don't have any lines, this would crash the game if the game tried to read dialog from nonexistent data.

- Add missing dialog files for Mehko's Thunder Ram MAP attack. Download the `addOns/data4/Meko/` folder and place it in your local `fmw_dosd/addOns/data4` folder to properly see it in-game.

# 1.2.6.1 ENG/JPN Release
## IMPORTANT INSTRUCTIONS, READ THIS FIRST BEFORE INSTALLING! ##
0. These instructions are important if you want to keep your existing addOns changes without them being overwritten. Otherwise, if you want a fresh install of 1.2.6.1, back up your previous addOns and mods folders, then download the latest addOns and mods folders in this repo and place them in your `fmw_dosd` folder. You can then apply the respective 1.2.6.1 patch depending on your localization (ENG or JPN) to your `data.win` file. You won't need to perform the rest of the steps here if a fresh install is all that's needed.

1. If your `fmw_dosd` folder already contains an existing addOns folder, delete the following addOns placeholder files in your existing installation:
    - `addOns/data4/data_bullet_all/data_bullet_all.json`
    - `addOns/data5-4/Data_Bullets_new/Data_Bullets_new.json`
    - `addOns/data5-4/Data_Chudan/Data_Chudan.json`
    - `addOns/data5-4/Data_Items/Data_Items.json`
    - `addOns/data5-4/Data_Land/Data_Land.json`
    - `addOns/data5-4/Data_Name/Data_Name.json`
    - `addOns/data5-4/Data_Specials/Data_Specials.json`
    - `addOns/data5-4/Data_Spells/Data_Spells.json`
    - `addOns/data5-4/Data_Stages/Data_Stages.json`
    - `addOns/data5-4/Data_Tips2/Data_Tips2.json`
    - `addOns/data5-4/Data_WMap/Data_WMap.json`
    - `addOns/data5-4/Data_WMap2/Data_WMap2.json`

    The game will crash every time if one of these addOns types becomes implemented in a future modding release. These should never have been put in the canonical path for      loading addOns; better to finally correct this and avoid future complications down the line.

2. Replace the `addOns/data5-4/Data_Updates/LettyFriendshipUpdateFix.json` file with the current version in the GitHub repo. The modding release has fixed an indexing bug with the addOns logic for `Data_Updates` to match the line numbers as presented in a text editor. As a result, the Letty Friendship fix has been updated with the correct corresponding Line Number to replace in the original `Data_Updates.txt` file.

3. In addition, rename the file at `addOns/data5-4/Data_PairName/Data_PairName.json` to `addOns/data5-4/Data_PairName/Kedama_Evileye_PairName.json`. This gives the file a proper name instead of leaving it with a template name.

4. Replace the previous modding release's `addOns/data4/data_char_skill_all` files with the new ones in this release. The previously separated CharSkill files are now grouped into single files for easier bookkeeping. You should replace the following files:

```
New File: AliceHouraiCharSkill.json
Replace:
- addOns/data4/data_char_skill_all/Alice01CharSkill.json
- addOns/data4/data_char_skill_all/Alice02CharSkill.json
- addOns/data4/data_char_skill_all/Alice03CharSkill.json
- addOns/data4/data_char_skill_all/Alice04CharSkill.json
- addOns/data4/data_char_skill_all/Alice05CharSkill.json
- addOns/data4/data_char_skill_all/Alice06CharSkill.json
- addOns/data4/data_char_skill_all/Alice07CharSkill.json
- addOns/data4/data_char_skill_all/Alice08CharSkill.json
- addOns/data4/data_char_skill_all/Alice09CharSkill.json

New File: Aya_RestoredSkillset.json
Replace: addOns/data4/data_char_skill_all/Aya01CharSkill.json

New File: Daiyosei_RestoredSkillset.json
Replace:
- addOns/data4/data_char_skill_all/Daiyosei01CharSkill.json
- addOns/data4/data_char_skill_all/Daiyosei02CharSkill.json

New File: Eiki_RestoredSkillset.json
Replace: addOns/data4/data_char_skill_all/Eiki01CharSkill.json

New File: Kaguya_RestoredSkillset.json
Replace: addOns/data4/data_char_skill_all/Kaguya01CharSkill.json

New File: Koakuma_RestoredSkillset.json
Replace: addOns/data4/data_char_skill_all/Koakuma01CharSkill.json

New File: Kogasa_RestoredSkillset.json
Replace: addOns/data4/data_char_skill_all/Kogasa01CharSkill.json

New File: Komachi_RestoredSkillset.json
Replace:
- addOns/data4/data_char_skill_all/Komachi01CharSkill.json
- addOns/data4/data_char_skill_all/Komachi02CharSkill.json
- addOns/data4/data_char_skill_all/Komachi03CharSkill.json
- addOns/data4/data_char_skill_all/Komachi04CharSkill.json

New File: Korin_RestoredSkillset.json
Replace:
- addOns/data4/data_char_skill_all/Korin01CharSkill.json
- addOns/data4/data_char_skill_all/Korin02CharSkill.json

New File: Kurumi_RestoredSkillset.json
Replace: addOns/data4/data_char_skill_all/Kurumi01CharSkill.json

New File: Meiling_RestoredSkillset.json
Replace:
- addOns/data4/data_char_skill_all/Meiling01CharSkill.json
- addOns/data4/data_char_skill_all/Meiling02CharSkill.json

New File: Mokou_RestoredSkillset.json
Replace:
- addOns/data4/data_char_skill_all/Mokou01CharSkill.json
- addOns/data4/data_char_skill_all/Mokou02CharSkill.json

New File: Remilia_RestoredSkillset.json
Replace: addOns/data4/data_char_skill_all/Remilia01CharSkill.json

New File: Rumia_RestoredSkillset.json
Replace:
- addOns/data4/data_char_skill_all/Rumia01CharSkill.json
- addOns/data4/data_char_skill_all/Rumia02CharSkill.json
- addOns/data4/data_char_skill_all/Rumia03CharSkill.json

New File: Sanae_RestoredSkillset.json
Replace: 
-  addOns/data4/data_char_skill_all/Sanae01CharSkill.json
-  addOns/data4/data_char_skill_all/Sanae02CharSkill.json

New File: Shizuha_RestoredSkillset.json
Replace:
- addOns/data4/data_char_skill_all/Shizuha01CharSkill.json
- addOns/data4/data_char_skill_all/Shizuha02CharSkill.json

New File: Wriggle_RestoredSkillset.json
Replace:
- addOns/data4/data_char_skill_all/Wriggle01CharSkill.json
- addOns/data4/data_char_skill_all/Wriggle02CharSkill.json
- addOns/data4/data_char_skill_all/Wriggle03CharSkill.json

New File: Yukari_RestoredSkillset.json
Replace:
- addOns/data4/data_char_skill_all/Yukari01CharSkill.json
- addOns/data4/data_char_skill_all/Yukari02CharSkill.json
- addOns/data4/data_char_skill_all/Yukari03CharSkill.json
```

5. Once steps 1, 2, 3, and 4 have been completed, drag-and-drop the addOns folder from the repo into your `fmw_dosd` folder to install the new addOns files. To keep your previous addOns changes, do NOT overwrite your existing files if prompted by the OS to replace the files.

6. Drag-and-drop the updated mods folder in this repo into your `fmw_dosd` folder to install the new JSON mods. Similarly, do NOT overwrite your existing files in order to keep your JSON mod changes.

7. Due to a majority of hardcoded text being moved out of the EXE into user-editable files, the addOns folder is now required for modding releases starting from 1.2.6.1. If you encounter issues with various text elements in-game, make your local addOns folder is updated with the most recent version in the repo.

## Major Features
- Primarily a bug-fixing patch, with some headway made to lay the foundation for future custom chapter creation. In addition, this release includes features restored from the original games that have been improved over their original implementations.
  - Please report any bugs under the Issues section of this repo, or follow up in the FMW Modding Framework Bug Reports Forum in the unofficial FMW Discord: https://discord.gg/q7tpedHj68.

![Custom Team Names Feature](https://i.imgur.com/JIAOZsX.png)

- Implement and improve the custom team name feature that was present in the original FMW games and Doujin CB. Previously, this feature was implemented with a Windows dialog box that would pause the entire game execution until the player finished creating their team names. Now, the entire UI has been overhauled to function in-engine for the player to freely navigate. You can access this by selecting the `Change Pair Name` menu option; this will open a separate menu for custom team name editing, instead of cycling through the available team names in a selected pair.

  - You can use the trigger buttons to toggle the default team names defined in `Data_PairName`, or select the `Input` option to manually create your own team names using the keyboard. There is a 50 character limit that's more of a recommendation than a strict requirement. In certain UI elements, the game applies scaling to fit the text it needs to draw within a limited pixel length, so overly long team names are not advised. The player can also retrieve the last 20 created team names and set any of them on the currently selected team.

  - Once you've entered your team name, you can select the `Confirm` option to register it. In addition, pressing ESC in the Input menu will revert the team name back to what it was before the Input screen, while pressing the Back button to exit the custom team name menu will cancel all team name changes. This is to ensure the `Confirm` option unambiguously registers the custom team name; these controls also allow for quick resets, if needed.

  - When the game is saved, a new JSON file with the filename format `gsw_xxx_extraData.json` will be saved alongside the regular save file. Currently, this new JSON file holds all the extra data needed to save and load custom team names, including the last modding version the save file was saved on, the list of custom team names + the list of team IDs corresponding to those team names, and the list containing the last 20 created team names.
 
    - Similarly, extraData JSON files are also created when suspend/turn saves are made. This is required to preserve your registered team names; otherwise, you would lose your custom team name data every time a suspend/turn save was loaded.
   
    - In the future, this extraData JSON file may be expanded to save additional data without conflicting with vanilla saves.
   
    - Because the team name data is saved in plaintext, you can freely edit the entries in the JSON. This is the most convenient option at the moment for viewing/updating your custom team names without needing external tools.

![Key Config Feature](https://i.imgur.com/avPHba2.png)

- Implement a new "Key Config" section in Settings that lets the player remap keyboard controls. You can essentially remap all your controls for a standard English keyboard (with support for other keyboard input keys that are recognized by GameMaker), restoring the keyboard controls config from the original FMW games and Doujin CB.

  - Navigate the interface using your arrow keys (or directional inputs on a controller), highlight a button control, then press the Confirm key/button to change the highlight color to light blue. Finally, press the key you wish to map to your selected control. If you want to restore the default keyboard controls back to vanilla, select the "Default" option. All previous controls will be retained until you select the "Save Config" option; this is to prevent your controls from chaotically changing during the remapping process. If you wish to exit this menu without changing your controls, press the Back key/button to cancel all changes.

  - Once you select "Save Config", your newly configured keyboard controls will be saved to a `key_config.json` file in the currently set save folder (usually it's `fmw_dosd/savedata/` if you haven't changed your save folder location). This file will be read at game startup to override the vanilla keyboard controls with your custom keyboard configuration.

  - Virtual Key Constant to Key Name mapping sourced from here: https://gist.github.com/attic-stuff/382c0aa89187afd043cf45890c0661f9

- Restore weapon paging functionality that was previously present in FMW4. As a refresher, units with more than 8 weapons had extra pages dedicated to displaying and selecting the unit's weapons. This was removed in CB so that all weapons could be displayed on a single page, but not all of the internal paging logic was removed. Because of this, there were certain buggy interactions with weapon indexing for units that had more than 8 weapons. A previous modding feature temporarily fixed this by expanding the page weapon limit to 13; however, weapon paging bugs still remained if units were given more than 13 weapons.

  - With the new modding release, paging functionality has been re-implemented in the unit weapon status screen. The total weapon list is now subdivided into mutliple pages that can display up to 13 weapons at once. The player can then flip through these pages using directional inputs to view each page. In addition, selecting a weapon on a given page will always correspond to the correct internal weapon index now, so this should fix previous bugs that occurred due to mismatched weapon indices.

  - Weapon lists can become as expansive as the player desires. This will be a boon for custom characters that are designed with larger weapon lists in mind.

- Improve weapon auto-selection after traversing through various menus in the battle info screen. For context, executing certain actions like Spirit casting, changing counterattack options, activating Support actions, selecting FPM attacks, etc. would always reset the saved cursor position for weapon selection to 0, AKA the top of the weapon list on the 1st page. New logic has been added to save the cursor position 1st before these actions begin. Then, once the actions are finished, the cursor position is restored to what it was before. In summary, the weapon selection cursor should always correspond now to whatever weapon is currently displayed in frontline/backline in the battle info screen.

- Implement addOns support for `Data_Stages` and `Data_Land`. Follow the guidance at the top of this CHANGELOG for 1.2.6.1 to remove the template files.

  - `Data_Stages`: In general, this file contains the overall info related to chapter maps in the game. These chapter map entries include data such as chapter internal ID, chapter name, number of deployment slots, cost limit and night flag, event properties for event handling, BGM/UI/chapter map sprite settings, map dimensions, unit restrictions, chapter win/loss/bonus conditions, and finally bonus condition values used in event handling. At the moment, this addOns type is useful for replacing various chapter map properties and will become necessary for creating new chapter maps once the custom map system has been implemented.

  - `Data_Land`: This file holds the database of terrain tiles distributed across all chapter maps in the game. Each entry is uniquely identified by its ID, which is later referenced in the data10 .dat files to create terrain mappings that specify where certain tiles are placed on chapter maps. In the addOns format, there are various fields that define the terrain tiles' properties. `Evade` is the additive evasion bonus; `Defense` is the additive damage reduction bonus; `Move` is the Move penalty from starting on and moving through the terrain tile; `HPRegen` and `MPRegen` obviously describe the regen values for each stat, and finally `Type` can take the values 0, 1, or 2 and the game has special handling for each terrain type depending on various checks in the EXE.

    - In the future, this addOn will be documented in more detail when the custom map system has been implemented and this file is more thoroughly understood.

- Restore the Scarlet Mist foreground effect on FMW1 chapter maps, as well as certain battle foreground effects that play during the chapters in FMW1 and FMW2. These effects were removed in Complete Box, but through JSON mod toggles and LayeredFS loading, these can be re-enabled once again. You must have the foreground effect files present in `modData/data7` (Hosted here at this Gamebanana link: https://gamebanana.com/mods/734489) and the `EnableLayeredFS` mod enabled.

  - In addition, the Scarlet Mist effect fadeout on Chapter 11 takes into account the new FPS for Complete Box. This way, the gradual fadeout in CB matches the choreography timing for the fadeout in the original FMW1.

- Implement additional logic to support animated small unit/icon sprites with more than 2 frames of animation in Land Terrain for chapter maps and the Intermission, loaded through the `modData/data8` folder after enabling LayeredFS. Previously, unit/icon sprites with the filename format `unit_<UNIT_CODE>.png` could not be properly animated as the vanilla loading routine did not recognize these files to have frames of animation. Even if you created an `_anime.json` addOn to define the frame choreography and made your `unit_<UNIT_CODE>.png` file into a sprite strip, the game would assume the sprite only had 1 frame of animation and would not cycle through the sprite's sub-images.

  - The sprite loading routine is now written to allow `_anime.json` addOns to define frame choreography for these data8 unit/icon sprites in sprite strip format. NOTE: For sprite strips with only 2 frames, the game will fallback to the vanilla frame choreography used for all other units on Land Terrain or in the Intermission, regardless of any `_anime.json` addOns.

- Extract a majority of hardcoded text references in the EXE and previous mods to convert them into `Data_Text` addOns that the game can use to replace text at runtime. This is a massive effort to make text edits more flexible by linking their references in files instead of code. By doing this, code edits will not be required whenever the player wants to change some text in the game that was previously hardcoded. Because the migrated hardcoded text is handled in files now, other localizers can edit the files without needing to make code changes for their translations of the game and/or various mod features.

  - The output text usually defaults to whatever is present in the `Text` field, but if there is an `ENG` and/or `JPN` field, the output will be overridden with either one of those values, depending on whether an ENG or JPN modding patch is applied to the `data.win` file.

  - Add a new `Override` field that can take the name of a generic JSON key name to fetch its corresponding value and output it. For example, I can specify the fields `"Override":"OPTION_2"` and `"OPTION_2":"HOOKED_TEXT"` to make the actual output text "HOOKED_TEXT". This will make it easier to create multiple options for text depending on your localization.

  - This is simply one checkpoint for hardcoded text extraction so far; more hardcoded text will be moved out of the EXE in future modding releases.

- Add support for JSON mods to run an internal GML script function in the EXE after mod changes are saved. You can now include the name of the internal GML script function in a new `Script` field along with an array of arguments to pass to the script function in the `Args` field. This is showcased in the ChangeButtonStyle JSON mod to immediately update the button appearance after mod changes are saved.

- Implement additional logic for MAP attacks to support multiple lines of pre-battle dialogue before executing the MAP, instead of only accepting the 1st line in a dialog group. You can advance the text just as you would in conversation scenes, so feel free to restructure your dialog addOns to include multiple lines of text for MAP attacks.

- Add a new true/false `ID_EF_Switch` field in `Data_Skills` addOns. This lets you override the Skill ID with the Skill EF instead in the routine that normally matches Skill ID to code logic. For context, Personal Skills that allow the unit to execute a command (i.e. Devil's Contract) have their backend logic uniquely determined by their current Skill ID. Skill IDs must be unique to avoid conflicts in the game's skill system, so this effectively makes code reuse impossible for new command Personal Skills with different Skill IDs.

  - The new field makes PS cloning far more flexible with the override to use the EF field instead. For example, let's say I wanted to use Flan's Devil's Contract on another custom unit with a newly created PS. I can write a `Data_Skills` addOn with `"ID":"DC_CLONE"`, `"EF":"CONTRACT_FLAN"`, and `"ID_EF_Switch":true` to apply the original effect of Devil's Contract on a new PS without conflicting with the original.

  - The restored PS for Makura takes advantage of this new field to generically cast a composite set of Spirits after the command is executed.

- Redesign the Exceeded Eternity status mod to display a symbol that lights up when EE is active and dims otherwise, instead of displaying text for either state. 

- Add a "Miscellaneous" section in the Settings menu that reads JSON files from the `fmw_dosd/options/MISC/` folder and creates new, selectable options to execute internal GML script functions. The JSON file defines the appearance of the option and allows you to include the name of an internal GML script function in the `SCRIPT` field and pass an array of arguments in the `ARGS` field. The GML script will then be executed after the option is selected.

  - Example:
  ```
  {
    "GAME_RESTART":
    {
        "TITLE": "Restart Game",
        "SHOW_TYPE": 6,
        "ENABLED": true,
        "OPTIONS":
        [
            "[ Execute ]"
        ],
        "SELECTION": 0,
        "HELP_TEXT": "Restart the game application.",
        "VARIABLE": -1,
        "SCRIPT": "restart_game",
        "ARGS":
        [
            "Restart the game?"
        ]
    }
  }	
  ```

  - This release had plans to include a new option that would have allowed you to restart your game without closing the application. This would have been executed through GML's `game_restart()` function; however, it currently crashes when re-initializing Steam and the consequences of restarting the game this way is not understood enough at this time. Not all dynamic resources and global variables will be re-initialized after the restart, so for now, this feature is paused until further research is done. 

## JSON Mods
- [Text|FileSystem] Change the folder location to custom load data file resources through LayeredFS. Restart the game for the updated folder location to apply (Default location is `modData/`). Due to the GMS sandbox, the folder must be located within the `APPDATA/fmw_dosd` folder to have writeable permissions.

  - Don't forget to add the `/` at the end of your input so the game correctly interprets it as a folder path.
 
- [Toggle|Mechanics] Enable Chain/Exceeded Eternity to trigger on a frontline allied unit if kills occur outside of player main/assist attacks. This will apply regardless of player or enemy distinction for the support attacking unit on the player side. This change restores the previous behavior of Chain/Exceeded Eternity in the original games and Doujin CB.

  - Previously in Doujin CB and FMW4, the game would allow Chain/Exceeded Eternity to activate on a frontline allied unit if a Support Attacker assisting that team secured the kill with their attack. This is only a high-level view of how Chain works in those games, however. What's going under the hood is if any other attack besides the player main/assist attack secures a kill while Chain/EE is active, Chain will activate on a frontline unit on the side of the entity that achieved the kill.

  - This definition is far more flexible and enables very silly situations to occur. For example, say I have a frontline unit that cast Chain attack the enemy. If the frontline unit's attack doesn't kill but the enemy's counterattack kills the player frontline unit, Chain will activate and give an extra turn to the ENEMY unit instead. A similar scenario can also occur if an Enemy Support Attack kills the player frontline unit with Chain applied.

  - This is obviously a bugged scenario, so an extra check was added in the Switch/Steam versions to disable Chain from activating if the attacker achieving the kill was categorized as an "enemy". Unfortunately, this caused another bug with the original behavior for Chain. For some reason, player Support Attackers are categorized with the "enemy" property, meaning this new check is what disables Chain from activating on player Support Attackers.

  - Thus, all the mod does is remove the Switch/Steam check to allow Chain to activate like before. Granted, you can still encounter the enemy Chain activation bug, but this is done for now to preserve the original behavior until a better solution is created in the future.

- [Toggle|QoL] Display critical chance percentages in the damage calculation UI. This projected critical chance is calculated before dynamic battle updates from Prevail/power gains/buffs/spirits/etc.

- [Toggle|QoL] Display the enemy's base internal EXP/PP/Points values rewarded after a kill in the unit status screen. The new UI element restores the previous display for rewarded PP and Points as shown in FMW4, with the additional bonus of also displaying EXP now.

  - Utilizing this will make routing more convenient; the player will have a more comfortable time planning out resource building against enemies without needing to consult the internal files.
 
- [Number|Visual] Change the appearance of UI buttons that are displayed in various menus. The following styles are available for selection based on the controllers the game recognizes using the Steam Input API:

  - Default (0): Displayed buttons change depending on the connected controller.
  - PlayStation (1): PlayStation controller buttons.
  - Switch (2): Switch controller buttons.
  - Keyboard (3): Keyboard keys as buttons.
  - ABXY (4): ABXY controller buttons.
    - NOTE: The Keyboard option displays the default Q and W keys in reverse; the key displayed for Q is actually activated by inputting W, while inputting Q activates the key for W. This also applies to the 1 and 2 keys. The reversed displays require an internal EXE sprite fix for the sub-image ordering. At the moment, this is not prioritized, but it may be fixed in the future.

- [Toggle|Visual] Restore functionality to display the foreground effects in battle animations using the effect filenames defined in the `fg_ground` and `fg_sky` data columns in Data_Stages. Requires the battle foreground effect files hosted on Gamebanana under the mod title "Restored Chapter Map/Battle Foreground Effects". Requires LayeredFS to be enabled to load the files in `modData/data7`.

- [Toggle|Visual] Restore functionality to display the foreground effects in chapter maps. Requires the chapter map foreground effect files hosted on Gamebanana under the mod title "Restored Chapter Map/Battle Foreground Effects". Requires LayeredFS to be enabled to load the files in `modData/data7`.

## Personal Skills
### [RESTORED|Utsuho|FMW4] Solar Reactor (FMW4)
```
When unit's limiter is released, increases unit's max Power by 50 and grants the ability HP Regen (M).
Learn Level: Lv. 1
```

  - This PS also has a legacy bug fixed where previously Utsuho's max Power could revert after a quicksave load. This happened if her current Power was updated through any other means (Enemy kills, for example) before the Solar Reactor PS effect had been initialized. With the previous implementation, Solar Reactor would only be initialized if Utsuho was selected with the cursor on a chapter map. Now, the fix initializes the Solar Reactor PS during the reload routine to ensure it is not missed before any Power updates occur.

### [RESTORED|Byakuren|FMW4] A Superhuman Beyond Superhuman
```
Max Power increases by 10 each time the Superhuman transformation is used.
Max Power increase is capped at 60.
Learn Level: Lv. 50
```

### [RESTORED|Hina|FMW4] Hidden Nagashi-bina (Original)
```
Casts Persist and Luck on unit. (Usable 2 times.)
Learn Level: Lv. 56
```

### [RESTORED|Mehko|FMWCB] Super Static Shock (Original)
```
Adds the MAP weapon variant of Thunder Ram to unit.
Learn Level: Lv. 15
```

### [RESTORED|Makura|FMWCB] Towards the Future
```
Casts every Spirit in the game on this unit, with some exceptions. (Usable 1 time.)
Normal Makura Learn Level: Lv. 80
Final Makura Learn Level: Lv. 1
```

## Bug Fixes
- For the FPM Text Color mod, replace the hardcoded text with a function call to fetch the "Full Power Mode" text from `Data_Text`. Linking this text field to the FPM text entry in `Data_Text` allows for better maintainability if the original "Full Power Mode" text needs to be changed.

- Extend the `//` control character sequence to apply to other text fields loaded from the `data4` and `data5-X` data files, including dialog files. For context, in `Data_Text`, the game's text parser attempts to replace every instance of `/` with a comma instead. Because of this, double `/`'s will turn into a set of 2 consecutive commas and not `//`; thus, this normally prevents forward slashes from being displayed in the text fields for `Data_Text`. To solve this, an additional statement was added that converts the `,,` character sequence into a single `/`. This means the double forward slash sequence could be used to display a single forward slash in this way: `//` -> `,,` -> `/`.

  - This special handling was only implemented in `Data_Text` and was not extended to any other data file. The code fix now applies this text handling to every other data loading routine to restore displaying 1 or more forward slashes in various text elements throughout the game.

    - For example, this fixes certain double-comma character sequences left in certain files, such as `Data_Skills.txt.` Originally, Yorihime's Okuninushi PS and Kurumi's Break the Sabbath PS were written to use the `//` character sequence to display a single forward slash in the PS description. Unfortunately, the handling for the `//` sequence did not exist in the loading routine for `Data_Skills`, meaning the double-comma character sequence would remain in the description instead. After extending the text handling fix to other data file loading routines, this text bug no longer appears for existing files that previously used the `//` character sequence.

    - This also includes a fix to ensure all `/` control char instances in text are always replaced with a comma. For context, some lines in the game that use this control char only replace the 1st instance of `/` with a comma. This occurred in certain team names like Sanae and Tenshi's team name: "Heaven, Earth, Man" was displayed as "Heaven, Earth/ Man" due to the faulty logic in the special text handling. 

- Bound item name text length to 160 pixels when displaying items in the Intermission Equip screen. The item name should no longer overflow outside the UI textbox; specifically, the text displaying "Bullet Branch of Hourai" should now stay within bounds.

- Bound weapon name text to 390 pixels in the Unit Upgrade screen to prevent it from overlapping with the Weapon ATK text. For example, "Profound Danmaku Barrier -Phantasm, Foam, and Shadow-" should no longer bleed over into the Weapon ATK column.

- Fix the miscalculated page index for the default page that is set in the PS Levelup screen. A previous modding feature expanded the PS Levelup screen UI to accommodate more PSes beyond the max of 6 in the vanilla game. This was done by adding paging logic that would organize the Personal Skills into viewable chunks of max 6 Personal Skills per page.

  - When a new PS is learned during a chapter map and the game transitions to the PS Levelup screen, the paging logic is supposed to set the default page to the one that contains the newly learned PS. However, this default paging logic was bugged in retrieving the numerical position of the PS in the character's skillset. Instead of searching from the list structure for the character's skillset, the bugged logic performed a search from the internal `Data_Skills` database instead and fetched a position there to calculate the default page. This led to the game displaying blank pages containing no PSes in the PS Levelup screen, and the player had to manually tab through the pages to see the rest of the character's PSes. Naturally, the fix makes the paging logic search through the actual skillset and return the correct position that's used to calculate the default page.

- Fix `Data_Specials` addOns replacement logic failing to replace VAL2 fields due to an incorrect set of calls appending to the internal lists instead of replacing at a given position. Credits to Mukyuuri for the fix.

- The following include addOns fixes for replacement. These will change the current method of Line Number replacement for your existing addOns that fall under the `Data_Bonus` and `Data_Updates` categories. You will need to update the `LineNumReplace` fields for these addOns if you have existing changes. `data_unit_all` and `data_weapon_all` are not affected because they replace by unique IDs instead of Line Number. Credits to Mukyuuri for catching these bugs so that I could figure out a fix.

  - For `Data_Bonus` addOns, apply an offset of -2 during replacement so that the `LineNumReplace` field can 1:1 match the actual Line Number as seen in a text editor without replacing the wrong entry. Before, `LineNumReplace` was treated as 0-indexed and it was assumed that the vanilla `Data_Bonus` loading routine was 0-indexed as well. Unfortunately, this wasn't the case as the vanilla routine actually starts counting from 1 instead. This would normally only offset the line numbers between the `Data_Bonus` addOns and the vanilla `Data_Bonus.txt` file by -1, but because the 1st file header row is skipped during loading in the vanilla routine, the offset increases by -1, making the total offset -2. The `Data_Bonus` entry at Line Number 2 would correspond to index 0, Line number 3 would correspond to index 1, and so on and so forth. Thus, the offset lets the written `LineNumReplace` correspond to the actual index number used in replacing an entry in the internal data structures for `Data_Bonus`.

    - TL;DR: Use the actual Line Number in `Data_Bonus` as displayed in a text editor when deciding to replace entries. There's no need to worry anymore about being off before replacement.

  - For `Data_Updates` addOns, apply the same `Data_Bonus` -2 offset fix for replacement through the `LineNumReplace` field. This was also another data file where replacing through addOns using `LineNumReplace` wouldn't 1:1 match the Line Number in the `Data_Updates.txt` file. Use the same guidance above to replace without worry about being off.
    - The `addOns/data5-4/Data_Updates/LettyFriendshipUpdateFix.json` has been updated to make the `LineNumReplace` field match the correct Line Number in `Data_Updates` to fix Letty's Friendship values. Remember to replace this file with the updated version in the repo.

  - For `data_unit_all` addOns, apply a +1 offset during replacement to account for the existing internal lists being 1-indexed instead of 0-indexed. The vanilla routine starts adding entries into the internal lists starting from position 1, instead of position 0. This meant the previous addOns replacement logic would be off-by-one due to assuming the internal lists started counting from 0.

  - For `data_weapon_all` addOns, fix replacement bug where the internal data structure used for mapping UnitID to its current position in the list of UnitIDs had the current position constantly incremented after each row was parsed in the vanilla loading routine. Multiple `data_weapon_all` entries can have the same UnitID but different WeaponIDs, so incrementing the UnitID position after each row-parsing will give incorrect values for the actual position of each UnitID in the UnitID list. This could overwrite weapon lists in other unrelated units after the replacement logic finished.

    - The UnitID to UnitID position mapping is now fixed to only update when a new UnitID is added to the list during the vanilla loading routine. This way, the replacement logic can properly search for the right UnitID using the correct positions in the mapping to replace the intended unit's weapons.

- Fix `Data_Bonus` addOns being added to the internal lists in reverse order. Before, each JSON item in the `addOn` JSON array was always inserted at the beginning of a Chapter ID group. Because the items in the JSON array are parsed sequentially, the order in which the items appear in the internal lists will be reversed. Say I have the following JSON items to add: A, B, C, and D, in that order. For simplicity's sake, let's say they'll be added at the beginning of the internal list. Now, the following visual shows how they'll appear in the internal list after being processed at each step. (X is a placeholder for other values.)

    1. No Add
    - JSON items: [A, B, C, D]
    - Internal List: [X]

    2. Add A 
    - JSON items: [A, B, C, D]
    - Internal List: [A, X]

    3. Add B
    - JSON items: [A, B, C, D]
    - Internal List: [B, A, X]

    4. Add C
    - JSON items: [A, B, C, D]
    - Internal List: [C, B, A, X]

    5. Add D
    - JSON items: [A, B, C, D]
    - Internal List: [D, C, B, A, X]

      - As you can see, because the sequential JSON items are always added at the beginning, the order will never match how they were constructed in the addOns JSON. This is an issue as certain `Data_Bonus` entries rely on ordering to initialize certain actions before executing others. For example, an entry with `INIT_CHAR` is used to initialize character data for new units, while `SET_SKILL` is used to set a specific PS for an existing character. `INIT_CHAR` needs to happen before `SET_SKILL` when both are applied to the same character; otherwise, `SET_SKILL` will fail since the character hasn't been initialized yet if performed before `INIT_CHAR`.

      - The fix now maintains order when adding new entries from `Data_Bonus` addOns by tracking the current position of the JSON item in the JSON array, then using that position as an offset when inserting into the internal lists.

- Finally, refactor Data_Bonus addOns loading routine to replace chapter entries 1st, then append remaining chapter entries afterwards to fix loading routine bugs. There was a previously missed consideration for this addOns routine: Any appended entries would shift the position of elements in the internal lists. Since addOns replacement for `Data_Bonus` relies on the line number/list position in respect to the original, unchanged file, shifting the elements would displace the addOns replacement and cause it to erroneously replace the wrong entries. Now, the fix performs replacements during the 1st pass of the addOns and saves a "checklist" of actions/properties to append later. After this 1st pass, the new routine then iterates through the checklist of appends to execute to finish the addOns routine. This ensures both replacements and appends are stable when loading `Data_Bonus` addOns. 

- Fix bug where frontline dialog in battles that included a generic assist attack animation (AKA one that does not have an existing `demo_sub` animation in the EXE) did not play the assist attack dialog and instead played the FPM frontline attack dialog. Previously, there was logic implemented to play backline assist attack dialog for backline units with generic assist attack animations. However, this logic was not extended to the frontline dialog selection, meaning the game would fallback to playing the FPM frontline attack dialog for frontline units paired with units with generic assist attack animations. The fix now covers the frontline case and also choreographs the frontline unit sprite to move with the same frame timing transitions as non-generic assist attack animations.

- Apply global flag to disable opening the GlobalMenu when set to true in various UI screens. This global flag is always reverted to false when the game is soft reset to prevent locking the player out from the GlobalMenu permanently. This fixes unintended scenarios where the GlobalMenu could be opened at inconvenient times, namely during the custom army name prompt where the player could input text from the keyboard.

- Remove redundant check that used to determine whether to display Straw Doll Kamikaze's multipliers in the damage calculation UI by checking the final damage value. SDK is no longer dependent on a hacky solution using the final damage to display the multiplier, so this logic is now removed.

- Simplify drawing logic for text/numbers used in the final damage display and expanded damage calculation UI mods. The `Main`, `Assist`, and `Support` headers are now right-aligned to draw from the same x-position, instead of previously adjusting the x-position based on English text length. The final damage number no longer uses logic to determine where the number should be aligned based on the text length; it is now drawn right-aligned from the same starting x-position as the numbers displayed in the Total Damage Multiplier.

- Bound Manual header item text to 210 pixels to prevent it from overlapping with the rectangular box. The text `Battle (Unit-Specific)` should be shortened accordingly to fix overlap.

- Add missing accuracy/damage/weapon availability function calls in the Spirit casting routine for Spirits located in the `Others` menu. In vanilla, casting Spirits in the battle info screen through the `Others` menu only updated the accuracy rate calculations for the frontline and backline of the player team. This meant the following issues could occur.

  1. Damage calculations wouldn't be updated. For example, casting Trust on a low HP unit with Prevail could result in misleading predictions. This could even result in a kill since the damage indicator would not properly update with the lowered additive armor bonus from Prevail.

  2. Weapon availability wouldn't be updated either. Take the enemy phase for starters. As enemy phase Spirits are now available in CB and beyond, you can restore HP, MP, and Power before counterattacking. You may find yourself lacking MP or Power to select certain weapons, so you cast Devote, Renew, Rouse, or Love. Unfortunately, because there are no calls to the function that re-checks and refreshes weapon availability, those weapons will remain unselectable even if you meet the conditions to use it normally. 

      - The missing accuracy/damage/weapon availability function calls for the player's frontline/backline/support units and the enemy's frontline/support units are now added to the Spirit casting routine through the `Others` menu. This should fix the aforementioned bugs in the previous section.

- Clear damage calculations for an enemy Support Attacker if the frontline player unit uses Fury to disable enemy Support actions. During enemy phase, the frontline unit can cast Fury to disable any enemy Support Attackers that are queued in the battle info screen. This was only discovered recently, so the previous expanded damage calculation mod hadn't taken this into account. Now, the damage calculations are cleared as expected after Fury is cast in this scenario.
  - Demo of this scenario with Fury in action: https://www.youtube.com/watch?v=zUbyWMofR8E 

 - Fix text coloring for expanded damage calculation UI to be set to gray color if no calculations exist and final damage = 0 for a given position. Previously, the condition for coloring the text was not strict enough; the text could still be drawn in gray if there were no calculations but final damage was more than 0.

- In the MAP status screen, fix the text extraction bug for the text next to `Area of Effect`, where it would always default to the blank text `------`. Previously in Doujin CB, that text field would slice a portion of text from the "Properties" section that described the Area of Effect. For example, "Centered on Self", "Targeted", and text ending with "-shaped" are supposed to display in that field. The game has logic to determine how much text to copy from "Properties" by extracting the text from the beginning all the way to the end of a designated "text end marker". Unfortunately, the marker in the ENG localization suffers from two issues. First, in the `Data_Text.txt` file where internal names are mapped to text, the marker has the same internal name mapped to 2 different display names.

```
weapon_type,Shape
weapon_type,Type
```

  - Because the entries are loaded in order, only the text name "Type" is mapped to the internal name `weapon_type`. "Type" is actually displayed in the weapon status UI to describe weapon attributes like Post-movement, Laser, etc., but the same "Type" text is used as the text end marker for copying over the MAP Area of Effect. There are no MAP attacks that include the case-sensitive word "Type" in "Properties", so by default, the game always displays blank text in the AoE text field as a fallback. Even if the internal name was mapped to "Shape", this still would be bugged since the actual marker used in the English localization is "-shaped". In addition, the marker logic doesn't include fetching text like "Centered on Self" and "Targeted", so MAP attacks with those descriptions will also default to displaying blank AoE text.

  - The fix for this creates a new set of `Data_Text` addOns that properly define the actual text end marker "-shaped" and include the other AoE range cases like "Centered on Self" and "Targeted". The marker logic is also rewritten to accommodate these new cases and bound the text display in the MAP status screen to prevent overlap with other text.

  - Remove the previous modding change to fix an invalid chapter ID bug after completing the Dream Again 3 chapter. One of the changes from vanilla 1.2.6 implements a default fallback for setting up deployment slots to load units in the Intermission. If the game encounters an invalid chapter ID, it will execute this fallback to prevent the player from entering an invalid state for deployment slots. Thus, saving the game after finishing DA3, then reloading the save will no longer crash the game. By extension, the fallback also solves the problem for previous saves that were softlocked due to this bug; because there is now handling for invalid chapter IDs, those saves can recover to a stable state for deployment slots and loaded units.
 









