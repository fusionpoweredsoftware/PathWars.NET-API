PathWars.NET API
================

## Concept

`PathWars` is an idea based on the Tolman's classic [rat in the maze study](https://en.wikipedia.org/wiki/Latent_learning). Rather than studying the 
performance of rats, `PathWars` studies the performance of programs. More precisely, `PathWars` tests the effeciency of programs to maneuver mazes. 
`PathWars.NET` is an extension of that idea that makes `PathWars` testing accessible over a centralized network. 

## How it works

`PathWars.NET` is the concept, but `PathWars.NET API` is the brainchild that allows the programmer to practice the concept.

`PathWars.NET API` listens for basic query requests to control the state of the game. The `start` query will begin the game. When the game starts, 
the programmer's virtual `MOUSE` (not the type of mouse next to your keyboard, but mouse as in the tiny rodent) will be randomly placed into a labyrinth 
of connecting pathways. The `maze navigation` queries will move `MOUSE` in various directions and manners: 

- `moveForward`
- `moveBackward`
- `turnLeft`
- `turnRight`
- `turnAround`

The `forfeit` query will end a game abruptly. For each `start` and `maze navigation` query requested, the API will return 
encoded sensory data for `MOUSE`'s vision and smell. Moreover, the API will additionally return the `UUID`  of the game, the `cheese found count`, how 
many `seconds` the game has been running, the number of `mazes beaten`, and the  number of `mazes in total` that are required to beat the game. 

The `getOutputFormat` query is available to check the exact output format for the aforementioned data. Finally, the `getScore` query returns `MOUSE`'s 
score for a game identified by its `UUID` and the `getTopScores` query reveals the top 10 scores of all-time. For visual analysis, the `show` query 
will allow users to observe how a `MOUSE` moved during a completed game.

The `checkStatus` query has been added which responds with the same output as `maze navigation` queries, without changing the state of `MOUSE`.

## API Usage

`PathWars.NET API` takes `GET` URL requests as follows:

- Pre-initilization Query:

    - **api.pathwars.net/*getOutputStructure*?format=`FORMAT`**

        - *Input:* Takes an optional data `FORMAT` input, which can be `html` or `plain-text`.
        - *Output:* Provides the output format that is returned when executing `start` and `maze navigation` queries.

- Game Control/Status Queries:

    - **api.pathwars.net/*start*?username=`USERNAME`&order=`ORDER`**

        - *Input:* Takes an optional `USERNAME` input. Also takes an optional `ORDER` input, which can be used to ensure that requests are
        received in-order. For more information on ordering, see section titled
        [Checking Requests are Sent In-Order](#Checking-Requests-are-Sent-In-Order).
        - *Output:* Relays the `UUID`, and provides the number of cheeses collected for the current maze, vision and smell sensory
        data, the number of seconds that has elapsed since the game was started (always zero for this query), and the total number of
        mazes that have been completed. The value of `ORDER` is also relayed as output which can be used to identify which output is
        the response to which request.

    - **api.pathwars.net/*checkStatus*?uuid=`UUID`&order=`ORDER`**

        - *Input:* Takes a `UUID` for game identification, determined by the output of the start query. Also takes an optional `ORDER` input, 
        which can be used to ensure that requests are received in-order. For more information on ordering, see section titled
        [Checking Requests are Sent In-Order](#Checking-Requests-are-Sent-In-Order).
        - *Output:* Relays the `UUID`, and provides the number of cheeses collected for the current maze, vision and smell sensory 
        data, the number of seconds that has elapsed since the game was started, and the total number of mazes that have been completed.
        The value of `ORDER` is also relayed as output which can be used to identify which output is the response to which request.

    - **api.pathwars.net/*forfeit*?uuid=`UUID`**

        - *Input:* Takes a `UUID` for game identification, determined by the output of the start query.
        - *Output:* Relays the `UUID`, and provides the cheese found count, vision and smell sensory data, the number of seconds the game 
        has been running, the number of mazes that have been beaten, and the total number of mazes requried to beat the game. 

- Maze Navigation Queries:

    - **api.pathwars.net/*moveForward*?times=`TIMES`&uuid=`UUID`&order=`ORDER`**

        - *Input:* Takes the number of `TIMES` to move forward and a `UUID` for game identification, determined by the output of 
        the start query. Also takes an optional `ORDER` input, which can be used to ensure that requests are
        received in-order. For more information on ordering, see section titled
        [Checking Requests are Sent In-Order](#Checking-Requests-are-Sent-In-Order).
        - *Output:* Relays the `UUID`, and provides the number of cheeses collected for the current maze, vision and smell sensory 
        data, the number of seconds that has elapsed since the game was started, and the total number of mazes that have been completed.
        The value of `ORDER` is also relayed as output which can be used to identify which output is the response to which request.

    - **api.pathwars.net/*moveBackward*?times=`TIMES`&uuid=`UUID`&order=`ORDER`**

        - *Input:* Takes the number of `TIMES` to move backward and a `UUID` for game identification, determined by the output of 
        the start query. Also takes an optional `ORDER` input, which can be used to ensure that requests are
        received in-order. For more information on ordering, see section titled
        [Checking Requests are Sent In-Order](#Checking-Requests-are-Sent-In-Order).
        - *Output:* Relays the `UUID`, and provides the number of cheeses collected for the current maze, vision and smell sensory 
        data, the number of seconds that has elapsed since the game was started, and the total number of mazes that have been completed.
        The value of `ORDER` is also relayed as output which can be used to identify which output is the response to which request.

    - **api.pathwars.net/*turnLeft*?uuid=`UUID`&order=`ORDER`**

        - *Input:* Takes a `UUID` for game identification, determined by the output of the start query. Also takes an optional `ORDER` input, 
        which can be used to ensure that requests are received in-order. For more information on ordering, see section titled
        [Checking Requests are Sent In-Order](#Checking-Requests-are-Sent-In-Order).
        - *Output:* Relays the `UUID`, and provides the number of cheeses collected for the current maze, vision and smell sensory 
        data, the number of seconds that has elapsed since the game was started, and the total number of mazes that have been completed.
        The value of `ORDER` is also relayed as output which can be used to identify which output is the response to which request.

    - **api.pathwars.net/*turnRight*?uuid=`UUID`&order=`ORDER`**

        - *Input:* Takes a `UUID` for game identification, determined by the output of the start query. Also takes an optional `ORDER` input,
        which can be used to ensure that requests are received in-order. For more information on ordering, see section titled
        [Checking Requests are Sent In-Order](#Checking-Requests-are-Sent-In-Order).
        - *Output:* Relays the `UUID`, and provides the number of cheeses collected for the current maze, vision and smell sensory 
        data, the number of seconds that has elapsed since the game was started, and the total number of mazes that have been completed.
        The value of `ORDER` is also relayed as output which can be used to identify which output is the response to which request.

    - **api.pathwars.net/*turnAround*?uuid=`UUID`&order=`ORDER`**

        - *Input:* Takes a `UUID` for game identification, determined by the output of the start query. Also takes an optional `ORDER` input,
        which can be used to ensure that requests are received in-order. For more information on ordering, see section titled
        [Checking Requests are Sent In-Order](#Checking-Requests-are-Sent-In-Order).
        - *Output:* Relays the `UUID`, and provides the number of cheeses collected for the current maze, vision and smell sensory 
        data, the number of seconds that has elapsed since the game was started, and the total number of mazes that have been completed.
        The value of `ORDER` is also relayed as output which can be used to identify which output is the response to which request.

- Performance Checking Queries:

    - **api.pathwars.net/*show*?maze=`MAZE`&uuid=`UUID`&format=**

        - *Input:* Takes a `UUID`, determined by the output of the start query, and a `MAZE` index, which lets the programmer
        specify which maze to view. Also takes optional data `FORMAT` input, which can be `html` or `plain-text`.
        - *Output:* By default, the maze is shown in `plain-text` format.

    - **api.pathwars.net/*getScore*?uuid=`UUID`**

        - *Input:* Takes a `UUID` for game identification, determined by the output of the start query.
        - *Output:* Shows resulting game scores for a specified game identified by the `UUID`.

    - **api.pathwars.net/*getTopScores*?**

        - *Input:* Takes optional data `FORMAT` input, which can be `html` or `plain-text`.
        - *Output:* Shows top 10 scores recorded to-date for all games, listed by `UUID` and `USERNAME`.

It should be noted that `api.pathwars.net` is the official public PathWars server. For your own private testing, you will need to replace the
prefix `api.pathswars.net` in each URL request above with the IP/hostname of the private server (e.g. `localhost`/`127.0.0.1`) where
your copy of PathWars.NET API is being hosted.

## Rules & Objectives

Queries are rate-limited to one query per second. The API will consider this time delay as well as the difficulty level 
of each maze as its played in order to determine each program's game scores. Scores are assigned by session ID, which is provided
at the `start` of each game. The objective is to collect all cheese in each maze. The number of completed mazes is provided
in the response of each navigation query, so you will know once your `MOUSE` has progressed to the next maze. Cheese is 
collected when `MOUSE` has successfully navigated to the position of the cheese. The game ends when `MOUSE` has collected 
all of the cheese in every maze. No additional queries are necessary for your `MOUSE` to complete the game.

## Handling Smell and Vision Sensory Input

Smell and vision sensory data are represented as an integer. Smell is straight-forward: its integer represents the magnitude of
how much cheese `MOUSE` can smell. Vision is slightly more complex: its integer represents two binary sequences that correspond to the left and right
sides of what `MOUSE` is seeing. The first binary bit is ignored. Here's a visual example of the bit structure as it corresponds to what is being seen 
for a vision data of `341`:

![101010101 (341 in binary) means 2 exits left and right](https://static.wixstatic.com/media/f41d49_f0c8f4a41b4643f784889b3b6935d93d~mv2.pn)

First we convert `341` to binary: `(101010101)₂`. Next, the first bit (`1`) is tossed, and the remaining bits `(01010101)₂` are split into two halves: 
`(0101)₂` for the left and `(0101)₂` for the right. `0` signifies a wall, whereas `1` signifies an entry way.

## Scoring

Scoring is initially calculated by taking the square size (height times width) of the maze, multiplying it times the number of mazes played, subtracting 
the time taken to win (in seconds) from the result, and then adding the number of cheese found. This means that the higher the score, the better the 
performance  of `MOUSE` to collect cheese effeciently. The formula for the calculating the initial score looks like this: 

`initialScore` = (`width` x `height` x `mazeCount`) - `secondsToWin` + `cheeseFound`

The main advantage to this scoring approach is its simplicity. However, a major downside to this approach is that it does not account for the difficulty 
of the maze and cannot be a "fair" method scoring. To address this problem, scores are weighted by `difficulty level`, determined by the least number of 
moves taken to solve all of the mazes. So for example, if you played a game with ten `100` x `100` mazes, but a minimum of two thousand moves were 
required to collect the cheese in all ten mazes, then your `end score` will be scaled to `2000` ÷ (`10` x `100` x `100`) or 2% of your `initial score`. 
The formula for calculating the final score looks like this:

`finalScore` = (`intialScore` x `minimumMovesToCollectAllCheese`) ÷ (`width` x `height` x `mazeCount`)

NOTE: Presently, the size of the board is fixed at `100` x `100`.

## Checking Requests are Sent In-Order

The movement of `MOUSE` is heavily dependent on the order in which requests are sent to the API, so checking that requests are sent in-order is a 
necessary step to ensure correct movement. Although TCP already does this check, TCP is limited to checking the order of requests per connection. 
Since TCP connections may be interrupted for any number of reasons, TCP alone is insufficient to ensure requests are received in-order. For this reason,
the `ORDER` parameter has been introduced to the API. Here's how it works:

The API will check a request for an optional `ORDER` input. If an `ORDER` input is provided in the request, the API will require that said `ORDER`
is equal to `1` PLUS the previous `ORDER` input as it relates to the provided `UUID` input. This conditional requirement is true with one exception: if 
the value of `ORDER` is negative OR a request has not yet been sent which contains the initial value of `ORDER` per `UUID` provided, then the API will 
not require the `ORDER` to be any particular value. 

If the request does not meet the aforementioned requirement, then the API will return an error: `Bad order value received.` followed by the expected
`ORDER`.

## License

Currently the API uses the `DW-BBK` license, which has only one clause: `Do Whatever, But Be Kind`. This is a derivative of a slightly more 
vulgar license `JBK-FFS!`, which also has one clause: `Just Be Kind, For F*** Sake!`. It is important to note that this license is in no way
affiliated with the `WTFPL` license which fails to take into account the fact that people should at least make some effort to `be kind`. For 
clarity, stealing someone's code is not kind. That said, feel free to use the code but do not claim it as your own.

## Official Website for PathWars.NET

https://pathwars.net

## An Open-Source Project Created by AI Innovators of Huntsville

https://pathwars.net/aiihsv

