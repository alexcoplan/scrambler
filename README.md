# scrambler

Generates a random and efficient scrambling algorithm to scramble a 3x3 rubik's cube.

## how it works?

magic

## no, seriously...

 - There are six sides of the cube which we can rotate: `[F, B, L, R, U, D] => [front, back, left, right, up, down]`
 - We can rotate them clockwise (considered a "standard" move i.e. front => `F`)
 - We can rotate them anticlockwise ("inverted" or "prime" move i.e. front prime => `F'`)
 - We can rotate them 180 degrees (double turn or 180 turn, i.e. front 2 => `F2`)

The planes of the cube are the x plane (with corresponding sides L and R), the y plane (with corresponding sides U and D), and the z plane (with corresponding sides F and B).

We can start with an algorithm that just chooses random sides and modifiers of those sides to generate moves. However, that generates scrambles with sequences like this: `F F'`, or `R L R'`.

What's wrong with both those sequences? The first one undoes itself. Since we can do any possible move on a side with either the standard, inverted, or double turn move, then we can assume that we do not want to follow a move by another move on the same side. Any two moves on the same side can expressed in terms of one move on that side, and therefore are wasted or even deterimental moves in our scramble (as shown above).

The second one is slightly more complex, as using our new rule, it appears to be valid. What's wrong here, is that a move on the R side followed by one on the L introduces no complexity to the cube, since both sides are on the same plane (x axis). When the R side is then inverted, the cube returns to it's original state with only the L applied. It is entirely valid to follow a move by another on the same plane (e.g. `R L`), however, the subsequent move must *not* be on this plane (i.e. must not be either R or L).

Using these two rules, the algortihm generates an efficient and complex scramble. 