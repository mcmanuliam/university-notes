- <https://www.geeksforgeeks.org/rock-paper-scissor-in-c/>

A simple first choice, it's a really easy game which will take input and compare with a random value generated with rand.

- Rock vs Paper -> Paper wins.
- Rock vs Scissor -> Rock wins.
- Paper vs Scissor -> Scissor wins.

In this game, the user will be asked to make choice and according to the choice of user and computer and then the result will be displayed along with the choices of both computer and user.

```c
#include <math.h>
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <stdbool.h>

int game(char you, char computer) {
    if (you == computer) {
        return -1;
    }
		
    bool win = 
	    ((you == 'S' && computer == 'P') 
	    || (you == 'P' && computer == 'R') 
	    || (you == 'R' && computer == 'S'));
		
    return win ? 1 : 0;
};

int main() {
	char player, computer;
    int result;

    srand(time(NULL));
    
    int randVal = rand() % 3;
    computer = (randVal == 0) ? 'R' : (randVal == 1) ? 'P' : 'S';
    
    printf("\nEnter R for ROCK, P for PAPER, and S for SCISSORS:\n");
    scanf(" %c", &player);
    
    result = game(player, computer);
    
    if (result == -1) {
        printf("\nGame Draw!\n");
    } else if (result == 1) {
        printf("\nWow! You have won the game!\n\n");
    } else {
        printf("\nOh! You have lost the game!\n\n");
    }
    
    printf("You chose: %c\n", player);
    printf("Computer chose: %c\n\n", computer);
    return 0;
}
```