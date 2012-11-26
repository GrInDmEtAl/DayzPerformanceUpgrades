# Performance improvements for DayZ#

This repository will focus on performance related improvements for DayZ


DayZ is a very special game and it seems many peoples are still loving it.   
DayZ runs normally really stable and nice now and we could just enjoying it.   

Under heavy load and on servers running many hours, we still have to notice some problems.   

Because of DayZ's history and origin, DayZ code is somewhat less than perfect.
But it is not really easy to replace old "quick and dirty" code with better optimized code.   
So the evolution of DayZ will still be a hard and slow process, which require much, intensive work of all community developers.   
I will help here a bit and from time to time present my results here.   

Please realize, the progress of work really depends of feedback from server admins testing this stuff presented here.    
So if you are brave enough to test some code from here, please tell me in the OpenDayZ forum how it works for you:

[http://opendayz.net/index.php?threads/a-better-queued-login-process-for-dayz.1052/](http://opendayz.net/index.php?threads/a-better-queued-login-process-for-dayz.1052/)    

If enough people have testing this stuff succesfully, i will request a related pull to the community build, hopfull that it is available with the next community build for everybody.

Thanks.   

Below you will find some code enhancements and a short "how to use".

## Instant Login always and for everybody !!!   
Do you think it is a joke? It isn't, try it out!

Login much accelerated, because of minimizing slow running overhead from MPFramework.   
Unload server simultaneous, by avoiding the serverside processing of commands like rSay e.t.c..    

In your `server_functions.sqf` file insert the following code lines below this `waituntil {!isnil "bis_fnc_init"};` :    

	BIS_MPF_remoteExecutionServer = {
		if ((_this select 1) select 2 == "JIPrequest") then {
			[nil,(_this select 1) select 0,"loc",rJIPEXEC,[any,any,"per","execVM","ca\Modules\Functions\init.sqf"]] call RE;
		};
	};

The only problem currently observed is the following:
Because you can now very fast relogin, it is possible that you meet the alerted Zombies from last login, looking stupid around and seems to wait for new order :D
They will disapear past a few seconds then.


## Reworked server cleanup state machine   
Better priority ordering, faster object update execution.  


Replace your `server_cleanup.fsm` with the file from here:


[https://github.com/fred41/DayzPerformanceUpgrades/blob/master/server_cleanup/server_cleanup.fsm](https://github.com/fred41/DayzPerformanceUpgrades/blob/master/server_cleanup/server_cleanup.fsm)



Thanks for testing this and let me know your results :)
