# Welcome
This is Heroic Defence developer wiki. Add here all game related information.

This game is created by our 2 person team: Piotr Jankowiak and Piotr Kałużny. It is written in C# and is made only from the free assets and samples that were changed and rewritten for our purposes.
Notably:
- Inventory Master (https://www.assetstore.unity3d.com/en/#!/content/26310).
- Magic Pack (https://www.assetstore.unity3d.com/en/#!/content/36269).
- Medieval Castle (https://www.assetstore.unity3d.com/en/#!/content/51230).
- RPG Character Animation Pack (https://www.assetstore.unity3d.com/en/#!/content/65284).
- Tileable Painted Ground Textures (https://www.assetstore.unity3d.com/en/#!/content/62018).
- RPG Inventory Icons (https://www.assetstore.unity3d.com/en/#!/content/56687),
And a lot of models and "creature packs", also models from other sources than assetstore that are included in our internal source base.
- RPG icons (http://7soul1.deviantart.com/art/420-Pixel-Art-Icons-for-RPG-129892453).

# Game Description #
Game purpose is to defend the Castle from the waves of incoming creatures. The game includes:
- Point to click hack&slash RPG interface.
- Inventory and statistics system (if you liked Diablo or Titan Quest you will appreciate it).
- Skill and attributes system with working Buffs and AOE.
- Functional shop and itembase.
- Loot system.
- Active items - e.g. potions with stacking and hotbar use.
- Waves of different spawning enemies.

Quick demo video: https://my.mixtape.moe/sxsngq.webm (from Project view - not standalone game). The file is also uploaded in the repository.

# Screenshots #
![main menu](https://raw.githubusercontent.com/grael2/HeroicDefence/master/Screenshots/6.png)
![fighting](https://raw.githubusercontent.com/grael2/HeroicDefence/master/Screenshots/1.png)
![spells](https://raw.githubusercontent.com/grael2/HeroicDefence/master/Screenshots/2.png)
![items](https://raw.githubusercontent.com/grael2/HeroicDefence/master/Screenshots/3.png)
![shop](https://raw.githubusercontent.com/grael2/HeroicDefence/master/Screenshots/4.png)
![talents](https://raw.githubusercontent.com/grael2/HeroicDefence/master/Screenshots/5.png)


# Technical wiki stuff #
* Mechanics description
* Formulas
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

Formula 1.0

![Bez tytułu.png](http://i.imgur.com/AfXAFDf.png)

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

Formula 2.0
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

In our version the crit modifiers are: 1.2, 1.4, 1.6, 1.8 and 2.0 since we won't have "Critical damage" statistic
Source: http://www.grimdawn.com/guide/gameplay/combat.php 

***
# Player statistics #

## Dexterity ##

| Stat | Rating/flat increase | Function |
|------|----------------------|----------|
|Offensive ability| Rating | +0.5 OA  |
|Defensive ability| Rating | +0.5 DA  |
|Speed | Rating | +0.33% moveSpeed up to +50% cap |
|Attack speed | Rating |-0.33% attackSpeed up to -100% cap |

## Intellect ##

| Stat | Rating/flat increase | Function |
|------|----------------------|----------|
| Mana | Flat increase | +5 mana|
| Mana regeneration | Flat increase | +0.05 manaPerSecond | 
| Resist | Rating | Formula 1.0 |
| Ability damage | Rating | +0.33% abilityDamage |


## Strength ##

| Stat | Rating/flat increase | Function |
|------|----------------------|----------|
| Health  | Flat increase | +5 maxHealth |
| Health regeneration | Flat increase | +0.05 healthPerSecond |
|Physical damage  | Rating | +0.33% attackPower |
| Armor  | Rating | +0.33% armor |

