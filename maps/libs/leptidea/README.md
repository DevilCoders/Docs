LEPTIDEA - LEveled Partitioned TIme DEpendent Algorithm
More information on http://wiki.yandex-team.ru/JandeksKarty/development/fordevelopers/routing/TD

The new experimental alternatives algorithm has the following list of tunable parameters:

1. `rewardOffset`

    Plays the role of default reward for unexplored actions. Any real number from 0 to 1 (is not advisable to change).
2. `discountFactor`

    Gamma in Q-learning like algorithms. Any number from 0 to 1 (is not advisable to change).
3. `learningRate`

    Alpha_0 in Q-learning like algorithms. Controls the rate of changes in Q-values. Any positive number (is not advisable to change).
4. `lambda`

    Lambda in SARSA(lambda) algorithm. Makes the alternatives to be more optimal in aggregate. Any number from 0 to 1 (is not advisable to change).
5. `exponentiationShift`

    The greater this parameter is the more the weights of actions differ from each other. Makes the algorithm more prone to exploitation. Any real number.
6. `maxLengthRatio`

    The algorithm doesn't return alternatives that are more than `maxLengthRatio` times longer than the optimal route. Any number greater than 1.
7. `shortcutUnpackingThreshold`

    The algorithm excludes only those shortcuts that are shorter than `shortcutUnpackingThreshold * optimal-route-length`, unpacking longer shortcuts if necessary. The lower this value the lesser the difference between alternatives. Any number from 0 to 1.
8. `branchingFactor`

    The maximal number of attempts to exclude a distinct set of shortcuts from a single parent alternative to produce child alternatives. The higher this value the lesser the difference between alternatives.
9. `experimentalShortcutExclusionType`

    Changes the initial behavior of the algorithm to produce more distinct alternatives for longer routes.

    If set to `EntireComponent`, several first steps of the algorithm will produce alternatives by excluding entire leptidea components from the optimal route.

    If set to `SameEndpoints`, several first steps of the algorithm will produce alternatives by excluding pairs of edges from the optimal route.
10. `prioritizeShortcutsAtStart`

    If set to true, prioritizes shortcuts exclusion at the beginning of the route.
