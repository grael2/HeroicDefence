# Welcome

This is Heroic Defence developer wiki. Add here all game related information.

* Mechanics description
* Formulas
* Anything else you feel like is fitting

Table of contents:

1. [Damage and armor system](#markdown-header-damage-and-armor-system)
2. [Technical wiki info](#markdown-header-wiki-features)
***

# Damage and armor system #

## Version 1 ##





```
#!python

Damage = (1 - armorMitigation)
```




Armor and magicArmor which follow the same formula

Function 1.0

![Bez tytułu.png](https://bitbucket.org/repo/Bre4xM/images/3162467063-Bez%C2%A0tytu%C5%82u.png)

Formula link:   
https://www.wolframalpha.com/input/?i=plot+1+-+0.004++x+%2F(1+%2B+(0.004++%7Cx%7C))+,++x%3D-0...5000 

## Version 2 (with resists)  

```
#!python


Damage = (1 - armorMitigation) * (1 - resistsOnDamageType)
```


Resists are flat similar to Grim Dawn, capped at 80%.

Damage/resist types:
* Physical
* Ranged
* Elemental
* Dark/Hex
* Divine

Requires adding damage type to every attack and variables of resists for every creature, costly from developer perspective, but allows to build more complicated systems.
***
# Offensive and Defensive Ability #

## Chance to hit ##
Chance to hit formula.

```
#!python


Probability To Hit (PTH) = ((((Attackers OA / ((Defenders DA / 3.5) + Attackers OA)) * 300) * 0.3) + (((((Attackers OA * 3.25) + 10000) - (Defenders DA * 3.25)) / 100) * 0.7)) - 50

```
## Glancing blows and crital hits ##


```
#!python

PTH Threshold 1: 70 (1.0 damage)
```


If your PTH is lower than 70, any attacks that land will do reduced damage. The damage reduction multiplier is equal to your PTH / 70 (ex. if your PTH is 65, you will do 92.86% of normal damage on a hit, or 65/70). It is highly uncommon to go below a PTH of 70, though it can happen against targets that are significantly higher level than you.

Example: PTH = 65, 1-65 hits for 93.33% damage, 66-100 misses


```
#!python

PTH Threshold 2: 90 (1.10x damage)
```


When your PTH reaches 90 and beyond, you will begin to see critical hits.

Example: PTH = 97, 1-89 hits, 90-97 critically hits for 1.1x damage, 98-100 misses


```
#!python

PTH Threshold 3: 105 (1.2x damage)
```


At PTH 100 and above, you cannot miss your target. At PTH 105+, you will begin to see the second tier of critical hits.

Example: PTH = 107, 1-89 hits, 90-104 critically hits for 1.1x damage, 105-107 critically hits for 1.2x damage


```
#!python

PTH Threshold 4: 120 (1.3x damage)
```


At PTH 120 and above, you will begin to see the third tier of critical hits.

Example: PTH = 124, 1-89 hits, 90-104 critically hits for 1.1x damage, 105-119 critically hits for 1.2x damage, 120-124 critically hits for 1.3x damage

```
#!python


PTH Thresholds 5 and 6: 130 (1.4x damage) and 135 (1.5x damage)
```


The pattern continues for the final two tiers of critical hits. Beyond the 6th threshold, you will no longer see higher critical hit values, but you will see critical hits more reliably.


Source: Taken from http://www.grimdawn.com/guide/gameplay/combat.php 
***
## Wiki features

This wiki uses the [Markdown](http://daringfireball.net/projects/markdown/) syntax. The [MarkDownDemo tutorial](https://bitbucket.org/tutorials/markdowndemo) shows how various elements are rendered. [Bitbucket documentation](https://confluence.atlassian.com/display/BITBUCKET/Use+a+wiki) has more information about how using a wiki.

The wiki itself is actually a git repository, which means you can clone it, edit it locally/offline, add images or any other file type, and push it back to us. It will be live immediately.

Go ahead and try:

```
$ git clone https://piotr_jankowiak@bitbucket.org/piotr_jankowiak/hero_defence.git/wiki
```

Wiki pages are normal files, with the .md extension. You can edit them locally, as well as creating new ones.