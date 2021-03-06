Potion Recipe Maker
===================

Randomly generate potion recipes for tabletop roleplaying games. Generates recipes such as

    - 28 g of Dragon Salt
    - 20 ml of Gnoll Spit
    - 24 g of Nightmare Skin
    - 6 Spider Teeth
    - 50 ml of Titan Extract

You can also guarantee that a given set of creature types will appear in the potion; Potions of Dragon Control should contain something from a dragon for example.

User Interface
==============

This program comes with two different user interfaces; `potion_recipe_maker.rb` contains a command line interface (which is referred to throughout this file), and `potion_recipe_maker_gui.rb` contains a graphical user interface. The GUI version requires `FXRuby` to run, the CLI version has no dependencies.

Data Files
==========

Combines the name of a creature from `creatures.txt` with a body part/ingredient type from `creatureParts.txt`. Syntax for `creatures.txt` is

    creature_name:  rarity ![item1 item2 ...]
  
where `rarity` takes the value `common`, `uncommon`, `rare`, or `very_rare`. Rarity is weighted according to powers of 2, so `rare` is twice as likely to occur as `very_rare` and 4 times as unlikely to occur as `common`. The `!` is optional and is for denoting the list (which is also optional) as a blacklist instead of a whitelist. If a whitelist is given then only creature parts in the list can be used to make each ingredient. If a blacklist is given then only parts *not* inside the list can be used to make each ingredient. For example,

    Cyclops: rare [Eyes]
    
will stop any ingredients involving a Cyclops except Cyclops Eyes from occuring, and

    Worm: common ![Teeth]

will stop Worm Teeth from occuring.

Syntax for `creatureParts.txt` is

    part: property1 property2 property3 ...
  
where each property is on the same line and separated by whitespace. Currently there are only 4 recognised properties that should not be used together; `solid`, `countable`, `fluid`, and `gaseous`. `solid`s are measured in grams (g), `fluid`s are measured in millilitres (ml), and `countable` and `gaseous` are just a number or 'some', respectively.

Guaranteeing Creatures
======================

Creatures can be guaranteed to occur by entering a comma separated list of them when prompted

    How many ingredients?
    3
    Specific creatures to include?
    Cow, Dragon, Wolf
     - some Wolf Scent
     - 100 ml of Dragon Bile
     - 60 ml of Cow Bile

The whitespace is irrelevant, so `Cow, Dragon` is the same as `Cow,Dragon`.
