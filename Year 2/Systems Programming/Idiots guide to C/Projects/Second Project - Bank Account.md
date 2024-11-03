This was more as an attempt to work with data manipulation and how it would work keeping globals in the main which I will edit in the helper functions:

- See current Balance.
- Make a Withdrawal.
- Make a Deposit.

In this app, the user will be asked to enter the name and promoted to select an action, from this we then run the required action.

```c
#include <stdio.h>

#define NAME_SIZE 40

void show_balance(const char name[], int balance);
void withdraw(const char name[], int *balance);
void deposit(const char name[], int *balance);

int main() {
    int balance = 0;
    char name[NAME_SIZE];
    int choice;

    printf("\n\nPlease enter your name:\n");
    scanf("%39s", name); // Limit of 39 to prevent overflow

    printf("\n\nWelcome to your Bank Account, %s!\n", name);

    while (1) {
        printf("\nEnter the respective number to perform an action\n\n");
        printf("[1] See current Balance.\n");
        printf("[2] Make a Withdrawal.\n");
        printf("[3] Make a Deposit.\n");
        printf("[4] Exit.\n");
        scanf("%i", &choice);

        switch (choice) {
            case 1:
                show_balance(name, balance);
                break;
            case 2:
                withdraw(name, &balance);
                break;
            case 3:
                deposit(name, &balance);
                break;
            case 4:
                printf("\nThank you for using our banking service. Goodbye, %s!\n", name);
                return 0;
            default:
                printf("Please enter a valid action (1-4).\n");
                break;
        }
    }

    return 0;
}

void show_balance(const char name[], int balance) {
    printf("\n%s, your current balance is: %i\n\n", name, balance);
}

void withdraw(const char name[], int *balance) {
    int withdrawal_amount;

    printf("\n%s, your current balance is: %i\n", name, *balance);
    printf("How much would you like to withdraw?\n");
    scanf("%i", &withdrawal_amount);

    if (withdrawal_amount > *balance) {
        printf("\nInsufficient funds for this withdrawal.\n\n");
    } else {
        *balance -= withdrawal_amount;
        printf("\nWithdrawal successful. New balance: %i\n\n", *balance);
    }
}

void deposit(const char name[], int *balance) {
    int deposit_amount;

    printf("\n%s, your current balance is: %i\n", name, *balance);
    printf("How much would you like to deposit?\n");
    scanf("%i", &deposit_amount);

    *balance += deposit_amount;
    printf("\nDeposit successful. New balance: %i\n\n", *balance);
}

```
