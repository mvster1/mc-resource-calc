mc-resource-calc
=================

a minecraft crafting resource calculator. one html file, no build, no
dependencies, no framework, no server. open it and it works.

what it does
------------
you name an item and a quantity, it tells you the exact ingredients the
vanilla crafting recipe requires, scaled to that quantity. that's it. it
does not walk the full tree down to raw ores by default, it shows the
recipe as it exists in the crafting table, one level, same as the game.

you can also queue several items into a list and get the combined total
across all of them in one pass.

quantities over 64 are shown with a stack breakdown in parentheses,
because that's how you think about inventory space in this game.

why
---
every "minecraft calculator" on the internet is a react app with a
build step, a node_modules folder, ads, and a spinner. this is one
file. view source and you have the whole program.

data
----
recipes are not hand-typed. they are parsed directly from vanilla's
own data generator output (data/minecraft/recipe/*.json, the same
files the game itself ships): crafting_shaped, crafting_shapeless,
smelting/blasting/smoking/campfire_cooking, stonecutting, and
smithing_transform. brewing and the cosmetic special-case recipes
(banner duplication, firework stars, map extending, ...) are left out
on purpose, they don't belong in a materials calculator.

where the source data disagreed with itself (an item craftable two
different ways, or a reverse "uncraft the block back into ingots"
recipe competing with the real one) the parser picks the canonical
path: mined ore over decorative block, built-from-scratch over
recolor-an-existing-one. ~1076 items total.

usage
-----
locally:
    open index.html

    no build, no server, no deps. just open the file.

or use the github page (same file, hosted):
    https://mvster1.github.io/mc-resource-calc/

either way the procedure is identical:

    1. type an item name, underscores or spaces both work
    2. type a quantity
    3. calculate        -> shows that item's direct recipe
       add to list      -> queues it instead
    4. calculate list   -> sums every queued item into one table

the footer switches the interface language between en and
pt-br on the fly (default: en).

structure
---------
    index.html   everything. markup, css, the recipe table, the logic.

one file on purpose. no separation of concerns beyond what fits in
your head at once. if you want to add or fix a recipe, ctrl-f the
item name in the R{} object and edit the number.

philosophy
----------
this project follows the suckless (suckless.org) and werc
(werc.cat-v.org) approach to software: do one thing, keep the whole
thing readable in one sitting, prefer deleting code to adding a
config flag for it. a resource calculator does not need a framework,
a package.json, or an api. it needs an item name, a number, and
arithmetic.

	the more code you have removed, the more progress you have made.

license
-------
public domain. do whatever.