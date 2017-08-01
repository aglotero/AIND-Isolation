# Custom Score Functions

## AB_Custom

A more aggressive version of "Open Moves" metric suggest on the course material.

In this version we multiply the opp_moves by 2 to force the current player to pursue the opponent.

### Pros

Is cheap to compute.

### Cons

As the opponent has better search strategies this function is unable to capture the game score, and begin to fail against smarter opponents.

## AB_Custom_2

When a board has a partition we, immediately, can determine the final result: the player in the largest partition win.

This function gives high scores to boards with partition with player has more moves, otherwise returns the flat "Open Moves" metric.

### Pros

As soon we find one partition we win the game.

### Cons

Takes more time to compute.

## AB_Custom_3

Pursue boards that have more equal moves but less unique moves form opponent.

As we transform the opponent options in a subset of my own options we gain advantage to isolate him.

### Pros

Is cheap to compute.

### Cons

n/a.

# Tournament evaluation

To reduce the variability of the test due to random initializations, I increase the total games from 5 to 50 and run for three times.


| Match |   Opponent   |AB_Improved | AB_Custom  |AB_Custom_2 |AB_Custom_3 |
|-------|--------------|------------|------------|------------|------------|
|       |              | Won / Lost | Won / Lost | Won / Lost | Won / Lost |
|    1  |    Random    | 91  /   9  | 90  /  10  | 94  /   6  | 88  /  12  |
|    2  |    MM_Open   | 66  /  34  | 82  /  18  | 73  /  27  | 66  /  34  |
|    3  |   MM_Center  | 93  /   7  | 86  /  14  | 77  /  23  | 82  /  18  |
|    4  |  MM_Improved | 72  /  28  | 71  /  29  | 77  /  23  | 61  /  39  |
|    5  |    AB_Open   | 40  /  60  | 49  /  51  | 44  /  56  | 44  /  56  |
|    6  |   AB_Center  | 54  /  46  | 60  /  40  | 48  /  52  | 38  /  62  |
|    7  |  AB_Improved | 52  /  48  | 49  /  51  | 44  /  56  | 33  /  67  |
|       |    Win Rate  |    66.9%   |   69.6%    |    65.3%   |    58.9%   |


| Match |   Opponent   |AB_Improved |AB_Custom   |AB_Custom_2 |AB_Custom_3 | 
|-------|--------------|------------|------------|------------|------------| 
|       |              | Won / Lost | Won / Lost | Won / Lost | Won / Lost |
|    1  |    Random    | 97  /   3  | 94  /   6  |  96  /  4  | 89  /  11  |
|    2  |    MM_Open   | 72  /  28  | 69  /  31  |  79  / 21  | 65  /  35  |
|    3  |   MM_Center  | 88  /  12  | 87  /  13  |  90  / 10  | 77  /  23  |
|    4  |  MM_Improved | 72  /  28  | 71  /  29  |  67  / 33  | 55  /  45  |
|    5  |    AB_Open   | 57  /  43  | 50  /  50  |  57  / 43  | 42  /  58  |
|    6  |   AB_Center  | 56  /  44  | 51  /  49  |  54  / 46  | 38  /  62  |
|    7  |  AB_Improved | 50  /  50  | 52  /  48  |  48  / 52  | 40  /  60  |
|       |   Win Rate:  |   70.3%    |   67.7%    |    70.1%   |  58.0%     |


| Match |   Opponent   |AB_Improved |AB_Custom   |AB_Custom_2 |AB_Custom_3 |
|-------|--------------|------------|------------|------------|------------|
|       |              | Won / Lost | Won / Lost | Won / Lost | Won / Lost |
|   1   |   Random     | 91  /   9  | 90  /  10  | 92  /   8  | 90  /  10  |
|   2   |   MM_Open    | 74  /  26  | 73  /  27  | 71  /  29  | 59  /  41  |
|   3   |  MM_Center   | 89  /  11  | 92  /   8  | 82  /  18  | 86  /  14  |
|   4   | MM_Improved  | 71  /  29  | 65  /  35  | 71  /  29  | 64  /  36  |
|   5   |   AB_Open    | 49  /  51  | 44  /  56  | 53  /  47  | 41  /  59  |
|   6   |  AB_Center   | 54  /  46  | 58  /  42  | 57  /  43  | 49  /  51  |
|   7   | AB_Improved  | 52  /  48  | 47  /  53  | 51  /  49  | 41  /  59  |
|       |   Win Rate:  |  68.6%     |  67.0%     |  68.1%     |  61.4%     |



The `AB_Improved` function performs better than each heuristic alone.

To outperform `AB_Improved` I believe that a mix of heuristics must be created, varying the heuristic as the game goes on.

For example, `AB_Custom` at the beginning of the game can be a good start as the board is full of spaces, after a certain
threshold of board occupation we can use `AB_Custom_2` as the search of partitions have more chance to find some partition
in less time.

## Which evaluation function should be used ?

Given the data, `AB_Custom` gives the best scores, even though we does not consistently beat `AB_Improved`.

This is a good evaluation function due to the fact to be cheap to compute, so we avoid timeouts searching deepening on
game tree, though we always got a score above 67% in thw tree runs.