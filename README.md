# Performance improvements for DAYZ#

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


Thanks.   


**Reworked server cleanup fsm**

replace your server_cleanup.fsm with the file from here:


[https://github.com/fred41/DayzPerformanceUpgrades/blob/master/server_cleanup/server_cleanup.fsm](https://github.com/fred41/DayzPerformanceUpgrades/blob/master/server_cleanup/server_cleanup.fsm)



Thanks for testing this and let me know your results :)


