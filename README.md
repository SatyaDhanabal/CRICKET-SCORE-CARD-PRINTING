# CRICKET-SCORE-CARD-PRINTING
#include <stdio.h>
#include <stdlib.h>
#include <time.h>
#include <string.h>

struct Player {
    char name[50];
    int runs_scored;
    int balls_faced;
    int wickets_taken;
    int num_6s;
    int num_4s;
    int num_1s;
    int num_2s;
    int num_3s;
    int num_5s;
    float strike_rate;
};

int main() {
    srand(time(NULL));

    int tossResult = rand() % 2; // Generate a random number (0 or 1)
    char teamA[50];
    char teamB[50];
    struct Player playerA[11];
    struct Player playerB[11];

    // Initialize player data
    char* playerA_names[] = {
        "MSD", "Sachin", "Yuvaraj", "Rohith", "Kapil ",
        "Sam", "Hardik", "Raina", "Bumrah", "Jadeja", "Yadav"
    };
    char* playerB_names[] = {
        "Jadhav", "Virat", "Rahul", "Murali", "Randiv",
        "Bailey", "Bravo", "Hussey", "Robin", "David", "Varun"
    };

    for (int i = 0; i < 11; i++) {
        strcpy(playerA[i].name, playerA_names[i]);
        playerA[i].runs_scored = 0;
        playerA[i].balls_faced = 0;
        playerA[i].wickets_taken = 0;
        playerA[i].num_6s = 0;
        playerA[i].num_4s = 0;
        playerA[i].num_1s = 0;
        playerA[i].num_2s = 0;
        playerA[i].num_3s = 0;
        playerA[i].num_5s = 0;
        playerA[i].strike_rate = 0;

        strcpy(playerB[i].name, playerB_names[i]);
        playerB[i].runs_scored = 0;
        playerB[i].balls_faced = 0;
        playerB[i].wickets_taken = 0;
        playerB[i].num_6s = 0;
        playerB[i].num_4s = 0;
        playerB[i].num_1s = 0;
        playerB[i].num_2s = 0;
        playerB[i].num_3s = 0;
        playerB[i].num_5s = 0;
        playerB[i].strike_rate = 0;
    }

    printf("Enter the name of Team A: ");
    scanf("%s", teamA);

    printf("Enter the name of Team B: ");
    scanf("%s", teamB);

    printf("Tossing the coin...\n");

    if (tossResult == 0) {
        printf("Heads. %s wins the toss!\n", teamA);
    } else {
        printf("Tails. %s wins the toss!\n", teamB);
    }

    char choice;
    printf("What would you like to do? Enter 'B' for batting or 'F' for fielding: ");
    scanf(" %c", &choice);

    printf("\n%s Players:\n", teamA);
    for (int i = 0; i < 11; i++) {
        printf("Player %d: %s\n", i + 1, playerA[i].name);
    }

    printf("\n%s Players:\n", teamB);
    for (int i = 0; i < 11; i++) {
        printf("Player %d: %s\n", i + 1, playerB[i].name);
    }

    // Perform scoring and wickets tracking for Team A
    for (int over = 0; over < 50; over++) {
        for (int ball = 0; ball < 6; ball++) {
            // Simulate a random score for Team A (4, 6, 1, 2, 3, 5)
            int score = rand() % 6;
            int player_index = rand() % 11;

            // Update player statistics for Team A
            playerA[player_index].balls_faced++;
            playerA[player_index].runs_scored += score;

            if (score == 6) {
                playerA[player_index].num_6s++;
            } else if (score == 4) {
                playerA[player_index].num_4s++;
            } else if (score == 1) {
                playerA[player_index].num_1s++;
            } else if (score == 2) {
                playerA[player_index].num_2s++;
            } else if (score == 3) {
                playerA[player_index].num_3s++;
            } else if (score == 5) {
                playerA[player_index].num_5s++;
            }
        }
    }

    // Perform scoring and wickets tracking for Team B
    for (int over = 0; over < 50; over++) {
        for (int ball = 0; ball < 6; ball++) {
            // Simulate a random score for Team B (4, 6, 1, 2, 3, 5)
            int score = rand() % 6;
            int player_index = rand() % 11;

            // Update player statistics for Team B
            playerB[player_index].balls_faced++;
            playerB[player_index].runs_scored += score;

            if (score == 6) {
                playerB[player_index].num_6s++;
            } else if (score == 4) {
                playerB[player_index].num_4s++;
            } else if (score == 1) {
                playerB[player_index].num_1s++;
            } else if (score == 2) {
                playerB[player_index].num_2s++;
            } else if (score == 3) {
                playerB[player_index].num_3s++;
            } else if (score == 5) {
                playerB[player_index].num_5s++;
            }
        }
    }

    // Simulate wickets taken for Team A and Team B
    for (int wicket = 0; wicket < 10; wicket++) {
        int player_index_A = rand() % 11;
        int player_index_B = rand() % 11;
        playerA[player_index_A].wickets_taken++;
        playerB[player_index_B].wickets_taken++;
    }

    // Calculate strike rates for both teams
    for (int i = 0; i < 11; i++) {
        if (playerA[i].balls_faced > 0) {
            playerA[i].strike_rate = (float)playerA[i].runs_scored / playerA[i].balls_faced * 100;
        }
        if (playerB[i].balls_faced > 0) {
            playerB[i].strike_rate = (float)playerB[i].runs_scored / playerB[i].balls_faced * 100;
        }
    }

    // Calculate the total score for both teams
    int total_score_A = 0;
    int total_score_B = 0;
    for (int i = 0; i < 11; i++) {
        total_score_A += playerA[i].runs_scored;
        total_score_B += playerB[i].runs_scored;
    }

    // Get the name of the winning team
    char* winning_team;
    if (total_score_A > total_score_B) {
        winning_team = teamA;
    } else if (total_score_B > total_score_A) {
        winning_team = teamB;
    } else {
        winning_team = "It's a tie!";
    }

    // Print the scorecard with strike rates
    printf("\n\t\t\t\t\t\tSCORECARD\n");

    printf("%s Players:\n", teamA);
    for (int i = 0; i < 11; i++) {
        printf("Player: %s\tRuns: %d\tBalls Faced: %d\t6s: %d\t4s: %d\t1s: %d\t2s: %d\t3s: %d\t5s: %d\tStrike Rate: %.2f\n",
               playerA[i].name, playerA[i].runs_scored, playerA[i].balls_faced,
               playerA[i].num_6s, playerA[i].num_4s, playerA[i].num_1s,
               playerA[i].num_2s, playerA[i].num_3s, playerA[i].num_5s,
               playerA[i].strike_rate);
    }

int i;
    printf("\n%s Players:\n", teamB);
    for (int i = 0; i < 11; i++) {
        printf("Player: %s\tRuns: %d  Balls Faced: %d\t6s: %d\t4s: %d\t1s: %d\t2s: %d\t3s: %d\t5s: %d\tStrike Rate: %.2f\n",
               playerB[i].name, playerB[i].runs_scored, playerB[i].balls_faced,
               playerB[i].num_6s, playerB[i].num_4s, playerB[i].num_1s,
               playerB[i].num_2s, playerB[i].num_3s, playerB[i].num_5s,
               playerB[i].strike_rate);
    }

    // Print the winning team
    printf("\t\t\t\t\tThe winning team is: %s\n", winning_team);
    printf("\t\t\t\t\tCONGRATULATIONS!!!");
    printf("\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a\a");

    // Allow the user to enter a player's name to display their details
    char player_name[50];
    printf("\nEnter a player's name to display their details: ");
    scanf("%s", player_name);

    // Search for the player and display their details
    for (int i = 0; i < 11; i++) {
        if (strcmp(player_name, playerA[i].name) == 0) {
            printf("\n%s's Details:\n", playerA[i].name);
            printf("Runs: %d\tBalls Faced: %d\t6s: %d\t4s: %d\t1s: %d\t2s: %d\t3s: %d\t5s: %d\tStrike Rate: %.2f\n",
                   playerA[i].runs_scored, playerA[i].balls_faced,
                   playerA[i].num_6s, playerA[i].num_4s, playerA[i].num_1s,
                   playerA[i].num_2s, playerA[i].num_3s, playerA[i].num_5s,
                   playerA[i].strike_rate);
            break;
        } else if (strcmp(player_name, playerB[i].name) == 0) {
            printf("\n%s's Details:\n", playerB[i].name);
            printf("Runs: %d\tBalls Faced: %d\t6s: %d\t4s: %d\t1s: %d\t2s: %d\t3s: %d\t5s: %d\tStrike Rate: %.2f\n",
                   playerB[i].runs_scored, playerB[i].balls_faced,
                   playerB[i].num_6s, playerB[i].num_4s, playerB[i].num_1s,
                   playerB[i].num_2s, playerB[i].num_3s, playerB[i].num_5s,
                   playerB[i].strike_rate);
            break;
        }
    }
    int max=0,max1=0;
    for(int i=0;i<11;i++)    
    {
        if(playerA[i].strike_rate>max){
        max=playerA[i].strike_rate;
        }
    }
        printf("%s has got maximum score of %d and obtains purple cap from team %s\n",playerA[i].name,max,teamA);
    for(int i=0;i<11;i++)
    {
        if(playerB[i].strike_rate>max1){
        max1=playerB[i].strike_rate;
        }
    }
        printf("%s has got maximum score of %d and obtains orange cap from team %s\n",playerB[i].name,max1,teamB);
    return 0;
}




