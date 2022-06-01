#SingleInstance Force	;Disallow multiple instances of this scripts
SetWorkingDir, %A_ScriptDir%
ListLines Off ;can be used to selectively omit some lines from the history, which can help prevent the history from filling up too quickly (such as in a loop with many fast iterations).
#NoEnv  ; Recommended for performance and compatibility with future AutoHotkey releases.

; ---> SCRIPT MUST BE RELOADED AFTER ANY CHANGE! <---
; For better performance always put the lowest number in the ench1Pos

ConfigPath = %A_WorkingDir%\config.ini

if !FileExist(ConfigPath){
	FileAppend,[ITEM]`n, %ConfigPath%
	FileAppend,Type=0`n, %ConfigPath%
	FileAppend,[ENCHANTMENT]`n, %ConfigPath%
	FileAppend,Enchantment1=1`n, %ConfigPath%
	FileAppend,Enchantment2=0`n, %ConfigPath%
	FileAppend,Max=10`n, %ConfigPath%
	MsgBox,4096, READ-ME, Please configure the "config.ini" file of Speed Enchanting`nThe script must be reloaded after any changes!`nFor better performance always put the lowest number of Enchantment1 and Enchantment2 in the Enchantment1
	Run, %ConfigPath%
}

IniRead, itemTypeConfig, %A_ScriptDir%\config.ini, ITEM, Type
IniRead, ench1PosConfig, %A_ScriptDir%\config.ini, ENCHANTMENT, Enchantment1
IniRead, ench2PosConfig, %A_ScriptDir%\config.ini, ENCHANTMENT, Enchantment2
IniRead, maxEnchConfig, %A_ScriptDir%\config.ini, ENCHANTMENT, Max

;First enchantment position on list
Global ench1Pos := ench1PosConfig

;Second enchantment position on list
;Set 0 if you dont wanna the second enchantment
Global ench2Pos := ench2PosConfig

;Max enchantments to make
Global maxEnch := maxEnchConfig

;Inform the type of your item
;0 = Any other item
;1 = Weapon
Global itemType := itemTypeConfig

if(itemType != 1 AND itemType != 0){
	MsgBox, 4096,, Type must be 0 or 1`n1 = Weapon`n0 = Everything else`nCheck config.ini
}

if(ench1Pos <= 0){
	MsgBox, 4096,, Enchantment1 must be higher then 0`nCheck config.ini
}

if(ench2Pos < 0){
	MsgBox, 4096,, Enchantment2 must be 0 or higher`nCheck config.ini
}

if(ench1Pos == ench2Pos){
	MsgBox, 4096,, Enchantment1 must be different then Enchantment2`nCheck config.ini
}

if(maxEnch <= 0){
	MsgBox, 4096,, Max must be higher then 0`nCheck config.ini
}

CAPSLOCK::
    Toggle4 := !Toggle4
    settimer,doloop4,1
return

doloop4:

i := 0
settimer,doloop4,off
while (Toggle4) {
	if(WinActive("ahk_exe SkyrimSE.exe")){
		if(i != maxEnch){

			;ITEM LIST
			Send, s ;Select first item
			Sleep, 50
			Send, e ;Marks the first item as selected
			Sleep, 50

			;ENCHANTMENT LIST
			Send, d ;Change tab to Enchament List
			Sleep, 50
			SelectEnchDown(ench1Pos) ;Select enchantment 1
			Sleep, 50
			if(ench2Pos != 0){
				if(ench2Pos > ench1Pos){
					newPos := ench2Pos-ench1Pos
					SelectEnchDown(newPos) ;Select enchantment 2
					Sleep, 50
				} else {
					newPos := ench1Pos-ench2Pos
					SelectEnchUp(newPos) ;Select enchantment 2
					Sleep, 50
				}
			}

			;SOUL GEM LIST
			Send, d ;Change tab to Soul Gem List
			Sleep, 50
			Send, s ;Select first item
			Sleep, 50
			Send, e ;Marks the first item as selected
			Sleep, 50
			Send, r ;Craft
			Sleep, 50
			Send, y ;Confirm Craft
			Sleep, 50

			;RETURNING TO ITEM LIST
			Send, a
			Sleep, 50
			Send, a
			Sleep, 50

			i := i+1
		} else {
			Toggle4 := !Toggle4
		}
	} else {
		Toggle4 := !Toggle4
	}
}

SelectEnchDown(Number){
	loop, %Number%{
		Send s
		Sleep 50
	}
	Send e ;Select enchantment
	if(itemType = 1){
		Sleep 50
		Send e
	}
}

SelectEnchUp(Number){
	loop, %Number%{
		Send w
		Sleep 50
	}
	Send e ;Select enchantment
	if(itemType = 1){
		Sleep 50
		Send e
	}
}
