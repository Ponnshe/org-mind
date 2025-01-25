
# Table of Contents

1.  [Objective](#orgf963437)
2.  [Fleeting](#org958dfdb)
    1.  [Python](#org08ba3b1)
        1.  [Planning](#org0e2fb2b)
        2.  [Implementation](#orgc8d5b4c)
3.  [See Also](#org84c565a)



<a id="orgf963437"></a>

# Objective

Zombie Dice is a quick, fun dice game from Steve Jackson Games. The players are zombies trying to eat as many human brains as possible without getting shot three times. There is a cup of 13 dice with brains,
footsteps, and shotgun icons on their faces. The dice icons are colored, and each color has a different likelihood of each event occurring. Every die has two sides with footsteps, but dice with green icons have more sides with brains, red-icon dice have more shotguns, and yellow-icon dice have an even split of brains and shotguns. Do the following on each player’s turn:

1.  Place all 13 dice in the cup. The player randomly draws three dice from the cup and then rolls them. Players always roll exactly three dice.
2.  They set aside and count up any brains (humans whose brains were eaten) and shotguns (humans who fought back). Accumulating three shotguns automatically ends a player’s turn with zero points (regardless of how many brains they had). If they have between zero and two shotguns, they may continue rolling if they want. They may also choose to end their turn and collect one point per brain.
3.  If the player decides to keep rolling, they must reroll all dice with footsteps. Remember that the player must always roll three dice; they must draw more dice out of the cup if they have fewer than three footsteps to roll. A player may keep rolling dice until either they get three shotguns—losing everything—or all 13 dice have been rolled. A player may not reroll only one or two dice, and may not stop mid-reroll.
4.  When someone reaches 13 brains, the rest of the players finish out the round. The person with the most brains wins. If there’s a tie, the tied players play one last tiebreaker round.

Install the zombiedice module with pip.

You’ll create bots by writing a class with a turn() method, which is called by the simulator when it’s your bot’s turn to roll the dice.

Template for a program:

    import zombiedice
    class MyZombie:
        def __init__(self, name):
            # All zombies must have a name:
            self.name = name
        def turn(self, gameState):
            # gameState is a dict with info about the current state of the game.
            # You can choose to ignore it in your code.
            diceRollResults = zombiedice.roll() # first roll
            # roll() returns a dictionary with keys 'brains', 'shotgun', and
            # 'footsteps' with how many rolls of each type there were.
            # The 'rolls' key is a list of (color, icon) tuples with the
            # exact roll result information.
            # Example of a roll() return value:
            # {'brains': 1, 'footsteps': 1, 'shotgun': 1,
            #  'rolls': [('yellow', 'brains'), ('red', 'footsteps'),
            #            ('green', 'shotgun')]}# REPLACE THIS ZOMBIE CODE WITH YOUR OWN:
            brains = 0
            shorguns = 0
            while diceRollResults is not None:
                brains += diceRollResults['brains']
                if brains < 2:
                    diceRollResults = zombiedice.roll() # roll again
                else:
                    break
    zombies = (
        zombiedice.examples.RandomCoinFlipZombie(name='Random'),
        zombiedice.examples.RollsUntilInTheLeadZombie(name='Until Leading'),
        zombiedice.examples.MinNumShotgunsThenStopsZombie(name='Stop at 2
    Shotguns', minShotguns=2),
        zombiedice.examples.MinNumShotgunsThenStopsZombie(name='Stop at 1
    Shotgun', minShotguns=1),
        MyZombie(name='My Zombie Bot'),
        # Add any other zombie players here.
        )
    
    # Uncomment one of the following lines to run in CLI or Web GUI mode:
    #zombiedice.runTournament(zombies=zombies, numGames=1000)
    zombiedice.runWebGui(zombies=zombies, numGames=1000)

Try writing some of your own bots to play Zombie Dice and see how
they compare against the other bots. Specifically, try to create the
following bots:

•  A bot that, after the first roll, randomly decides if it will continue
or stop
•  A bot that stops rolling after it has rolled two brains
•  A bot that stops rolling after it has rolled two shotguns
•  A bot that initially decides it’ll roll the dice one to four times, but
will stop early if it rolls two shotguns
•  A bot that stops rolling after it has rolled more shotguns than
brains


<a id="org958dfdb"></a>

# Fleeting


<a id="org08ba3b1"></a>

## Python


<a id="org0e2fb2b"></a>

### Planning

Well this coding project give us a taste of OOP (Object Oriented Programming) in Python, we do not need exactly how they work because the project give us the template so it is not that useful to experiment with classes in python.

Well I have to create five bots:

-   **ZombieRandomDecidesToRoll**
-   **ZombieStopsAfterTwoBrains**
-   **ZombieStopsAfterTwoShotguns**
-   **ZombieRandomDecidesNumRolls**
-   **ZombieStopsIfMoreShotguns**

1.  ZombieRandomDecidesToRoll

    For this zombie I will just have to use the [Python Module - random](20250119144921-python_module_random.md) specifically the choice function.
    This class should work
    
        class ZombieRandomDecidesToRoll:
            def __init__(self, name):
                self.name = name
            def turn(self, gameState):
                diceRollResults = zombiedice.roll() # first roll
                while diceRollResults is not None:
                    choice = random.choice(["r", "q"]) #r: roll , q: quit
                    if choice == "r":
                        diceRollResults = zombiedice.roll() # roll again
                    else:
                        break

2.  ZombieStopsAfterTwoBrains

    For this zombie I will have to count the brains and break the while loop when the counter reach 2.
    
    So this class should work:
    
        class ZombieStopsAfterTwoBrains:
            def __init__(self, name):
                self.name = name
            def turn(self, gameState):
                diceRollResults = zombiedice.roll() # first roll
                brains = 0
        
                while diceRollResults is not None:
                    brains += diceRollResults['brains']
                    if brains < 2:
                        diceRollResults = zombiedice.roll() # roll again
                    else:
                        break

3.  ZombieStopsAfterTwoShotguns

    This is the same that the previous one just that this time I will count shotguns instead of brains
    
    So this class should work:
    
        class ZombieStopsAfterTwoShotguns:
            def __init__(self, name):
                self.name = name
            def turn(self, gameState):
                diceRollResults = zombiedice.roll() # first roll
                shotguns = 0
        
                while diceRollResults is not None:
                    shotguns += diceRollResults["shotguns"]
                    if shotguns < 2:
                        diceRollResults = zombiedice.roll() # roll again
                    else:
                        break

4.  ZombieRandomDecidesNumRolls

    For this zombie I will have to use the random, specifically the randint function to select a random number of times to roll the dice. Also I will have to count the shotguns
    
        class ZombieRandomDecidesNumRolls:
            def __init__(self, name):
                self.name = name
            def turn(self, gameState):
                times_to_roll = random.randint(1,4)
                diceRollResults = zombiedice.roll() # first roll
                rolls = 1
                shotguns = 0
        
                while diceRollResults is not None and rolls < times_to_roll:
                    shotguns += diceRollResults["shotguns"]
                    if shotguns < 2:
                        diceRollResults = zombiedice.roll() # roll again
                        rolls+=1
                    else:
                        break

5.  ZombieStopsIfMoreShotguns

    This is simple too, I just have to count the brains and shotguns, and compare them.
    
        class ZombieStopsIfMoreShotguns:
            def __init__(self, name):
                self.name = name
            def turn(self, gameState):
                diceRollResults = zombiedice.roll() # first roll
                brains = 0
                shotguns = 0
        
                while diceRollResults is not None:
                    brains += diceRollResults["brains"]
                    shotguns += diceRollResults["shotguns"]
                    if shotguns < brains:
                        diceRollResults = zombiedice.roll() # roll again
                    else:
                        break


<a id="orgc8d5b4c"></a>

### Implementation

There were some errors with the name of the keys, specially with "shotguns" because the key is not "shotguns" it is shotgun, but apart from that, tha classes were well defined.
This is the final code for the program

    import zombiedice
    import random
    
    class ZombieRandomDecidesToRoll:
        def __init__(self, name):
            self.name = name
        def turn(self, gameState):
            diceRollResults = zombiedice.roll() # first roll
            while diceRollResults is not None:
                choice = random.choice(["r", "q"]) #r: roll , q: quit
                if choice == "r":
                    diceRollResults = zombiedice.roll() # roll again
                else:
                    break
    
    class ZombieStopsAfterTwoBrains:
        def __init__(self, name):
            self.name = name
        def turn(self, gameState):
            diceRollResults = zombiedice.roll() # first roll
            brains = 0
    
            while diceRollResults is not None:
                brains += diceRollResults['brains']
                if brains < 2:
                    diceRollResults = zombiedice.roll() # roll again
                else:
                    break
    
    class ZombieStopsAfterTwoShotguns:
        def __init__(self, name):
            self.name = name
        def turn(self, gameState):
            diceRollResults = zombiedice.roll() # first roll
            shotguns = 0
    
            while diceRollResults is not None:
                shotguns += diceRollResults["shotgun"]
                if shotguns < 2:
                    diceRollResults = zombiedice.roll() # roll again
    
                else:
                    break
    
    class ZombieRandomDecidesNumRolls:
        def __init__(self, name):
            self.name = name
        def turn(self, gameState):
            times_to_roll = random.randint(1,4)
            rolls = 1
    
            diceRollResults = zombiedice.roll() # first roll
            rolls += 1
            shotguns = 0
    
            while diceRollResults is not None and rolls < times_to_roll:
                shotguns += diceRollResults["shotgun"]
                if shotguns < 2:
                    diceRollResults = zombiedice.roll() # roll again
                    rolls+=1
                else:
                    break
    
    class ZombieStopsIfMoreShotguns:
        def __init__(self, name):
            self.name = name
        def turn(self, gameState):
            diceRollResults = zombiedice.roll() # first roll
            brains = 0
            shotguns = 0
    
            while diceRollResults is not None:
                brains += diceRollResults["brains"]
                shotguns += diceRollResults["shotgun"]
                if shotguns < brains:
                    diceRollResults = zombiedice.roll() # roll again
                else:
                    break
    
    zombies = (
        zombiedice.examples.RandomCoinFlipZombie(name='Random'),
        zombiedice.examples.RollsUntilInTheLeadZombie(name='Until Leading'),
        zombiedice.examples.MinNumShotgunsThenStopsZombie(name='Stop at 2 Shotguns', minShotguns=2),
        zombiedice.examples.MinNumShotgunsThenStopsZombie(name='Stop at 1 Shotgun', minShotguns=1),
        ZombieRandomDecidesToRoll(name = "Randomly decides if to roll"),
        ZombieStopsAfterTwoBrains(name = "Stops at two brains"),
        ZombieStopsAfterTwoShotguns(name="Stops after two shotguns"),
        ZombieRandomDecidesNumRolls(name="Randomly Decides the number of rolls"),
        ZombieStopsIfMoreShotguns(name="Stops if gets more shotguns than brains"),
        # Add any other zombie players here.
        )
    
    # Uncomment one of the following lines to run in CLI or Web GUI mode:
    #zombiedice.runTournament(zombies=zombies, numGames=1000)
    zombiedice.runWebGui(zombies=zombies, numGames=1000)


<a id="org84c565a"></a>

# See Also

-   [Python Dictionary](20250111130125-python_dictionary.md)
-   [Python List](20250111131854-python_list.md)
-   [Python Tuples](20250114030727-python_tuples.md)

-[Python Classes](20250119143902-python_classes.md) 

