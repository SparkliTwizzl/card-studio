# structure


## modes

two modes, one for editing game systems and one for editing cardsets.


---
## game mode


### games

define and contain everything related to a game system.

when making a new version of a game, migration rules can be defined to automatically update card content.
this is a potentially destructive and thus non-reversible operation.
    - example:
        - Game v1.6.0 contains a number field "size", a text field "title", and a text field "subtitle"
        - Game v1.7.0 changes the name of "size" to "height", removes "title" and "subtitle", and adds a text field "name"
        - when updating a cardset from Game v1.6.0 to v1.7.0, for each card:
            - all "size" values are copied to the "height"  field
            - all "title" and "subtitle" values are combined and copied into the "name" field
            - all "size", "title", and "subtitle" values are discarded

can be exported for distribution.

when importing, check user's installed games.
    - if not present, install
    - if present and version matches, do nothing and inform user that they already have it
    - if present and version doesnt match, ask user if they want to keep the higher version number or keep both
        - EXAMPLE: user imports Magic: The Gathering v3.6.0
            - app finds an existing game called Magic: The Gathering with version number v3.6.0
                - app does not install the imported game
                - app opens a popup window saying "Magic: The Gathering v3.6.0 is already installed"
            - app finds an existing game called Magic: The Gathering with version number 3.7.0
                - app opens a popup window saying "a newer version of Magic: The Gathering is already installed (v3.7.0), do you want to keep both versions or use the newer version?"
                    - the user clicks "use newer"
                        - app does not install the imported game
                    - the user clicks "keep both"
                        - app installs the imported game
                        - app does not uninstall the other version of the imported game
            - app finds an existing game called Magic: The Gathering with version number 3.5.0
                - app opens a popup window saying "an older version of Magic: The Gathering is already installed (v3.5.0), do you want to keep both versions or use the newer version?"
                    - the user clicks "use newer"
                        - app installs the imported game
                        - app uninstalls the other version of the imported game
                    - the user clicks "keep both"
                        - app installs the imported game
                        - app does not uninstall the other version of the imported game


#### fields

define the names and types for all the different value entry fields that can appear on cards.


#### card designs

define the layout, appearance, and fields for each type of card.


#### cardlist templates

define any templated cardlists (subsets of cardsets) for autogeneration in cardset mode.


---
## card mode


### cardsets

cardset projects link to the game system they use, and bundle the game system with themselves when exported for distribution.

when changing the version of a game that a cardset uses, if anything in the game was removed or renamed in the newer version, app will prompt user to confirm that they want to irreversibly migrate their content, then automatically update cards using the defined migration rules.


#### assets

define and include any text, numerical, etc values, images, or procedural elements such as gradients, functions, etc for generating images.


#### cards

define cards using a game system and a collection of assets.
