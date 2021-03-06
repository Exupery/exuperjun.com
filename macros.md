---
layout: page
title: Macros
permalink: /macros/
---

## Mistweaver-specific macros

### Defensive talent row
This will automatically use [Healing Elixir](https://www.wowhead.com/spell=122281), [Diffuse Magic](https://www.wowhead.com/spell=122783), or [Dampen Harm](https://www.wowhead.com/spell=122278) depending on which talent from that row is selected.
```
#showtooltip
/use [talent:5/1]Healing Elixir;[talent:5/2]Diffuse Magic;[talent:5/3]Dampen Harm;
```

### CC talent row
This will automatically use [Ring of Peace](https://www.wowhead.com/spell=116844) or [Song of Chi-Ji](https://www.wowhead.com/spell=198898) depending on which of those is selected. If RoP is selected and `SHIFT` is pressed with the keybind it will instantly drop the ring centered on your character.
```
#showtooltip
/cast [modifier:shift, @player][talent:4/3] Ring of Peace; [talent:4/2] Song of Chi-Ji
```

### Detox
Having three Detox macros allows dispelling yourself or a teammate without needing to switch targets first.
```
#showtooltip Detox
/use [@party1] Detox
```

```
#showtooltip Detox
/use [@party2] Detox
```

```
#showtooltip Detox
/use [@player] Detox
```

### Healing Spehere
This allows dropping a [Healing Sphere](https://www.wowhead.com/spell=205234) immediately where your cursor is at when the keybind is pressed (instead of opening up the targetting reticle and needing to click where to place).
```
#showtooltip Healing Sphere
/use [@cursor] Healing Sphere
```

### Crackling Jade Lightning
Will zap your current target if it's an enemy (and alive), otherwise will hit the player (either character itself or a unit frame) your mouse is over (likewise if it's an enemey and still alive). Useful for when you want to apply [Mystic Touch](https://www.wowhead.com/spell=8647/mystic-touch) to an enemy without swapping targets from who you're currently healing.
```
#showtooltip Crackling Jade Lightning
/cast [harm,nodead][@mouseover,harm,nodead] Crackling Jade Lightning
```

### Provoke
This will taunt an enemy's pet if present, otherwise your mouseover if an enemy, otherwise your current target. This allows not needing to target a specific pet when attempting a taunt a pet right before receiving breakable CC.
```
#showtooltip Provoke
/cast [@arenapet1] Provoke
/cast [@arenapet2] Provoke
/cast [@arenapet3] Provoke
/cast [@mouseover, harm, exists][] Provoke
```

## General macros

### Drink
Replace the second `use` with whatever mana drink you use and this allows you to have a single keybind that will use mana food if you have it and otherwise will use the bought food.
```
#showtooltip Ambroria Dew
/use Conjured Mana Bun
/use Ambroria Dew
```

### Target teammates
I don't like to use the native Blizzard keybindings for targeting `party1` and `party2` because if the teammate has a pet and you press the keybind a second time it will target their pet (this is particularly problematic if you use mousewheel up/down to target arena partners). Using a macro prevents that and will only target the actual party member. The `party2` macro isn't as simple as one would expect because I'm clumsy and I found that when I did some 2s after a long 3s session my mind would get used to my party2 keybind (mousewheel down) targetting the bottom unit (of my party frames), but in 2s the bottom unit is party1 - thus I created a macro that would target party2 when there is one, but would otherwise target party1.
```
/target party1
```

```
/target [@party2, exists][] party1
```

### Dealing with Empyrean Domain's brightness
This macro will toggle between normal brightness (Blizz's default of 50) and a much lower brightness setting, useful for not getting blinded on Empyrean Domain. Just press it when you zone into ED (or wherever) to lower the brightness and then press it again after the match to return it to normal.

If your normal brightness setting is something other than the default of `50` then replace the two occurances of `50` below with whatever value you have under System -> Advanced -> Brightness. Can likewise replace the `32` below to alter the "dimmed" value when toggled.
```
/run local b="Brightness";local m=GetCVar(b); if tonumber(m)==50 then m=32 else m=50 end; SetCVar(b,m); print("Brightness:",m)
```

### Nameplate numbers
This will replace arena enemy names with their number if you don't want to use an addon like [Arena Names](https://www.curseforge.com/wow/addons/arena-names) to do so (this needs to be ran each time you log in)
```
/run local U=UnitIsUnit hooksecurefunc("CompactUnitFrame_UpdateName",function(F)if IsActiveBattlefieldArena()and F.unit:find("nameplate")then for i=1,3 do if U(F.unit,"arena"..i)then F.name:SetText(i)F.name:SetTextColor(1,1,0)break end end end end)
```