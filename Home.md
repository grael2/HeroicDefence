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

Chance to hit formula. Taken from http://www.grimdawn.com/guide/gameplay/combat.php 
```
#!python


Probability To Hit (PTH) = ((((Attacker's OA / ((Defender's DA / 3.5) + Attacker's OA)) * 300) * 0.3) + (((((Attacker's OA * 3.25) + 10000) - (Defender's DA * 3.25)) / 100) * 0.7)) - 50

```

***
## Wiki features

This wiki uses the [Markdown](http://daringfireball.net/projects/markdown/) syntax. The [MarkDownDemo tutorial](https://bitbucket.org/tutorials/markdowndemo) shows how various elements are rendered. [Bitbucket documentation](https://confluence.atlassian.com/display/BITBUCKET/Use+a+wiki) has more information about how using a wiki.

The wiki itself is actually a git repository, which means you can clone it, edit it locally/offline, add images or any other file type, and push it back to us. It will be live immediately.

Go ahead and try:

```
$ git clone https://piotr_jankowiak@bitbucket.org/piotr_jankowiak/hero_defence.git/wiki
```

Wiki pages are normal files, with the .md extension. You can edit them locally, as well as creating new ones.