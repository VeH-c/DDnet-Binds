Source https://gist.github.com/b3z/1f2175a221cfa3f62060b2374e3aa200
credits https://gist.github.com/b3z
# Teewords config cheatsheet
> In this repository you will find a collection of teeworlds binds, configs and scripts which you can use in your `settings_ddnet.cfg`



> If you feel like a bind is missing please contribute.
---

[How binding works](#how-binding-works)

> the basics of binding

[Toggle binding](#toggle-binding)

> using config files for binding 

[Gores Hammer autoswitch](#gores-hammer-autoswitch)

[Dummy Deepfly](#dummy-deepfly)

[Spectating binds](#spectating-binds) 

> Pause, Spec, Two binds One key, view resets.

[Team binds](#team-binds)

> Join and lock. Back for gores.

[Emotes](#emotes)

> Binding emotes. All available emotes and eyes.

[HUD and game](#hud-and-game)

> Zenmode, antiping, zooming, entities, aiming.

Here you can find an [overview of all commands](https://ddnet.tw/settingscommands/) in Teeworlds.



### How binding works

Here we just want to bind a command to a key. 

```py
# simple bind
bind [key] [command]

# multi bind
bind [key] "[command1]; [command2]; ..."

# nested bind
bind [key1] "bind [key2] \"[command1]; [command2]\"; [command3]"
```

Examples
```py
# simple bind
bind i say Hello World!

# multi bind 
bind space "+jump; emote 7"

# multi nested bind
bind 6 "bind mouse1 \"+fire; +prevweapon\"; bind mouse2 \"+hook; +weapon2\"; echo Firemode: gores"
```



### Toggle binding

Now facing the problem that one key can only execute one set of commands using normal binding we need to come uo with something else because we only have a 104 keys on our keyboard.

To solve this we will use secondary config files. This way we can change the behaviour of a key in a certain state.

file1.cfg
```py
[mainCommand] # the main command we want to have
[rebindCommand] # a reference to file2
```

file2.cfg
```py
[mainCommand] # second main command we want to have
[rebindCommand] # a reference to file1
```

This way we can switch between two commands which creates like a toggle effect.
This also works with more than 2 files. You just have to chain them.

Example:

ping.cfg
```py
echo "ping"
bind 6 "exec pong.cfg"
```

pong.cfg
```py
echo "pong"
bind 6 "exec ping.cfg"
```





### Gores Hammer autoswitch

This is a useful toggle bind for goresplayers it allowes to always hammer even if another weapon is selected. This way you can play and aim with the gun but always have the hammer for saving.

In this case you can toggle the modes by pressing rgui. You might want to replace rgui with the key of your favour.

goresmode.cfg

```py
bind mouse1 "+fire;+prevweapon"
bind mouse2 "+hook;+weapon2"
echo "Firemode: Gores"
bind rgui "exec defaultmode.cfg"
```

 defaultmode.cfg

```py
bind mouse1 "+fire"
bind mouse2 "+hook;"
echo "Firemode: Default"
bind rgui "exec goresmode.cfg"
```



These two files have to lay in the same directory like your settings.cfg.

Now we have to create a reference to the settings.cfg and either bind it initially or just go ingame and execute `exec defaultmode.cfg` in the console. This will write a reference to the settings so you now can use the toggle.



### Dummy deepfly

This bind allowes deepfly with your dummy.

dummyDeepflyMode.cfg

```.py
bind mouse1 "+fire;+toggle cl_dummy_hammer 1 0 "
echo "Dummymode: Deepfly"
bind f exec "dummyNormalMode.cfg"
```

dummyNormalMode.cfg

```.py
bind mouse1 "+fire"
echo Dummymode: Normal
bind f exec "dummyDeepflyMode.cfg"
```

Also activate it by executeing `exec dummyDeepfly.cfg`



### Spectating binds

A very command bind is the spectating command.

```py
bind w say /pause
```

This lets you unlock your camera and freely move around with your view when pressing `w`. in this mode your tee stays where it is! This is important for some DDRace maps and especially for Gores.

Another way to "spec" is to use this command:

```py
bind p say /spec
```

The issue or better said feature of this command is that in Gores and some DDRace maps your tee will disappear and make space for others. It will pop back in when you press `p` again. This is helpful for e.g. onetiles if someone wants to pass without bouncing on you. 

These are the basics but there are ways to to advanced binding here.

```py
bind s "+showhookcoll; +spectate"
```

 Now the hookcollision is a little random but mine is on `s`  and its something you cant use in spec mode. So you can combine it with another command that only works in spec mode. This way in play mode `s`  toggles the hook collision and in spec mode it toggles the spectator board where you can select who you want to watch.

To round it up I also modified my bind in `w` (`/pause`) 

```py
bind w "say /pause; zoom; spectate -1"
```

What this does is of course `/spec` but also reset the zoom to default. If you zoom out in spec mode to see more this will reset you if you need to react fast in game mode again. Also the spectate part at the end of the command resets who you are spectating to "free cam" so you are not stuck spectating a player when you go into spec mode again. 

This can also be applied to `p` (`/spec`)



### Team binds

 Useful for joining a team

```py
bind 7 chat all "/team "
```

this way you just press `7`  followed by a number and press enter. Boom you are in.



Locking teams, very common bind

```py
bind 0 say /lock
```



For goresplayers this "back" bind might be interesting, I use it a lot.

```py
bind q say_team b
```



### Emotes

```
bind lshift "emote 7; say /emote surprise 999999"
```

This way you can bind a fix emote to a key and also have the same eye emote all the time.

Some people prefere the "emote wheel" where you can select an emote.

Those shall use `+emote` instead of `emote 7`



Available eye emotes:

* happy
* angry
* pain
* surprise
* blink
* normal

Available emotes:
(with the number as emote id)

1. !
2. heart
3. waterdrop
4. three dots
5. music notes
6. sorry!
7. ghost
8. pain
9. angry
10. devil
11. swearwords
12. WTF
13. ^^
14. ???



### Hud and Game

```py
# toggle HUD (ammo, hearts and stuff. Nice zen mode)
bind j "toggle cl_showhud 0 1"

# toggle antiping
bind n "toggle cl_antiping 0 1"

# zooming
bind v zoom-
bind c zoom+
bind b zoom

# entitites
bind x "toggle cl_overlay_entities 0 100"

# accurate aim
bind 6 "+toggle inp_mousesens 5 100"

# easy shooting up (only 45° angles movement)
bind y "+toggle cl_mouse_max_distance 2 400; +toggle inp_mousesens 1 100"
```


