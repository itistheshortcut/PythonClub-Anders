# Let's make a text-based RPG game

Practice Python OOP by building a small text-based game.

**Before you start:**
You basically don't need any extra library for this. However, I used `black` to format the scripts.
So if you want to use `black` too, just create a virtualenv, and run `pip install black`.

Activate your virtualenv and when you want to re-format your code, just run `black .` (yes, the `.` is necessary)

## Easy:
- 1v1, Good guy vs Bad guy
- Create a class `Person` with attributes e.g:
    - name - string
    - hp - int
    - max_hp - int( = hp)
    - mp - int
    - max_mp - int (= mp)
    - atk_high = atk + 10
    - atk_low = atk - 10
    - action - list of string: at this level, only ["Attack"]
- class `Person` has method:
    - `get_stat()` to print out name, HP/MaxHP, MP/MaxMP
    - `generate_dmg()` return a attack damage value, randomly between atk_high and atk_low
    - `take_dmg()` take into a damage value and calculate the HP loss and return new HP points
    - `choose_action()` print out all the action options in the action list, at this stage is to print out from ["Attack"]
- Game Play:
    - The game starts with a instruction printed out, says `"This game is ....."`
    - After that is the stats of the player and enemy
    - Player plays first, start choosing action
    - At this point, only attack, after choose attack, enemy will take damage
    - Recalculate HP
    - Print out the result of this turn, how many damages has been caused by player to enemy
    - Enemy's turn
    - Call generate damage from enemy, player will take damage
    - Recalculate HP
    - Print out the result of this turn, how many damages has been caused by enemy to player
    - Print out the new stats of player and enemy
    - Check hp of player and enemy, whose hp == 0, lost
    - If hp != 0, start the loop again

## Medium:
- Create a new class called `Magic`:
    - this class will have some attributes below:
        - name - string
        - mp_cost - int
        - dmg - int
        - type - string (dark or light)
    - this class has a method to generate magic damage which will return a random value between dmg + 15 and dmg - 15

- Attribute action is now `["Attack","Magic"]`
- Add new `magic` attribute to `Person`
- Update `choose_action()` method
- For `Person`:
    - `Mp` will be deducted after each execution
    - Create new method to choose what magic to use
- Game Play:
    - create 3 - 4 instances of Magic and put it in a magic list
    - add this magic list to player and enemy  
    - Modify/add game logic when player choose magic
    - For the enemy, let's just hard code the Attack option for it at this point. In other word, enemy only use Attack, even though it has Magic but it uses only Attack
    - After each round, check hp and mp, if mp is <= 0, set mp value to 0

## Hard:
- Instantiate 1 more type of magic, not dark one, but light one
- Give `Person` ability to heal, note that:
    - If after healing, the hp is bigger than maxhp, set the hp = maxhp.
    - Else if 0 < hp < maxhp, return hp
    - And if hp < 0, set hp = 0

- In the game loop, now you have to check if the magic that the player chooses it dark or light, if the light magic is chosen:
    - print a message "Your HP is full" if after healing, new hp is max
    - print a message, something like "The light magic heals ... points of hp" if HP is not full after healing
    - Since you're healing yourself, enemy will take 0 damage

- In this mode, you will give your enemy a "brain":
    - in Enemy's turn, enemy will now select the action randomly
    - If enemy chooses magic, and the magic choice is also a random choice.

## A bit harder
- Create new class called Item, that has name, type, description, property, and quantity
- Instantiate a few more items from Item class:
    - potion - type potion, heals 50 hp and quantity of 20
    - high potion - heals 100 hp and quantity of 10
    - super potion - heals 300 hp and quantity of 5
    - elixer - type elixer, restore max HP and MP, quantity of 1
    - grenade - type attack, deal 300 damage, quantity of 2
- Give `Person` ability to choose items and perform action accordingly

## A lot more harder:
- The game should be played by teams, which mean, the "hero" team will have e.g 3 players, and the enemy will be also 3.
- Each team member of each team take turn to perform actions, still "human" goes first.
- Calculate HP after each turn, if any team member runs out of HP, aka `dead`, reduce number of member in the team.
- When every member of a team `dead`, that team loose the game.

## Consideration:
- We haven't considered to give `Person` the `def` power, which mean to reduce the amount of taken damage, and `dodge` means a chance to take no damage