# VASP
to learn the code and update with no credit to myself for the original work


Hey folks,
 
some time ago i pushed something to the public, but here is next!
 
 
"Damn which Truck was the open Camouflage one?"
"Bah cant remember which of the Vehicles holds the most amount of Magazines and Weapons..."
"How many Players can Drive in XYZ Vehicle?"
"How fast can that Vehicle go?"
 
"What the hell a 'Donald' skin look like?"
"'Rocker 1 2 3 whats the difference?"
 
Ever had such questions?
 
 
Here you go - VASP - Vehicle and Skin Preview
 
 
This little Mod let you Preview any Vehicle or Skin in the TraderMenu.
Vehicles will show additional Infos like:

Max Speed
Max Seats
Max Cargo Weapons
Max Cargo Magazines
Max Cargo Backpacks
Max Fuel
Max Armor
All stuff is totally client side spawned and will not be visible to any other Player on Server!
 
The Player clicks in the Tradermenu on a Vehicle or a Skin and he will get a hint message to press F5 for a preview of it.
 
While in preview, you can use these Hotkeys:
Zoom in/out:       Arrowkeys up/down 
Rotate left/right: Arrowkeys left/right
Close preview:   F5
 
After preview the Tradermenu will open again on the same spot the Player left it for the preview.
Just hit Buy and the last previewed item get bought.
 
Easy as Pie.

 
Demo Video
  http://youtu.be/KN8MAEpTC8I
 
Download:
https://www.dropbox.com/s/a2ziauc6rudqk97/VASP_v1.2.zip
 
Install instructions:
1. Download und unzip VASP_v1.2.zip
2. unpbo MPMissions\YOURMISSIONNAME.pbo (If your hoster has just folders you can skip this obviously ^^)
3. Copy the custom folder from unziped VASP_v1.2.zip to MPMissions\YOURMISSIONNAME\
4. open MPMissions\YOURMISSIONNAME\init.sqf
 
Find this block:

if (!isDedicated) then {
	0 fadeSound 0;
	waitUntil {!isNil "dayz_loadScreenMsg"};
	dayz_loadScreenMsg = (localize "STR_AUTHENTICATING");
	_id = player addEventHandler ["Respawn", {_id = [] spawn player_death;}];

};
And insert this line above the last closing bracket };

       _nil = [] execVM "custom\VASP\VASP_init.sqf";
If you dont have already a custom pulicEH.sqf continue on 5a) else continue on 5b)
 
5a)
Still in the init.sqf Find this line:

call compile preprocessFileLineNumbers "\z\addons\dayz_code\init\publicEH.sqf";
and replace with:

call compile preprocessFileLineNumbers "custom\VASP\publicEH.sqf";
5b)
open your custom publicEH.sqf and find this line:


"PVDZE_plr_SetDate"		addPublicVariableEventHandler {setDate (_this select 1);};
and replace with:

"PVDZE_plr_SetDate"		addPublicVariableEventHandler {if (!(player getVariable["Preview",false])) then {setDate (_this select 1);};};
If you dont have already a custom compiles.sqf continue on 6a) else continue on 6b)
 
6a)
Still in the init.sqf Find this line:

call compile preprocessFileLineNumbers "\z\addons\dayz_code\init\compiles.sqf";
and replace with:

call compile preprocessFileLineNumbers "custom\VASP\compiles.sqf";                //Compile regular functions
6b)
Open your custom compiles.sqf and find this block:


	// trader menu code
	if (DZE_ConfigTrader) then {
		call compile preprocessFileLineNumbers "\z\addons\dayz_code\compile\player_traderMenuConfig.sqf";
	}else{
		call compile preprocessFileLineNumbers "\z\addons\dayz_code\compile\player_traderMenuHive.sqf";
	};
and replace with:

	// trader menu code
	if (DZE_ConfigTrader) then {
		call compile preprocessFileLineNumbers "custom\VASP\player_traderMenuConfig.sqf";
	}else{
		call compile preprocessFileLineNumbers "custom\VASP\player_traderMenuHive.sqf";
	};
Find this line:

	fnc_usec_selfActions =			compile preprocessFileLineNumbers "\z\addons\dayz_code\compile\fn_selfActions.sqf";		//Checks which actions for self
and replace with:

	fnc_usec_selfActions =			compile preprocessFileLineNumbers "custom\VASP\fn_selfActions.sqf";		//Checks which actions for self
If you already use a custom fn_selfActions.sqf open it and find this line:

				_buy = player addAction [localize "STR_EPOCH_PLAYER_289", "\z\addons\dayz_code\actions\show_dialog.sqf",(_traderMenu select 0), 999, true, false, "",""];
and add ABOVE:

				LastTraderMenu = (_traderMenu select 0);
7. repbo MPMissions\YOURMISSIONNAME\ - upload - restart server - enjoy!
 
 

- Configuration -

Open VASP_init.sqf and edit this block to your liking:

	/****************************/
	/*      Configuration       */
	/****************************/
	/*  Vehicle Preview on/off  */
	/* true = ON / false = OFF  */
	VASP_VehiclePreview = true;
	/****************************/
	/*    Skin Preview on/off   */
	/* true = ON / false = OFF  */
	VASP_SkinPreview = true;
	/****************************/
	/* !!! DONT EDIT BELOW !!!  */
 
- Additional Information -
 
For those who have MORE then the standard Epoch Skins buyable at the Traders you would need to open MPMissions\YOURMISSIONNAME\custom\VASP\VASP_init.sqf
 
and add them to this block:


    AllAllowedSkins = [
        "Skin_Survivor2_DZ","Skin_SurvivorWcombat_DZ","Skin_SurvivorWdesert_DZ",
        "Skin_SurvivorWurban_DZ","Skin_SurvivorWsequishaD_DZ","Skin_SurvivorWsequisha_DZ",
        "Skin_SurvivorWpink_DZ","Skin_SurvivorW3_DZ","Skin_SurvivorW2_DZ",
        "Skin_Bandit1_DZ","Skin_Bandit2_DZ","Skin_BanditW1_DZ",
        "Skin_BanditW2_DZ","Skin_Soldier_Crew_PMC","Skin_Sniper1_DZ",
        "Skin_Camo1_DZ","Skin_Soldier1_DZ","Skin_Rocket_DZ",
        "Skin_Rocker1_DZ","Skin_Rocker2_DZ","Skin_Rocker3_DZ",
        "Skin_Rocker4_DZ","Skin_Priest_DZ","Skin_Functionary1_EP1_DZ",
        "Skin_GUE_Commander_DZ","Skin_Ins_Soldier_GL_DZ","Skin_Haris_Press_EP1_DZ",
        "Skin_Pilot_EP1_DZ","Skin_RU_Policeman_DZ","Skin_Soldier_TL_PMC_DZ",
        "Skin_Soldier_Sniper_PMC_DZ","Skin_Soldier_Bodyguard_AA12_PMC_DZ","Skin_Drake_Light_DZ",
        "Skin_CZ_Special_Forces_GL_DES_EP1_DZ","Skin_TK_INS_Soldier_EP1_DZ","Skin_TK_INS_Warlord_EP1_DZ",
        "Skin_FR_OHara_DZ","Skin_FR_Rodriguez_DZ","Skin_CZ_Soldier_Sniper_EP1_DZ",
        "Skin_GUE_Soldier_MG_DZ","Skin_GUE_Soldier_Sniper_DZ","Skin_GUE_Soldier_Crew_DZ",
        "Skin_GUE_Soldier_CO_DZ","Skin_GUE_Soldier_2_DZ","Skin_TK_Special_Forces_MG_EP1_DZ",
        "Skin_TK_Soldier_Sniper_EP1_DZ","Skin_TK_Commander_EP1_DZ","Skin_RU_Soldier_Crew_DZ",
        "Skin_INS_Lopotev_DZ","Skin_INS_Soldier_AR_DZ","Skin_INS_Soldier_CO_DZ",
        "Skin_INS_Bardak_DZ","Skin_INS_Worker2_DZ"
    ];
This is ONLY needed if you have custom Skins that are buyable on the Traders!
