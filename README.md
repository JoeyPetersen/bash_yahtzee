# bash_yahtzee

I was making some changes to the script so it would be easy to select a
different amount of dice and I noticed that the new one was hitting Yahtzee in
much fewer rolls, so now I'm comparing them and adding some statistics to see
if I can figure out why that's happening.

Output from old_playyahtzee:

$ ./old_playyahtzee | grep YAHT
After 9033 rolls, I got a YAHTZEE!
After 4158 rolls, I got a YAHTZEE!
After 2749 rolls, I got a YAHTZEE!
After 7221 rolls, I got a YAHTZEE!
After 42046 rolls, I got a YAHTZEE!
After 741 rolls, I got a YAHTZEE!

Output from playyahtzee:

After 1 rolls, I got a YAHTZEE!
After 2 rolls, I got a YAHTZEE!
After 0 rolls, I got a YAHTZEE!
After 1 rolls, I got a YAHTZEE!
After 1 rolls, I got a YAHTZEE!
After 18 rolls, I got a YAHTZEE!

The kicker? I noticed that my original was rolling 6 dice (instead of 5 for the actual game), 
so I increased the amount of dice the new one was rolling and it was still low. The above 
output is with it at 7 dice.

Here are some roll output from the both of them. I made sure that they were all getting random
numbers 1-6:

Output from old_playyahtzee:

$ ./old_playyahtzee | grep "Here"
Here is what I rolled: 3 5 5 6 2 2
Here is what I rolled: 2 2 4 5 4 4
Here is what I rolled: 3 2 6 1 1 3
Here is what I rolled: 2 5 3 5 2 6
Here is what I rolled: 1 1 4 5 6 4
Here is what I rolled: 1 2 3 6 4 3
Here is what I rolled: 5 2 3 2 5 3
Here is what I rolled: 1 6 2 5 2 6
Here is what I rolled: 3 1 4 2 5 6
Here is what I rolled: 4 6 6 6 1 4

$ ./playyahtzee | grep "Here"
Here is what I rolled: 2 6 6 6 4 4 3
Here is what I rolled: 1 5 2 5 1 6 1
Here is what I rolled: 6 4 6 5 5 3 5
Here is what I rolled: 2 4 4 3 2 6 2
Here is what I rolled: 3 1 5 1 3 2 6
Here is what I rolled: 5 4 2 4 5 3 6
Here is what I rolled: 1 4 4 2 6 5 1
Here is what I rolled: 6 2 4 2 5 3 6
Here is what I rolled: 6 2 3 6 4 1 1
Here is what I rolled: 3 1 4 6 5 1 5

I ran a test I should have checked before and found that it was my stupid match check. I need to 
break that loop when there isn't a match. The problem here is that if the first and last die match,
it's marked as a Yahtzee.

Once I fixed it:

$ ./playyahtzee | grep YAHT
After 681 rolls, I got a YAHTZEE!
After 5738 rolls, I got a YAHTZEE!
After 1602 rolls, I got a YAHTZEE!
After 16939 rolls, I got a YAHTZEE!
After 23538 rolls, I got a YAHTZEE!

Now to see how often the computer can roll a one-roll Yahtzee with 5 dice:

$ ./playyahtzee | grep YAHT
After 316 rolls, I got a YAHTZEE!
After 2730 rolls, I got a YAHTZEE!
After 992 rolls, I got a YAHTZEE!
After 586 rolls, I got a YAHTZEE!
After 1515 rolls, I got a YAHTZEE!
After 2536 rolls, I got a YAHTZEE!
After 751 rolls, I got a YAHTZEE!

Looks right. Now on to having it collect more stats.
