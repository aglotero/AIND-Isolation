# Mastering the game of Go with deep neural networks and tree search

## The problem

Games with perfect information have a function to calculate the game outcome, 
using this function you can build a tree with all possible moves and search in this
tree the next move that takes you on a win situation.

Besides, the complexity increases as the board size and quantity of moves increases. 
Such games has a tree of size `b^d` where `b` is the number of legal moves per move
and `d` is the length of the game.   
 
Monte Carlo Tree Search (MCTS) is used on others games with super human performance, but in Go this
technique achieves an Amateur level of accuracy. This is possible due to the combination of tree search
with a Policy to mimic human moves, this police allows MCTS to select moves more likely to be made by
experts and ignore moves with low probability to be made.

## Methods

The AlphaGo team uses a combination of neural networks to play.

The first is a Neural Network to search for moves mimetizing expert moves, called Supervised Learning 
Policy Network (SL). This network is trained using a supervised method based on expert moves.

The second is a Reinforcement Learning Policy Network (RL), this network is identical in structure to SL
network, but is trained using a unsupervised learning.

This two networks aim to narrow the search on the game value tree, each one with own speed and accuracy,
giving as output a probability distribution of moves on a given board.

The third network aim to evaluate the game outcome giving a board, it is trained using supervised
learning.

To make a move the AlphaGo mix these tree networks in a MCTS search, using the Monte Carlo Simulation to
find nodes on game tree evaluating the tree networks to decide where to go on tree search. This is possible
to achieve on a feasible time due to the combination of Hardware (48 CPUs + 18 GPUs) and accuracy of the
networks outcomes.

## Results

Against other software players (Fuego, Crazy Stone, Zen and Pachi) AlphaGo wins 99.8% of the time,
against another AplhaGo player the win ratio is about 77%.

Against the best human player AlphaGo win 5 games of 5. 

## Why this is important?

This is the first time that neural networks are used side-by-side with tree search
on a hybrid approach to solve a hard problem. Thus the mix of Supervised and Reinforcement Learning
is an unprecedented feat.

Maybe win Go isn't so important per se, but more studies in hybrid approaches is.