DAYZ-LOOT-TABLE
===============
private["_position","_veh","_num","_config","_itemType","_itemChance","_weights","_index","_iArray"];

waitUntil{!isNil "BIS_fnc_selectRandom"};
if (isDedicated) then {
_position = [getMarkerPos "center",0,7000,10,0,2000,0] call BIS_fnc_findSafePos;

_randomvehicle = ["MV22Wreck","LADAWreck","BMP2Wreck","MH60Wreck","C130JWreck","Mi24Wreck","UralWreck","HMMWVWreck","T72Wreck"] call BIS_fnc_selectRandom;
_vehicleloottype = ["Residential","Industrial","Military","Farm","Supermarket","Hospital"] call BIS_fnc_selectRandom;

_veh = createVehicle [_randomvehicle,_position, [], 0, "CAN_COLLIDE"];
dayz_serverObjectMonitor set [count dayz_serverObjectMonitor,_veh];
_veh setVariable ["ObjectID",1,true];

_num = round(random 3) + 3;

if (_randomvehicle == "UralWreck") then { _num = round(random 12) + 5; };
if (_randomvehicle == "C130JWreck") then { _num = round(random 12) + 5; };

  switch (_vehicleloottype) do {
  
		case "Military": {
    
			_itemType = [["M9", "weapon"], ["UZI_EP1", "weapon"], ["MakarovSD", "weapon"], ["M9SD", "weapon], ["UZI_SD_EP1", "weapon"],  ["Sa61_EP1", "weapon"], ["DZ_ALICE_Pack_EP1", "object"], ["MP5SD", "weapon"], ["Bizon_silenced", "weapon"], ["FN_Fal", "weapon"], ["AmmoBoxSmall_556", "object"], ["AmmoBoxSmall_762", "object"], ["NVGoggles", "military"], ["M24", "weapon"], ["Binocular_Vector", "military"], ["PipeBomb", "military"], ["G36A_Camo", "weapon"], ["M14_EP1", "weapon"], ["MG36", "weapon"], ["BAF_L85A2_UGL_Holo", "weapon"], ["G36K", "weapon"], ["M16A4_ACG_GL", "weapon"], ["M4A3_RCO_GL_EP1", "weapon"], ["ItemFlashlightRed", "military"], ["M4A1_HWS_GL_Camo", "weapon"], ["ItemGPS", "military"], ["Skin_Soldier1_DZ", "magazine"], ["Skin_Sniper1_DZ", "magazine"]];
			_itemChance = [0.08, 0.08, 0.04, 0.04, 0.04, 0.08, 0.1, 0.03, 0.03, 0.04, 0.05, 0.05, 0.04, 0.01, 0.01, 0.05, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.01, 0.05, 0.01, 0.05, 0.03, 0.02];
		};
		case "Residential": {
    
			_itemType = [["ItemSodaMdew", "generic"], ["Huntingrifle", "weapon"], ["ItemCompass", "weapon"], ["ItemMap", "weapon"], ["Makarov", "weapon"], ["Colt1911", "weapon"], ["glock17_EP1", "weapon"], ["ItemKnife", "weapon"], ["ItemMatchbox", "weapon"], ["LeeEnfield", "weapon"], ["revolver_EP1", "weapon"], ["DZ_CivilBackpack_EP1", "object"], ["Winchester1866", "weapon"], ["WeaponHolder_ItemTent", "object"], ["Binocular", "weapon"], , ["Skin_Camo1_DZ", "magazine"], ["Skin_Sniper1_DZ", "magazine"]];
			_itemChance = [0.1, 0.02, 0.1, 0.1, 0.07, 0.07, 0.05, 0.05, 0.1, 0.04, 0.07, 0.1, 0.03, 0.02, 0.05, 0.02, 0.01];
		};
		case "Industrial": {
    
			_itemType = [["WeaponHolder_PartGeneric", "object"], ["WeaponHolder_PartWheel", "object"], ["WeaponHolder_PartFueltank", "object"], ["WeaponHolder_PartEngine", "object"], ["WeaponHolder_PartGlass", "object"], ["WeaponHolder_PartVRotor", "object"], ["WeaponHolder_ItemJerrycan", "object"], ["WeaponHolder_ItemHatchet", "object"], ["ItemKnife", "generic"], ["ItemToolbox", "weapon"], ["ItemWire", "magazine"], ["ItemTankTrap", "magazine"], ["ItemSandbag", "magazine"], ["LeeEnfield", "weapon"], ["Remington870_lamp", "weapon"], ["ItemEtool", "generic"], ["DZ_Assault_Pack_EP1", "object"]];
			_itemChance = [0.04, 0.1, 0.01, 0.03, 0.04, 0.01, 0.1, 0.1, 0.05, 0.1, 0.03, 0.07, 0.07, 0.05, 0.05, 0.05, 0.1];	
		};
		case "HeliCrash": {
			_itemType = [["DZ_Backpack_EP1", "object"], ["Skin_Soldier1_DZ", "magazine"], ["Skin_Sniper1_DZ", "magazine"], ["NVGoggles", "military"], ["Binocular_Vector", "military"], ["M24_des_EP1", "weapon"], ["M40A3", "weapon"], ["SVD_Camo", "weapon"], ["BAF_L85A2_UGL_ACOG", "weapon"], ["M4A1_HWS_GL_SD_Camo", "weapon"], ["FN_FAL_ANPVS4", "weapon"], ["G36_C_SD_eotech", "weapon"], ["M4SPR", "weapon"], ["AK_107_PSO", "weapon"], ["BAF_LLR_scope", "weapon"], ["M9SD", "weapon"], ["MakarovSD", "weapon"], ["UZI_SD_EP1", "weapon"], ["Saiga12k", "weapon"], ["M60E4_EP1", "weapon"], ["Mk_48_DES_EP1", "weapon"], ["m240_scoped_EPI1", "weapon"], ["BAF_L110A1_Aim", "weapon"], ["M249_m145_EP1", "weapon"]];
			_itemChance = [0.15, 0.05, 0.05, 0.08, 0.02, 0.02, 0.01, 0.01, 0.02, 0.02, 0.05, 0.02, 0.02, 0.02, 0.01, 0.1, 0.1, 0.1, 0.05, 0.02, 0.02, 0.02, 0.02, 0.02];
		};
		case "Farm": {
    
			_itemType = [["ItemToolbox", "weapon"], ["huntingrifle", "weapon"], ["LeeEnfield", "weapon"], ["Winchester1866", "weapon"], ["M1014", "magazine"], ["revolver_EP1", "weapon"], ["WeaponHolder_ItemHatchet", "object"], ["TrapBear", "magazine"], ["ItemSandbag", "magazine"], ["DZ_CivilBackpack_EP1", "object"], ["Skin_Camo1_DZ", "magazine"], ["Skin_Sniper1_DZ", "magazine"], ["WeaponHolder_ItemTent", "object"], ["WeaponHolder_PartGeneric", "object"], ["WeaponHolder_PartWheel", "object"], ["WeaponHolder_PartFueltank", "object"], ["WeaponHolder_PartEngine", "object"], ["WeaponHolder_PartGlass", "object"], ["WeaponHolder_ItemJerrycan", "object"], ["ItemCompass", "weapon"], ["ItemMap", "weapon"], ["Binocular", "weapon"], ["ItemKnife", "generic"], ["ItemMatchbox", "generic"], ["ItemEtool", "weapon"]];
			_itemChance = [0.04, 0.03, 0.05, 0.05, 0.03, 0.04, 0.05, 0.1, 0.1, 0.05, 0.01, 0.01, 0.01, 0.02, 0.05, 0.01, 0.01, 0.02, 0.1, 0.04, 0.04, 0.04, 0.05, 0.05, 0.04];	
		};
		case "Supermarket": {	
		
			_itemType = [["FoodBox0", "object"], ["Huntingrifle", "weapon"], ["ItemCompass", "weapon"], ["ItemMap", "weapon"], ["Makarov", "weapon"], ["Colt1911", "weapon"], ["FoodBox1", "object"], ["ItemKnife", "generic"], ["ItemMatchbox", "generic"], ["LeeEnfield", "weapon"], ["revolver_EP1", "weapon"], ["DZ_CivilBackpack_EP1", "object"], ["Winchester1866", "weapon"], ["WeaponHolder_ItemTent", "object"], ["Binocular", "generic"], ["FoodBox2", "object"], ["Skin_Camo1_DZ", "magazine"], ["Skin_Sniper1_DZ", "magazine"]];
			_itemChance = [0.04, 0.03, 0.05, 0.1, 0.1, 0.1, 0.03, 0.05, 0.1, 0.04, 0.1, 0.1, 0.03, 0.02, 0.05, 0.03, 0.02, 0.01];
		};
		case "Hospital": {
    
			_itemType = [["", "trash"], ["", "hospital"], ["MedBox0", "object"], ["", "generic"], ["","medical"]];
			_itemChance = [0.55, 0.15, 0.1, 0.05, 0.15];
		};
	};

diag_log("DEBUG: Spawning a " + str (_randomvehicle) + " at " + str(_position) + " with loot type " + str(_vehicleloottype) + " With total loot drops = " + str(_num));

waituntil {!isnil "fnc_buildWeightedArray"};

_weights = [];
_weights = 		[_itemType,_itemChance] call fnc_buildWeightedArray;	
for "_x" from 1 to _num do {
	_index = _weights call BIS_fnc_selectRandom;
	sleep 1;
	if (count _itemType > _index) then {
		_iArray = _itemType select _index;
		_iArray set [2,_position];
		_iArray set [3,10];
		_iArray call spawn_loot;
		_nearby = _position nearObjects ["WeaponHolder",20];
		{
			_x setVariable ["permaLoot",true];
		} forEach _nearBy;
	};
};
};
