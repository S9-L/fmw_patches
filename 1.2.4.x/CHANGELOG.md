# 1.2.4.2 JPN Release
## Features
- Released 1st modding patch for the 1.2.4 JPN version.
- The `FMWCB-1.2.4.2-JPN` patch and future patches will have feature parity with the modded ENG version. However, at this time, certain text elements and dialog may still appear in English because they were initially created for the modded English version.
  - These include, but are not limited to:
    - Various battle dialog like the restored Kedama/Evil Eye lines
    - UI textboxes/info
    - Personal Skills
    - and more
- I am not fluent in Japanese, and I would rather not machine translate text into another language that I cannot personally verify. In future updates for the JPN modded version, I will gradually move internal string references from the binary into the `Data_Text` addOns to make it easier for more qualified JPN localizers to translate.

# 1.2.4.2 Release
## Major Features/Tool Releases
- The Fantasy Maiden Wars Save Manager tool has been released, allowing any player to modify and fine-tune their local Steam/Switch save files to their liking. Download the release from this new GitHub repo: https://github.com/S9-L/FMWSaveManager

- The "NG+ Freeplay" Carryover feature is now available in this modding version. In the NG+ unit carryover selection screen, a new option titled "Carry Over All Units" will allow the player to bring every unit from the vanilla base game into NG+ as if they were part of the 6 units selected for the ordinary NG+ unit carryover. As a bonus - Hourai, Shanghai, Zenki, and Goki are also included in the Full NG+ Carryover without needing to bypass unit selection flags through other modding means.

  - Additionally, after selecting your carryover units, a new menu screen will pop up and ask the player what resources they would like to carry over. You can choose the following resources to retain their current + carryover values for the next playthrough: Points, Ex-Points, Items, Character PP, and Character Kills. Any resource that is not selected will be reset to 0 or their default values.

- The FMW Community Saves repo has been updated with pre-crafted saves for Steam/Switch that carry over all units for NG+ and reset almost all resources to 0 for a fresh start. These work on both vanilla and modded versions of the game. Look into the "SQ-L" folder in the save repo: https://github.com/S9-L/fmw_community_saves

  - These saves are also split into two versions: The 1st where units start with their initial learnset of PSes in a NG+ playthrough, and the 2nd where units have all their PSes unlocked regardless of level and event restrictions.

  - For these saves, the starting chapter is set to the 2nd chapter of either route, since it's the earliest that a save file can be created. The 1st chapter's clear records are configured for a 1-turn clear on Lunatic with the bonus achieved. This can be changed through the save manager, if desired.

- Implement addOn support for `Data_Bonus`, `Data_Updates`, `Data_Trust`, `Data_IniPos`, and `Data_Sprites`. Remember to remove the dummy addOn files in the previous addOn folders to prevent crashes from invalid files. In addition, you should remove the `Data_States` and `Data_Text` dummy addOns from previous installations, then replace them with the new addOns for `Data_States` and `Data_Text` in this release to clean up previous placeholder addOns.

  - `Data_Bonus`: This internal file controls event triggers/resource gains/notifications/unlocks on certain chapters. For example, adding new records can allow a character to gain new weapons or abilities after a chapter is completed. NOTE: If you want to replace any previous row in the file by implementing a new addOn, you will need to specify the Line/Row number for that row so that the previous row can be successfully replaced. This is required due to the way the file is read during startup.

  - `Data_Updates`: In general, this file determines how and when unit/character versions should be updated, according to the chapter ID number. The game attempts to update the intial unit/character versions from the ID0 columns into the final unit/character verions in the ID1 columns. The addOns system will quite useful for controlling these updates; for example, you can define new addOns that update a custom character on specific chapters without needing to hardcode new rows in the original `Data_Updates` folder. Due to the way this file is read, the addOns for this will also require specifying the Line/Row number of the original file for a successful replacement. 

  - `Data_Trust`: This defines the Friendship and Revenge Value pairings for specific character versions. The addOns format is fairly simple; add the CharID of the character you want to add Friendships/Revenge Values to, then specify an array of character IDs without the 2-digit suffix that will give Friendships/Revenge Values to the original CharID. Example: `"CharID":"Yugi01","Chars":["Suika","Parsee","Kaguya"]`. Then, in pairwise fashion, you can create two other arrays for the `TrustVals` and `RevengeVals` fields that contain the actual Friendship and Revenge Values, respectively.

  - `Data_IniPos`: This file designates the initial starting positions for deployment slots on chapter maps. The x and y coordinates give the pixel position of the top-left corner of a deployment slot square tile. To convert these "pixel coordinates" into the actual square tile positions, divide the x and y coordinates by 16, and you'll get the x and y positions that are offset by square tiles instead of pixels. The Group column is used for special clusters of deployment slots, like reinforcement positions, and the PosID column determines numerical order of the deployment slots that appear on the map.
 
  - `Data_Sprites`: Finally, the `Data_Sprites` file contains records that the game matches to UnitIDs to find what sprites to display for Ace rankings and enemy spellcard/FPM poses in the battle info screen. To implement the addOn correctly, you will need to add your custom FPM/spellcard pose/Ace sprites in `modData/data15` to be loaded through LayeredFS, and they should follow this filename pattern: `<BASE_UNITID_WITHOUT_2DIGIT_SUFFIX><DATA_SPRITES_TEXT_ENTRY>.png` (i.e. `Alice_HAce1.png`, `Alice_HAce2.png`, `Alice_HAce3.png`, and `Alice_HFPM.png` would work for Ace + FPM sprites). Once this is done, you can modify this sample addOn with your actual custom UnitID and the game should display the `modData/data15` sprites properly:
  ```
  {"Data_Sprites":{"Active":true,"AddOn":[{"Enabled":true,"UnitID":"Alice_H","AceVals":["Ace1","Ace2","Ace3"],"FPM":"FPM","AtkVals":["","","","","","","","",""]}]}}
  ```
- Extend the damage calculation UI to display stats for the main, assist, and support attack positions for the player and enemy. In addition, the Friendship damage bonus/penalty can be shown in the `Final Modifiers` section of the UI. Finally, the projected final damage total can also now be displayed in the UI; this number is calculated before any dynamic battle updates such as reactions/critical hits/temporary spirits or buffs/power gains/etc. These display options can be enabled through the newly added JSON mods that control these features.

- Add Debug Menu option + JSON mod to fully unlock all Personal Skills and Spirits for all characters in the current army, regardless of event flags/level restrictions. The Debug Menu option to unlock all PSes can potentially cause an irreversible change: Saving the game after the Intermission has been reloaded with the full PS unlock will permanently add all new skills to each character. On the other hand, enabling the JSON mod to fully unlock all Spirits will not overwrite the status of characters' Spirit sets, so this JSON mod can be toggled on and off as needed without permanent consequence.

- Implement animation pauser tool, enabled through a JSON mod feature flag. The battle animations can now be paused and advanced at the player's discretion. This will be useful for animation debugging/setting choreography, as well as capturing certain moments in animations for screenshots, thumbnails, ~~Keine's physics~~, and more.

- Bonus stat tracking has been restored + added for certain units/actions. These will appear during the ending sequence for Route A/B, and are reset at the start of every NG+ playthrough. The following stats have been restored/added:
  - General: Number of Vegetable Items eaten
  - Aya: Number of Photos Taken using the "Danmaku Photography" MAP attack
  - General: Number of Dream Spirits cast by characters
  - Toyohime: Number of times the Wave Guider Fan regular + MAP attack was used
  - Mehko: Number of Sheep Counters used for her Personal Commands
  - Makura: Number of times the Sweet Dreams attack was used
  - Akyu: Total points accumulated from performing certain actions that go towards unlocking Akyu as a fieldable unit
  - Lily: Total points accumulated from performing certain actions that go towards unlocking Lily Black as a fieldable unit

- General clean up and polishing of UI/UX
  - Add UI background behind the text for the Friendship Status QoL mod.
  - Redesign Reaction Status QoL mod to display a new background UI element that shows the parry/shield defense icons instead of text for those reactions. The Counter reaction display now uses an arrow icon instead of text. The calculated chance text is also updated to use the same font as the text used for HP/MP/Lv displays.
  - Add instructions about the controls on the Debug Menu SLG-1 page to initiate a forced Game Over or Chapter End. Additionally, this can now be done when the cursor is hovering over any option, as opposed to the previous behavior that disallowed these controls when the cursor was on the Confirm option.
  - Debug Menu now gracefully exits back to the global menu instead abruptly disappearing and kicking the player back to the chapter map/Intermission.
  - Debug Menu cursor now defaults back to the initial top "0" position after backing out or confirming options.
  - Debug Menu should now add points, PP, WP, and kills up to the current maximum without failing to update if the current value to add to would exceed the maximum.
  - Bound the Library menu text length to 242 pixels so the text is bounded within the textbox. 

- Implement SS Unit Terrain Rating for Night terrain. In the vanilla game, there is no logic that boosts unit terrain ratings through an SS rating in Night terrain. This can now be added to units and is one of the features included in a restored FMW2 PS for Kurumi.

- Implement a new EF field type for `Data_Skills` addOns called `COMPAT2+` that supports adding multiple unit terrain ratings at once. To utilize this, you can provide a comma-separated (or commas replaced with `/`) list of updated terrain ratings and internal terrain identifiers surrounded by the `|` character in the VAL1 and VAL2 fields. Here's a quick example using the Quake Kick (FMW2) PS addOn:
  -  `"EF":"COMPAT2+"`
  -  `"VAL1":"|1/0|"`
  -  `"VAL2":"|SS/B|"`
    - This will set the unit's Land unit terrain rating (identifier: 1) to SS rating and the Air unit terrain rating (identifier: 0) to B rating.
      - The internal identifiers (enums) for terrains follow a 0-indexed order:
        - Air - 0
        - Land - 1
        - Water - 2
        - Night - 3   

- Restore Strike/Grit Spirit names used in older fan-translations through 3 `Data_Spirits` addOns, replacing Bullseye/Persist, respectively. To enable this, set the "Active" field to true for the `Restore_GritName`, `Restore_StrikeName`, and `Restore_StrikeGritName_Courage` addOns.

- Restore the "Shiver" FMW1 Spirit (internal name: `SENRITSU`). Effect: Reduces the Power of all enemies by -10. The repo has been updated with a new `Data_Spirits` addOn that implements Shiver; all you'll need to do is update a character's spirit learnset with Shiver's internal name + custom learn level in the `data_char_all` file or addOn. 

## JSON Mods
- [Toggle|BugFixes] Fix Stale Entity Attack Manipulation bug by safely handling the front unit pointer when entering the unit spirit menu from Spirit Search. This is a relevant bug caused from removing the team swap action that occurred if a backline unit's spirit was selected from the Spirit Search menu in the original games. Because the update logic to the front unit pointer wasn't changed to accommodate the swapless scenario since PC CB, the rear unit ends up duplicating to the frontline when entering the battle info screen. The bug fix now handles the swapless scenario, and properly sets the front and rear unit pointers to fix the stale unit references.
  - For a simple and effective visual demonstration, please take a look at this video: https://www.youtube.com/watch?v=f5i0pAN8wQM

- [Toggle|Debugging] Disable auto leveling for characters already present in the unit roster when normally progressing through the game, advancing chapters through the Debug Menu Stage Select, or loading saves while the Debug Menu is enabled. Newly added/initialized characters will still be auto leveled according to the respective chapter number.

- [Toggle|Debugging] Enable the animation pauser during battle animations. This mod uses a blocking loop to force the game to wait; until the animation is unpaused, the game window will appear unresponsive. Even if the game window is unfocused, keyboard control inputs will still apply in the animation pauser.
  - Keyboard Controls:
    - P - Pause the current battle animation.
    - O - Unpause the current battle animation.
    - Down Arrow - Advance the battle animation as long as the key is held
    - Up/Right Arrow - Alternate between the two keys to advance the battle animation frame-by-frame
    - Left Arrow - Advance at 60 FPS

- [Toggle|Debugging] Skip chapter summaries during Arc Ending sequences. Press the A button to advance the Arc Ending sequence if this mod is enabled. This should let you quickly advance through the ending sequences without having to wait for all graphics and chapter summaries to slowly scroll through.

- [Number|FileSystem] Modify the max number of saves that the game will scan up to in the save folder. Restart the game for the updated max saves to apply in the Save/Load UI (Set to 4 for default max of 200). Minimum value:4, Maximum value:1000.
  - NOTE: The game will take longer to load on startup if you keep increasing the number of saves your save folder. This is because the startup sequence scans through all save files, validates them, and then records the save file metadata to display whether these files are valid/corrupt when the user enters the Save/Load UI. It's recommended that you utilize this mod alongside the ChangeSaveLocation JSON mod to organize your files and keep loading times at a minimum.
 
- [Text|FileSystem] Change the folder location where the game will scan and read saves from. Restart the game for the updated save location to apply (Default save location name is savedata/). Due to the GMS sandbox, the save folder must be located within the APPDATA/fmw_dosd folder to have writeable permissions.
  - Don't forget to add the `/` at the end of your input so the game correctly interprets it as a folder path.

- [Toggle|Mechanics] Enable Time Paradox/Re-Attack to activate in the backline of a team. This restores the previous behavior of these PSes, present in versions 1.0.4 and earlier in the original FMW3.

- [Toggle|Mechanics] Restore the activation condition that allowed Rei'sen's All-Out Shootout to persist in buff duration and only consume 1 Ammo in the backline, while giving her the full boost from the PS. This mechanic is now restored to match the previous behavior in the original FMW4.

- [Toggle|Mechanics] Restore tracking Game Overs throughout chapter attempts. Currently, the internal logic forcibly resets the Game Over counter every time a chapter is restarted after fulfilling the defeat condition. This mod disables the reset and allows the Game Over counter to increment as expected.

- [Toggle|Mechanics] Restore the old WP condition rewards from the original games. After enabling this mod, the game will revert to giving +5 WP upon clearing the Bonus Condition for a chapter, instead of giving 10000 Points. This will be added on top of the base result of +10 WP after normally clearing the chapter. If the Game Over restoration mod is enabled, no WP will be gained upon completing a chapter if it has been replayed after at least 1 Game Over, as in the original games.
  - In addition, this mod is paired with another `data5-4/Data_Text` addOn named `Restore_WPMessage` that corrects the Bonus Condition clear message with the reverted WP reward. There are two entries in that addOn to choose to enable, depending on whether you'd like to display the "WP" term or the "EX-P" term.
 
- [Toggle|Mechanics] Average Team-Up attack weapon upgrade values among the partner units participating in the attack, like in PC CB and the original FMW games. For example, if Reimu has 6 weapon upgrades, then a 2-unit attack like Trichromatic Lotus Butterfly would only be boosted by an equivalent 6/2=3 weapon upgrades when the averaging logic is applied.

- [Toggle|Modifiers] Bypass chapter transition checks to force the game to always enter the Route Selection event after completing Chapter 70. This enables the player to enter Route B even on a fresh NG0 playthrough. Certain units like Mehko and Makura that are only available in NG+ will be initialized after the player enters Route B on a NG0 playthrough. Additionally, for a NG0 playthrough entering Route B, the game will update all units to their latest unit/character versions, just like in NG+. This may also affect item distributions and Points/WP/PP resource gains, so back up your saves accordingly.

- [Toggle|Modifiers] Restore stacking multiple Mystic Memory equips to reduce SP costs. To update the UI in the Intermission, you will need to change equipment or reload the game after this mod flag has been modified to update SP costs.

- [Toggle|Modifiers] Enforce capped unit upgrade levels determined by each arc. This applies even on NG+, where the unit upgrade caps normally default to 10 levels. These are the following unit upgrade level caps in each arc.
  - Scarlet: 5 levels
  - Mystic: 5 levels
  - Eternal: 7 levels
  - Dream: 10 levels
 
- [Number|Modifiers] Override the character level cap (Set to 0 to restore default level caps by arc). Reload your saves for the updated level cap to apply. Minimum value:0, Maximum value:99.

- [Toggle|Modifiers] Fully unlock all Spirits for each character regardless of level/flag restrictions. Reload the Intermission/saves while flag is modified for unit spirit sets to update. This does not permanently overwrite characters' spirit sets, so the flag can be toggled on and off as needed.

- [Toggle|Modifiers] Disable the internal logic for strictly checking certain Personal Skill effects in the 8th skill slot. This will allow certain PSes to apply their effects even when set as a general skill.
  - This will be useful if you're adding PSes in the 7 other skills slots using the save manager.
  - NOTE: Certain PSes are hardcoded to only work for specific characters. In those cases, EXE editing would be required to remove the hardcoding to apply the PSes to all characters.

- [Toggle|Modifiers] Disable the internal logic for updating unit/character versions according to the internal `Data_Updates` file. The logic consecutively updates an entity according to each chapter record in the file up to the current chapter. Because the internal update logic is disabled,you will need to directly modify the entity's UnitID and/or CharID to change the entity's properties.
  - If you want to prevent the game from automatically updating your units/characters data, you can enable this mod. This way, you can use the save manager to change the UnitID/CharID to whatever you'd like for trying out different unit/character versions.
    - As a side note, the save manager could be used to fix vanilla bugs such as the Reimu/Marisa Route B form availability bug. You can edit their UnitIDs to revert to their expected final forms with True Trichromatic Lotus Butterfly.
   
- [Toggle|Modifiers|Experimental] Enable Full Power Mode to be available in all chapters of the game. As long as a team reaches at least 150 Power for both front and rear units, FPM will activate for that team regardless of chapter restrictions.
  - This is an experimental mod since it has not been rigorously tested. More user/anecdotal testing is needed before integration into the standard JSON mod suite. 

- [Toggle|Modifiers|Experimental] Enable pairs/teams to be available in all chapters of the game, including the FMW1 and FMW2 Arcs that normally allow only single units to be deployed per slot.
  - Likewise, this is also an experimental mod due to limited testing results. This may result in more unexpected bugs/scenarios than the FPM mod due to the 1st two arcs not being designed around teams, and so more user/anecdotal testing is definitely needed.
 
- [Toggle|QoL] Display the damage dealt/taken bonus from the Friendship mechanic in the damage calculation UI. This can be enabled independently from the other damage calculation UI mods.

- [Toggle|QoL] Display damage calculations for main, assist, and support attack types. The damage calculation UI will now include multiple pages that contain each calculation on player and enemy sides. This can be enabled independently from the other damage calculation UI mods.

- [Toggle|QoL] Display projected Final Damage number in the damage calculation UI. As mentioned before, the projected damage is calculated before dynamic battle updates, so the final damage may differ from expectations. This can be enabled independently from the other damage calculation UI mods.

- [Toggle|Visual] Revert to displaying WP instead of Ex-P/EX throughout various hardcoded text elements in the EXE. This mod is also paired with a `data5-4/Data_Text` addOn named `Restore_WPName`, that replaces the remaining instances of the "EX"/"Ex-P" text with "WP". You will need to manually set that addOn's `Active` field to true to enable those replacements.

- [Toggle|Visual] Disable movement animations for the small unit/icon sprites in the Intermission + [Toggle|Visual] Disable movement animations for the small unit/icon sprites in chapter maps when the unit is set in Air/Land Terrain
  - This reverts the animated sprites to the statically displayed sprites in the PC CB version.
 
- [Toggle|Visual] Revert CB change to display MAP attack spellcard sprites as red. This will display all spellcard sprites as blue as in the original games.

- [Toggle|Visual] Toggle Private Square's animation between the version present in the original games vs. the generic Bunshin animation set for Sakuya in Switch/Steam CB.

- [Toggle|Visual] Display bonus stats during the game ending sequence. In addition, this mod restores tracking these stats through various actions in-game. Check the features section above for the bonus stats that have been added/restored.

- [Toggle|Visual] Restore displaying and tracking quicksave loads as in the original games. The "Loads" counter will now track the quicksave load button combo during a chapter, turn-by-turn loads from the chapter map menu, and finally a presumptive load when the game is closed and the player later resumes from the title screen or through the button combo.
  - The Loads/Total Loads Counters will now be displayed during the end-of-chapter summary as well as the game ending sequence, respectively.

## Personal Skills
### [RESTORED|Generic|FMW4] Safe Spot L1/2
```
If the enemy does not counterattack, increases damage dealt by +10% (+20% at level 2).
Does not apply to support or assist attacks.
```

### [RESTORED|Komachi|FMW2] Slacker (FMW2)
```
Unit gains HP Regen (L), but reduces her EXP and PP gain by -50%.
Learn Level: Lv. 15
```

### [RESTORED|Meiling|FMW2] Quake Kick (FMW2)
```
Sets unit's Land terrain rating to SS and Air terrain rating to B.
Learn Level: Lv. 25
```

### [RESTORED|Meiling|FMW3] Unyielding Spirit
```
If an enemy attack will reduce their HP to 0, the unit will survive with 10 HP.
(1 uses.)
Learn Level: Lv. 30
```

### [RESTORED|Kurumi|FMW2] Night Owl (FMW2)
```
Sets unit's Night terrain rating to SS.
Learn Level: Lv. 24
```

### [RESTORED|Mokou|FMW2] Phoenix Claw L1/2/3
```
Increases damage dealt by CQB weapons by +10/15/20%.
Decreases damage dealt by RNG weapons by -10/15/20%.
Learn Level: L1: Lv. 24, L2: Lv. 33, L3: Lv. 45
```

### [RESTORED|Shizuha|FMW2] Golden Autumn (FMW2)
```
Increases EXP gain by +20％, reduces damage taken by -10％.
Learn Level: Lv. 10
```

### [RESTORED|Rumia|FMW2] Is That So~ L1/2
```
When unit hits an enemy with an attack, enemy loses 2/3 Power.
Learn Level: L1: Lv. 30, L2: Lv. 50
```

### [RESTORED|Daiyousei|FMW2] Teleport
```
The unit can ignore movement penalties from terrain.
In addition, the unit can move through any other unit.
Learn Level: Lv. 41
```
  - As a bonus, this PS includes a new teleporting animation for movement, repurposed from the Connect Mountains to Sea warp animation.

### [RESTORED|Rinnosuke|FMW4] Inventory Usage
```
Unequipped items can be selected and used on the ship. Each item can only be used once per stage. (Usable 2 times.)
Learn Level: Lv. 45
```

## Bug Fixes
- Improve Straw Doll Kamikaze's unique doll count calculation in the animation initialization by scanning the map for viable Hourai/Shanghai units, instead of relying on an additive damage bonus dividend from the internal damage calculation for SDK's bonus damage.

- Fix FPM aura effects being removed in the Battle Info screen when casting a Spirit from units in the current team or from the `Others` group.

- For the Reaction Status mod, fix calculated shield defense chance displaying an incorrect inflated percentage due to pre-1.2.3's bugged code boosting Shield Defense chances for the enemy if Skill was invested for a player unit. The Shield Defense bug was fixed after the 1.2.3 patch, so this mod fix now utilizes that change for the calculation.

- For the Reaction Status mod, restrict displaying calculated Counter chance only when it's applicable on the corresponding player/enemy phase. For example, player Counter chances should only be displayed during the enemy phase, while enemy Counter chances should only be displayed during the player phase.

- Stop selection sound effect from being played twice when selecting the General or BGM option in the Settings menu.

- In the EX Bonus selection UI, fix the underline lengths for the `Fixed Bonuses` and `Select 2 Bonuses` headers to match up with the actual text length instead of a monospaced font width calcualtion.

- Fix missing selection sound effect in the Dream Spirit selection UI where navigating upwards and wrapping the cursor to the bottom of the spirit page doesn't play any SE.

- Fix orphaned ds_lists that were not deleted after use for loading `Data_IsIN` addOns.

- Fix code logic when loading `Data_Text` replacement addOns to immediately exit instead of proceeding to the rest of the code block.

- Fix `data_weapon_all` addOns incorrectly appending to Utsuho's weapon list and making Limiter Release-only weapons available in the base 3.5 form. To account for her vanilla hardcoded weapon list expecting a hardcoded weapon list size, there is now additional code added to distinguish weapon additions through addOns for Utsuho.
  - Weapon addOns that include the `HEAT` string in the "Effect" field will be designated as HEAT weapons that will only be made available in the Limiter Release form. All other weapons will only be added to the base 3.5 form.

- Bound skill name text length to 230 pixels when displaying skills in the Level Up UI. This should prevent skill names from overflowing outside the UI texbox.

- Properly handle the generic Assist Attack dialogue when using the FPM animation fallback for units that do not have implemented Assist Attack code animation scripts. The Assist Attack dialog no longer defaults to FPM dialogue, so you can now update your `dialog_meta` files to correctly separate your dialog groups to play only for Assist Attacks or only for FPM Attacks.

- Restore functionality for the missing DEL_ITEM update case that would delete items as defined in the records for the `Data_Bonus` file.
  - As a result, this fixes the Parasol item count overflow bug that occurs in the Mehko chapters by correctly deleting the Parasol item after finshing the chapter where it was previously used.

- Decrease text length bound for item names to 180 pixels in the unit status screen. This prevents item names like the Bullet Branch of Hourai and Unknown Seeds from overlapping with their respective item sprites.

- Fix instant, abrupt flash that occurs when the NG+ unit carryover screen displaying your 6 selected NG+ units fades into white to transition into the next playthrough. The flash is now properly timed within the fade into white after the shine effect animation fully plays out.

- Fix invalid chapter ID match bug for saves that have completed the Dream Again 3 chapter. When a file is saved after completing Dream Again 3, the chapter ID will be set to `81Common` from the game's internal logic. However, the internal `Data_Stages` file does not have an `81Common` chapter ID entry to initialize deployment slots and cost, which causing the game to revert to default values for these parameters. If the file is saved again and reloaded, the game will always crash in this invalid state that doesn't load units correctly into the roster. To fix this, there is now internal handling in the EXE to change the chapter ID of the `04OST` data entry loaded into the internal data structures from `04OST` to `81Common`. By doing this, the game will load the correct deployment slots and cost parameters that match up with the original parameters used for completing Dream Again 3 in PC CB.
  - However, this unfortunately does not fix those saves that were written in the invalid state. Only saves that were created immediately after Dream Again 3 was completed can be fixed.

- Fix the double selection bug for Duplex Barrier in the Learn Skills UI on Marisa's Route. This is now handled by correctly overwriting Reimu's Duplex Barrier with Super Duplex Barrier at the end of the common events for Chapter 40, ensuring that the update is not missed on either route.

- Bound the Debug Menu stage selection for Route B to the end of Chapter 75B to prevent crashes/unstable cases from loading other chapter IDs that are outside of Chapter 75B.

- Fix missing case for the ChangeUnitTileColor mod for overriding the tile color during certain Personal Command executions, like the execution for Ran's Protection of Zenki and Goki PS.

- Update number of deployment slots in all cases, bypassing the no-update case when the number of selectable units doesn't match up with the static number of deployment slots defined in `Data_Stages`. This should allow any number of deployment slots to be configured for any chapter.

- Fix end-of-chapter/save metadata cases of binary file write bug for file size when seeking from the end of the file and prematurely closing the file to write the current file position into the file size header. If the convention isn't followed for closing files after all binary data has been read, this will always result in filesize-based reads failing to read the entire file the next time the file is opened.

- Fix 6 damage calculation UI bugs:
  -  Stale reference for FPM rear attack always defaulting to the original auto-selected attack. You can select another attack for the rear FPM attack, and the game will update the damage calculation and accuracy rate to match the new attack's parameters. However, if you cast a Spirit afterwards, the game will revert the damage calculation and accuracy rate to the original auto-selected attack that was chose when initially entering the Battle Info screen.
  -  Rear FPM unit attack can ignore alert in the UI if an FPM rear attack is reselected. This is casued by bugged logic treating updates to rear FPM attacks as Support Attacks.
  -  Missed damage re-calculations for player rear/enemy support units when selecting counterattacks during the enemy phase.
  -  When the counter options are cycled among Attack, Evade, and Defend, the player damage calculation will update when cycling options toward the right, but not toward the left. This is due to legacy logic shortcutting fixed counter options that could not wrap from one end to the other, so the damage calculation only accounted for cycling counter options towards the right. The fix now performs the damage calculation for player attacks whether cycling left or right, when the weapon/action does modify damage.
  -  Previously updating rear FPM attacks did not update the displayed rear FPM multiplier. This was because the variable that controls the rear FPM multiplier wasn't updated with the new damage calcs after the attack was changed.
  -  Adapt did not factor into damage calculations when cast from the Battle Info screen. This is because the damage calculation routine was placed before finalizing Adapt's effects after casting the Spirit, meaning the damage calculation missed the new modifiers from the Terrain updates. This is now fixed by re-calculating the damage modifiers after Adapt's effects have been finalized.
 
- Implement `Data_Updates` addOn to fix ineffective character update for Letty's character data on Chapter 49. Letty's character data is expected to update from `Letty01` to `Letty02`, but the current record in `Data_Updates` attempts to update a `Letty02` instance to `Letty02`, which causes the update miss for `Letty01`. This fix restores the Friendships Letty is expected to have since the original FMW3.
  - Credits to TGxPerpetual and SteveO for figuring out the bugged update record of Letty on Chapter 49.

- Implement `Data_Updates` addOn to fix missing character update case for Lily White's character data on Chapter 36. Lily White's character data when reaching Chapter 36 is set to `LilyW02`, but the current record in `Data_Updates` only performs an update for `LilyW01` to `LilyW03`. This causes Lily White to miss out on her new Friendships that exist on `LilyW03` and later versions (such as `LilyW04` after she gets access to the Lily Black form). The fix adds another record to update from `LilyW02` to `LilyW03` to cover this case.

- Implement `Data_Trust` addOn to fix Yuugi's missing Friendships and Revenge Values for her single character data entry `Yugi01`. When the `Data_Trust` file was refactored in Complete Box, Yuugi's character data record was missing her Friendships and Revenge Values that had previously been declared in FMW4. This has persisted across all recent versions of Complete Box for Doujin PC, Switch, and Steam. The addOn fix restores the `Yugi01` character data to her original FMW4 values. She should now have the following Friendships and Revenge Values below:
```
Friendships
Suika: 3
Parsee: 2
Kaguya: 1

Revenge Values
Suika: 30
Parsee: 40
Kaguya: 0
```
 
# 1.2.4.1b Release
- Remove experimental changes for save metadata writes that had previously corrupted the Library data. Please download and apply this patch to restore saving/loading to original metadata format.
 
- Remove debug message logging for Straw Doll Kamikaze animation.

- Add skeleton for FMW1 Beta Flower Shooting animation. Internal name: `fshooting_beta`

# 1.2.4.1a Release
- Fix addOn bug for adding new abilities in the Data_Specials group by removing extraneous `pos` argument for functions that append to the abilities database. 

# 1.2.4.1 Release
- Migrate previous mod changes from 1.2.3.x

- Dynamically expand and draw the Abilities list if more than 4 abilities are present in the UI. This fixes previous text overflow UI bugs that did not take into account units (player or enemy) that had more than 4 abilities at a time.

- Fix UI bug where Distortion Barrier appears multiple times in the Abilities list if more than one Portable Gap is equipped.

- Remove Radiator Pack PS fix from modding changes as it is now natively implemented in the vanilla version starting from 1.2.4.
