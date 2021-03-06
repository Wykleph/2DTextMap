## 2DTextMap

So back in high school we made games with QBasic and I wanted to see if I could make a game based on ASCII/unicode characters in python instead.  As part of that, I want to be able to create maps that the player can move around on without having to hard-code the x/y coordinate for every map object.

Since it was going to be a simple little ASCII/unicode game, I figured I would make the levels text-based(at least for now).

Level's are built with text.  A `token` is a character like `#` that represents something(in this case a wall:

    ##################
    #                #
    #                #
    #                #
    #                #
    #                #
    ##################

Each `token` is converted to the character that will be displayed on the map.  Since this is a wall, the `Wall` object will figure out how to display itself based on its neighbors(and ends up looking like lines ─┘).

Here is a more complex example:

    #########################################################
    #$         #f                             #             #
    #          #                              |             #
    #          #                              |             #
    #####--#####                              #             #
    #                                         #             #
    |                 ###########             #             #
    |                 #wwwwwwwww#             ###############
    |                 #wwwwwwwww#             #            $#
    #                 #wwwwwwwww#             #             #
    #                 ###########             #             #
    #                                         |             #
    #                                         |             #
    #                                         #             #
    #########################################################

Turns into something like:

    ┌──────────┬──────────────────────────────┬─────────────┐
    │$         │                             │             │
    │          │                              ▒             │
    │          │                              ▒             │
    ├────▒▒────┘                              │             │
    │                                         │             │
    ▒                 ┌─────────┐             │             │
    ▒                 │▒▒▒▒▒▒▒▒▒│             ├─────────────┤
    ▒                 │▒▒▒▒▒▒▒▒▒│             │            $│
    │                 │▒▒▒▒▒▒▒▒▒│             │             │
    │                 └─────────┘             │             │
    │                                         ▒             │
    │                                         ▒             │
    │                                         │             │
    └─────────────────────────────────────────┴─────────────┘

(github doesn't format it exactly correct.  The lines are broken and 
nothing is colored.)

There are 2 objects for the mapping, `MapBuilder` & `Map`.
And some example objects that inherit from `MapObject`: `Ground`, `Wall` & `Door`.

`MapBuilder` builds up a `Map` object and populates the `Map` instance with `MapObjects` based on `token`s in the text representing the map.

The `MapObject` objects actually place themselves on the `Map` through their `place` method and have access to the `Map` being built. `MapObject`s can also control how they are displayed.  The `Wall`s have a mind of their own :P

The `MapBuilder` supports adding `MapObject`s through classes(passed in a dict with the `build` method) so adding and editing map objects is really flexible.

[Here is an imgur gallery with a better example](http://imgur.com/gallery/NUvXy).  Those wouldn't be levels in the game, but it shows how it converts everything to the appropriate box character :D  [Here is what an outline of a room might look like.](http://imgur.com/gallery/KtLRz)

You can run the code in `example.py` to see how to display the built up `Map` object.  You might need to make your terminal window larger to run it since it might try to draw outside of the terminal window otherwise.

Other than that, things are pretty self-explanatory.  If you run the code and look at the 2 files, you'll see what is going on.

API Documentation is going to be in the help strings for each object until I can find the time to generate some docs.
