# PIE TIME

## CATEGORY - BINARY EXPLOITATION

### CHALLENGE DESCRIPTION - 
Can you try to get the flag? Beware we have PIE!
Additional details will be available after launching your challenge instance.

### HINT

1)Can you figure out what changed between the address you found locally and in the server output?

### Solution

After connecting to the challenge through the given `nc` command I got a program which looked something like this-
```bash
Address of main: 0x60c380a9f33d
Enter the address to jump to, ex => 0x12345: 0x289424eds
Your input: 289424ed
Segfault Occurred, incorrect address.
```

Naturally I tried to enter a random address and got the above mentioned output, hence it became pretty clear that I need to know the correct address too get the flag , but as I went through the program, the function
"win()" which was responsible for printing the flag was not being called anywhere in the main function

```bash

#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

void segfault_handler() {
  printf("Segfault Occurred, incorrect address.\n");
  exit(0);
}

int win() {
  FILE *fptr;
  char c;

  printf("You won!\n");
  // Open file
  fptr = fopen("flag.txt", "r");
  if (fptr == NULL)
  {
      printf("Cannot open file.\n");
      exit(0);
  }

  // Read contents from file
  c = fgetc(fptr);
  while (c != EOF)
  {
      printf ("%c", c);
      c = fgetc(fptr);
  }

  printf("\n");
  fclose(fptr);
}

int main() {
  signal(SIGSEGV, segfault_handler);
  setvbuf(stdout, NULL, _IONBF, 0); // _IONBF = Unbuffered

  printf("Address of main: %p\n", &main);

  unsigned long val;
  printf("Enter the address to jump to, ex => 0x12345: ");
  scanf("%lx", &val);
  printf("Your input: %lx\n", val);

  void (*foo)(void) = (void (*)())val;
  foo();
}

```

we can see the program takes the input from the user and uses it as the address but we don't know the address of it in binary to execute win()



