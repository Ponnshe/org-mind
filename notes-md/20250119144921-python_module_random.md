
# Table of Contents

1.  [Functions](#org369b911)
    1.  [random.choice(seq)](#org1e944a5)
        1.  [Use cases](#org654ac39)
    2.  [random.randrange(stop), random.randrange(start, stop[, step])](#org8c81ce8)
    3.  [random.randint(a, b)](#org256c10f)

This module generate pseudo-random numbers


<a id="org369b911"></a>

# Functions


<a id="org1e944a5"></a>

## random.choice(seq)

Return a random element from the non-empty sequence seq. If seq is empty, raises IndexError.


<a id="org654ac39"></a>

### Use cases

1.  Randomly decide to roll a dice

        while True:
            choice = random.choice(["r", "q"]) #r: roll , q: quit
            if choice == "r":
                diceRollResults = zombiedice.roll() # roll again
            else:
                break

2.  Randomly decide what to eat

        menu = ["spaghetti", "lassagna", "raviolis", "sushi", "onion soup"]
        print("I will eat:", random.choice(menu))


<a id="org8c81ce8"></a>

## random.randrange(stop), random.randrange(start, stop[, step])

Return a randomly selected element from `range(start, stop, step).`

This is roughly equivalent to `choice(range(start, stop, step))` but supports arbitrarily large ranges and is optimized for common cases.

The positional argument pattern matches the `range()` function.

Keyword arguments should not be used because they can be interpreted in unexpected ways. For example `randrange(start=100)` is interpreted as `randrange(0, 100, 1).`


<a id="org256c10f"></a>

## random.randint(a, b)

Return a random integer N such that a <= N <= b. Alias for randrange(a, b+1).

