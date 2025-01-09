## C++ Project: Snake

- Implement a text based version of Snake that can be run on the command line.
- Snake spawns in the top left corner of the map.
- Snake is controlled by either the arrow keys or the 'W', 'A', 'S', 'D' keys.
- Snake starts with just a head (i.e. body length 0).
- Snake's body grows in length by 1 for each food it eats.
- Food is spawned when the game starts and when the snake eats.
- Food is spawned at a random empty cell on the map.
- Consumed food is tracked and displayed.
- Snake can move/wrap around the edges of the map.
- Game ends when snake runs into itself or food cannot be generated.
- Empty map cells are rendered as the '.' character.
- Snake head is rendered as the '0' (zero) character.
- Snake body is rendered as '@' (at) characters.
- Food is rendered as the '#' (pound) character.
- The map size should be 32x8, but also configurable via command line options.
    - Ex: `$ snake --height 32`.
    - Ex: `$ snake --width 8 --height 4`.

## Example Views

### Start of Game

```
Game State: New Game
Food Eaten: 0

0...............................
................................
................................
................................
....#...........................
................................
................................
................................

Press WASD or the arrow keys to move.
```

### Mid-Game: Middle of map

```
Game State: Playing
Food Eaten: 10

................................
.........................#......
................................
............@@@0................
............@...................
............@@@@@...............
................@...............
................................


```

### Mid-Game: Wrapped movement

```
Game State: Playing
Food Eaten: 5

................@...............
................@........#......
................0...............
................................
................................
................@...............
................@...............
................@...............


```

### Game Over

```
Game State: Game Over
Food Eaten: 12

................................
................................
..............@@0@@@............
................@..@............
................@@@@............
................................
...............................#
................................

Press any key to exit.
```

## Some Helpful Things

Below is some code that may be helpful, but not required to be used.

### Example CMakeLists.txt

```
cmake_minimum_required(VERSION 3.20)

project(snake)

set(HEADER_FILES
    "${PROJECT_SOURCE_DIR}/src/snake.h"
)

set(SOURCE_FILES
    "${PROJECT_SOURCE_DIR}/src/main.cpp"
    "${PROJECT_SOURCE_DIR}/src/snake.cpp"
)

add_executable(
    "${PROJECT_NAME}"
        "${HEADER_FILES}"
        "${SOURCE_FILES}"
)

target_include_directories(
    "${PROJECT_NAME}"
        PRIVATE
            "${HEADER_FILES}"
)

install(
    TARGETS
        "${PROJECT_NAME}"
    DESTINATION
        "bin"
)
```

### Getting a Millisecond Precision Timestamp

```
#include <chrono>

uint64_t millisecondsSinceEpoch()
{
    using std::chrono;

    auto timeSinceEpoch = system_clock::now().time_since_epoch();
    auto millisecondsSinceEpoch = duration_cast<milliseconds>(timeSinceEpoch);
    return millisecondsSinceEpoch.count();
}
```

### Clearing the Terminal Screen

```
void clearTerminalScreen()
{
#if defined _WIN32
    system("cls");
#elif defined __LINUX__ || defined __gnu_linux__ || defined __linux__
    system("clear");
#else
    std::cout << "Error: Unsupported OS."
#endif
}
```

### Keyboard Input

**Note:** This one may only work on Windows. Need to figure out how to do something similar on Linux.

```
#include <conio.h>

int const KEY_CODE_W = 119;
int const KEY_CODE_A = 97;
int const KEY_CODE_S = 115;
int const KEY_CODE_D = 100;
int const KEY_CODE_UP_ARROW = 72;
int const KEY_CODE_LEFT_ARROW = 75;
int const KEY_CODE_DOWN_ARROW = 80;
int const KEY_CODE_RIGHT_ARROW = 77;

void getPlayerInput(int & input)
{
    if(kbhit())
    {
        input = getch();
    }
}
```
