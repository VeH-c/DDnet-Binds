# DDnet-Binds
Binds For DDnet

WIP & Todo // everything...
starting points
https://forum.ddnet.tw/viewtopic.php?f=16&t=2537
https://forum.ddnet.tw/viewtopic.php?p=68892#p68892
my personal ScriptBinds folder :)
https://forum.ddnet.tw/viewtopic.php?p=68946#p68946


binds to add or sort out
Camera mode :
bind <key> "toggle cl_nameplates 0 1 ; toggle cl_showchat 0 1; toggle cl_showhud 0 1; toggle cl_showkillmessages 0 1;toggle cl_show_hook_coll_other 0 1;toggle cl_show_hook_coll_own 0 1 ; cl_show_quads 1 ;cl_overlay_entities 0"

a One key Bind that repeated, Connects Dummy, Teams & locks.
Hide
bind shift+l "bind l \"dummy_connect; bind l \\\"cl_dummy 1; say /team 27; bind l \\\\\\\"cl_dummy 0; say /team 27; bind l \\\\\\\\\\\\\\\"say /lock; echo press SHIFT+L to reset\\\\\\\\\\\\\\\"\\\\\\\"\\\"\""

// You could make it so that every time you start your client it will be at the beginning, by resetting the StepBind, closing the client, finding the string of what L is bound to in settings_ddnet.cfg & adding that to your autoexec.cfg. in this case bind l "dummy_connect; bind l \"cl_dummy 1; say /team 27; bind l \\\"cl_dummy 0; say /team 27; bind l \\\\\\\"say /lock; echo press SHIFT+L to reset\\\\\\\"\\\"\""

https://www.teeworlds.com/forum/viewtopic.php?id=12009

instantly joining a team with dummy
Spoiler
Hide
NOTE: These binds can be a bit finicky (dummy switch time, client lag etc. & only work when dummy is already connected)
CODE: SELECT ALL

bind x "cl_dummy 1; say /team 1; say /lock; cl_dummy 0; say /team 1"
Join team (1) with your dummy & lock it.

CODE: SELECT ALL

bind x "cl_dummy 1; say /team 1; say /team 2; say /lock; cl_dummy 0; say /team  1; say /team 2"
Joins you & your connected dummy to team (1) if available, if not then team (2) (& lock's it).
