---
layout: post
title: Rock Paper Scissor
---

Rock, Paper, Scissor is a classic game. Have you ever thought, though, how many games *on average* do you have to play to win or lose against another person, assuming that both choose randomly? Maybe you'd win or lose on the first try, or the second try, but the game surely cannot go that long, unless you keep getting ties? So on average, how many games would you have to play? Let's find out!

First, let's play a few games of Rock, Paper, Scissor against an RNG!

```
beat = {'rock': 'scissor', 'scissor': 'paper', 'paper': 'rock'}

def rock_paper_scissor():
    c = input('Rock, Paper, Scissor. Shoot! ').lower()
    ai = random.choice(['rock', 'paper', 'scissor'])
    print('AI chooses: {choice}. {result}!'.format(choice=ai.title(), result='Tie' if c == ai else 'You win' if beat[c] == ai else 'You lose'))

rock_paper_scissor()
```

How many games did it take you to win or lose? Let's explore this problem using both theory and simulations. First, mathematically, whatever the AI picks, we have 2 in 3 chances of either winning or losing, i.e., the game ends, and 1 in 3 chances of getting a tie. Let $E[X]$ be the expected number of games taken place, we have:

$E[X] = \frac{2}{3} + \frac{1}{3}(E[X] + 1)$

Let's break it down! When we play a game of RPS, in 2 in 3 chances, the game ends, the number of game stays the same, but in 1 in 3 chances, the players tie and the number of games increases by 1 (i.e., the game we played), hence $\frac{1}{3}(E[X] + 1)$. [Solving this equation](https://www.wolframalpha.com/input/?i=solve+for+y%3A+y+%3D+%282%2F3%29+%2B+%281%2F3%29+%28y+%2B+1%29) gives us:

$E[X] = \frac{3}{2} \text{ or } 1.5$

Let's compare with simulations!

```
# evaluates two ais
def rps_result(c1, c2):
    if c1 == c2: return 0
    elif beat[c1] == c2: return 1
    else: return -1

# two ais sitting in a tree, rock paper scissor RNG
def fast_rps():
    ais = random.choices(['rock', 'paper', 'scissor'], k=2)
    return rps_result(*ais)
```

 
