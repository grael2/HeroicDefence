# Welcome

Welcome to your wiki! This is the default page we've installed for your convenience. Go ahead and edit it.

## Wiki features

This wiki uses the [Markdown](http://daringfireball.net/projects/markdown/) syntax. The [MarkDownDemo tutorial](https://bitbucket.org/tutorials/markdowndemo) shows how various elements are rendered. [Bitbucket documentation](https://confluence.atlassian.com/display/BITBUCKET/Use+a+wiki) has more information about how using a wiki.

The wiki itself is actually a git repository, which means you can clone it, edit it locally/offline, add images or any other file type, and push it back to us. It will be live immediately.

Go ahead and try:

```
$ git clone https://piotr_jankowiak@bitbucket.org/piotr_jankowiak/hero_defence.git/wiki
```

Wiki pages are normal files, with the .md extension. You can edit them locally, as well as creating new ones.

## Syntax highlighting


You can also highlight snippets of text (we use the excellent [Pygments][] library).

[Pygments]: http://pygments.org/


Here's an example of some Python code:

```
#!python

def wiki_rocks(text):
    formatter = lambda t: "funky"+t
    return formatter(text)
```


You can check out the source of this page to see how that's done, and make sure to bookmark [the vast library of Pygment lexers][lexers], we accept the 'short name' or the 'mimetype' of anything in there.
[lexers]: http://pygments.org/docs/lexers/


Have fun!

***

# Damage and armor system #

## Version 1 ##

***Damage = (1 - armorMitigation)***

Armor and magicArmor which follow the same formula

![Bez tytułu.png](https://bitbucket.org/repo/Bre4xM/images/3162467063-Bez%C2%A0tytu%C5%82u.png)

Formula link:   
https://www.wolframalpha.com/input/?i=plot+1+-+0.004++x+%2F(1+%2B+(0.004++%7Cx%7C))+,++x%3D-0...5000 

## Version 2 (with resists)  

***Damage= (1 - armorMitigation) * (1 - resistsOnDamageType).***

Resists are flat similar to Grim Dawn, capped at 80%.

Damage/resist types:
* Physical
* Ranged
* Elemental
* Dark/Hex
* Divine

Requires adding damage type to every attack and variables of resists for every creature, costly from developer perspective, but allows to build more complicated systems.