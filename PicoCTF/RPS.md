# RPS

## CHALLENGE CATEGORY- BINARY EXPLOITATION

### CHALLENGE DESCRIPTION- 
Here's a program that plays rock, paper, scissors against you. I hear something good happens if you win 5 times in a row.
The program's source code with the flag redacted can be downloaded here.
Additional details will be available after launching your challenge instance.

### HINTS-
1)How does the program check if you won?

### Solution

I connected to the challenge using ```$ nc saturn.picoctf.net 63029``` and it connected to a program was a rock ,paper ,scissors game randomized where the way to 
get the flag was to beat the computer 5 times in a row.

![image](https://github.com/user-attachments/assets/882c8902-60ab-478f-9a04-43bd80b8abf0)



So naturally I tried playing it once but it was obvious that I wouldn't get the flag this way hence I moved my focus towards the source code of the game given.
The source code looked something like this-

```bash
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <string.h>
#include <time.h>
#include <unistd.h>
#include <sys/time.h>
#include <sys/types.h>


#define WAIT 60



static const char* flag = "[REDACTED]";

char* hands[3] = {"rock", "paper", "scissors"};
char* loses[3] = {"paper", "scissors", "rock"};
int wins = 0;



int tgetinput(char *input, unsigned int l)
{
    fd_set          input_set;
    struct timeval  timeout;
    int             ready_for_reading = 0;
    int             read_bytes = 0;
    
    if( l <= 0 )
    {
      printf("'l' for tgetinput must be greater than 0\n");
      return -2;
    }
    
    
    /* Empty the FD Set */
    FD_ZERO(&input_set );
    /* Listen to the input descriptor */
    FD_SET(STDIN_FILENO, &input_set);

    /* Waiting for some seconds */
    timeout.tv_sec = WAIT;    // WAIT seconds
    timeout.tv_usec = 0;    // 0 milliseconds

    /* Listening for input stream for any activity */
    ready_for_reading = select(1, &input_set, NULL, NULL, &timeout);
    /* Here, first parameter is number of FDs in the set, 
     * second is our FD set for reading,
     * third is the FD set in which any write activity needs to updated,
     * which is not required in this case. 
     * Fourth is timeout
     */

    if (ready_for_reading == -1) {
        /* Some error has occured in input */
        printf("Unable to read your input\n");
        return -1;
    } 

    if (ready_for_reading) {
        read_bytes = read(0, input, l-1);
        if(input[read_bytes-1]=='\n'){
        --read_bytes;
        input[read_bytes]='\0';
        }
        if(read_bytes==0){
            printf("No data given.\n");
            return -4;
        } else {
            return 0;
        }
    } else {
        printf("Timed out waiting for user input. Press Ctrl-C to disconnect\n");
        return -3;
    }

    return 0;
}


bool play () {
  char player_turn[100];
  srand(time(0));
  int r;

  printf("Please make your selection (rock/paper/scissors):\n");
  r = tgetinput(player_turn, 100);
  // Timeout on user input
  if(r == -3)
  {
    printf("Goodbye!\n");
    exit(0);
  }

  int computer_turn = rand() % 3;
  printf("You played: %s\n", player_turn);
  printf("The computer played: %s\n", hands[computer_turn]);

  if (strstr(player_turn, loses[computer_turn])) {
    puts("You win! Play again?");
    return true;
  } else {
    puts("Seems like you didn't win this time. Play again?");
    return false;
  }
}


int main () {
  char input[3] = {'\0'};
  int command;
  int r;

  puts("Welcome challenger to the game of Rock, Paper, Scissors");
  puts("For anyone that beats me 5 times in a row, I will offer up a flag I found");
  puts("Are you ready?");
  
  while (true) {
    puts("Type '1' to play a game");
    puts("Type '2' to exit the program");
    r = tgetinput(input, 3);
    // Timeout on user input
    if(r == -3)
    {
      printf("Goodbye!\n");
      exit(0);
    }
    
    if ((command = strtol(input, NULL, 10)) == 0) {
      puts("Please put in a valid number");
      
    } else if (command == 1) {
      printf("\n\n");
      if (play()) {
        wins++;
      } else {
        wins = 0;
      }

      if (wins >= 5) {
        puts("Congrats, here's the flag!");
        puts(flag);
      }
    } else if (command == 2) {
      return 0;
    } else {
      puts("Please type either 1 or 2");
    }
  }

  return 0;
}

```

On carefully reading through the lines and focusing on the hint , I moved to the part where the program decides his move, which was 

```bash
char* hands[3] = {"rock", "paper", "scissors"};
char* loses[3] = {"paper", "scissors", "rock"};
int wins = 0;

 int computer_turn = rand() % 3;
  printf("You played: %s\n", player_turn);
  printf("The computer played: %s\n", hands[computer_turn]);

  if (strstr(player_turn, loses[computer_turn])) {
    puts("You win! Play again?");
    return true;
  } else {
    puts("Seems like you didn't win this time. Play again?");
    return false;
  }

```
While analyzing the game's logic, I noticed something interesting. The program randomly selects one of the classic Rock-Paper-Scissors moves — "rock", "paper", or "scissors". It then uses a loses[] array to determine what defeats that move. For instance, if the computer picks "rock" (which is at index 0), loses[0] returns "paper", meaning the player would win if they respond with "paper".

Now, here’s where things get exploitable: instead of validating whether the player's move is an actual, valid RPS choice, the program simply checks if the player's input contains the string that beats the computer’s move. It does this using the C function strstr(player_input, loses[computer_move]).

So what happens if I input a string like "rockpaperscissors"? Well, no matter what the computer picks, the corresponding losing move (from the loses[] array) will always be found within my input. That means I win every time, regardless of the computer's choice.

In other words, by stuffing all three keywords into one string, I bypass the game’s logic completely. It doesn’t care if the move is valid—it just wants to find a winning substring.

This kind of oversight is a great example of how small logic bugs can lead to unintended behavior, especially in C-style string handling.


Hence i applied the same logic and boom it worked haha

![image](https://github.com/user-attachments/assets/e7454b01-8375-4fba-af6c-5aae2ab4c4e3)


Initially i thought that I had to change some code and make it print the flag on its own without the code but sometimes its much simpler and basic syntax logic 
like that 


Hence solved xd



