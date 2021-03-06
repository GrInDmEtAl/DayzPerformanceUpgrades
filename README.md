# Performance improvements for DayZ#

This repository will focus on performance related improvements for DayZ


DayZ is a very special game and it seems many peoples are still loving it.   
DayZ runs normally really stable and nice now and we could just enjoying it.   

Under heavy load and on servers running many hours, we still have to notice some problems.   

Because of DayZ's history and origin, current DayZ code is somewhat less than perfect.   
But it is not really easy to replace old "quick and dirty" code with better optimized code.   
So the evolution of DayZ will still be a difficult and tedious process, which require much work of all community developers.   
I will help here a bit and from time to time present my results here.   

Please realize, the progress of work really depends of feedback from server admins testing this stuff presented here.    
So if you are brave enough to test some code from here, please tell me in the OpenDayZ forum how it works for you:

[http://opendayz.net/index.php?threads/a-better-queued-login-process-for-dayz.1052/](http://opendayz.net/index.php?threads/a-better-queued-login-process-for-dayz.1052/)    

If enough people have testing this stuff succesfully, i will request a related pull to the community build,    
hopfull that it is available with the next community build for everybody.

Thanks.   

Below you will find some code enhancements and a short "how to use".

## Instant Login always and for everybody !!!   
Do you think it is a joke? It isn't, try it out!

Login much accelerated, because of minimizing slow running overhead from MPFramework.   
Unload server simultaneous, by avoiding the useless serverside processing of commands like rSay e.t.c..    
To accelerate other scripts in the "background" too, we simultaneously change some eventhandler defines in publicEH.sqf.   

How to install:    

In your `server_functions.sqf` file insert the following code lines below this `waituntil {!isnil "bis_fnc_init"};` :    

	BIS_MPF_remoteExecutionServer = {
		if ((_this select 1) select 2 == "JIPrequest") then {
			[nil,(_this select 1) select 0,"loc",rJIPEXEC,[any,any,"per","execVM","ca\Modules\Functions\init.sqf"]] call RE;
		};
	};

Copy the file `publicEH.sqf` from here ...

[https://github.com/fred41/DayzPerformanceUpgrades/blob/master/publicEH_experimental/publicEH.sqf](https://github.com/fred41/DayzPerformanceUpgrades/blob/master/publicEH_experimental/publicEH.sqf) 

... in your misson directory and edit `init.sqf` as follows:

	//call compile preprocessFileLineNumbers "\z\addons\dayz_code\init\publicEH.sqf";
	call compile preprocessFileLineNumbers "publicEH.sqf";


One problem currently observed is the following:
Because you can now very fast relogin, it is possible that you meet the alerted Zombies from your previous login, looking stupid around and seems to wait for new order :D   
They will disappear a few seconds later.


## Reworked server cleanup state machine   
Better priority ordering, faster object update execution.  

How to install:   

Replace your `server_cleanup.fsm` with the file from here:


[https://github.com/fred41/DayzPerformanceUpgrades/blob/master/server_cleanup/server_cleanup.fsm](https://github.com/fred41/DayzPerformanceUpgrades/blob/master/server_cleanup/server_cleanup.fsm)



Thanks for testing this and let me know your results :)
