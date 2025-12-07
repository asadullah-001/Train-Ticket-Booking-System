#include <stdio.h>
#include <string.h>
#include <stdlib.h>

struct Passenger {
    char name[50];
    int age;
    char train[50];
    int trainNo;
    char date[15];
    int seat;
    int pnr;
};

struct Passenger tickets[100];
int total = 0;
int pnrStart = 1000;

void showMenu();
void bookTicket();
void showTickets();
void findTicket();
void deleteTicket();
void saveData();
void loadData();

int main() {
    int option;
    
    printf("************************************\n");
    printf("      TRAIN RESERVATION SYSTEM\n");
    printf("************************************\n");
    printf("    Made by: Oli, Yamin, Zoheb\n");
    printf("************************************\n\n");
    
    loadData();
    
    do {
        showMenu();
        printf("What you want to do? Enter number: ");
        scanf("%d", &option);
        
        if(option == 1) {
            bookTicket();
        }
        else if(option == 2) {
            showTickets();
        }
        else if(option == 3) {
            findTicket();
        }
        else if(option == 4) {
            deleteTicket();
        }
        else if(option == 5) {
            saveData();
            printf("Saved!\n");
        }
        else if(option == 6) {
            saveData();
            printf("Bye bye!\n");
        }
        else {
            printf("Wrong number! Try 1 to 6\n");
        }
        
        printf("\n");
        
    } while(option != 6);
    
    return 0;
}

void showMenu() {
    printf("\n");
    printf("------------ MENU -------------\n");
    printf("1. Book new ticket\n");
    printf("2. See all tickets\n");
    printf("3. Find ticket\n");
    printf("4. Cancel ticket\n");
    printf("5. Save\n");
    printf("6. Exit\n");
    printf("-------------------------------\n");
}

void bookTicket() {
    if(total >= 100) {
        printf("Sorry full!\n");
        return;
    }
    
    printf("\n--- BOOK TICKET ---\n");
    
    printf("Passenger name: ");
    getchar();
    fgets(tickets[total].name, 50, stdin);
    tickets[total].name[strlen(tickets[total].name)-1] = '\0';
    
    printf("Age: ");
    scanf("%d", &tickets[total].age);
    
    printf("Train name: ");
    getchar();
    fgets(tickets[total].train, 50, stdin);
    tickets[total].train[strlen(tickets[total].train)-1] = '\0';
    
    printf("Train number: ");
    scanf("%d", &tickets[total].trainNo);
    
    printf("Travel date (dd/mm/yyyy): ");
    getchar();
    fgets(tickets[total].date, 15, stdin);
    tickets[total].date[strlen(tickets[total].date)-1] = '\0';
    
    tickets[total].seat = total + 1;
    tickets[total].pnr = pnrStart;
    pnrStart++;
    
    printf("\nSUCCESS! Ticket booked!\n");
    printf("Your PNR: %d\n", tickets[total].pnr);
    printf("Your seat: %d\n", tickets[total].seat);
    
    total++;
}

void showTickets() {
    int i;
    
    if(total == 0) {
        printf("No tickets!\n");
        return;
    }
    
    printf("\n--- ALL TICKETS ---\n");
    printf("Total tickets booked: %d\n\n", total);
    
    for(i = 0; i < total; i++) {
        printf("Ticket %d:\n", i+1);
        printf("PNR: %d\n", tickets[i].pnr);
        printf("Name: %s\n", tickets[i].name);
        printf("Age: %d\n", tickets[i].age);
        printf("Train: %s\n", tickets[i].train);
        printf("Train No: %d\n", tickets[i].trainNo);
        printf("Date: %s\n", tickets[i].date);
        printf("Seat: %d\n", tickets[i].seat);
        printf("-------------------\n");
    }
}

void findTicket() {
    int searchPnr;
    int i;
    int found = 0;
    
    if(total == 0) {
        printf("No tickets to search!\n");
        return;
    }
    
    printf("Enter PNR to find: ");
    scanf("%d", &searchPnr);
    
    for(i = 0; i < total; i++) {
        if(tickets[i].pnr == searchPnr) {
            printf("\nFOUND TICKET!\n");
            printf("PNR: %d\n", tickets[i].pnr);
            printf("Name: %s\n", tickets[i].name);
            printf("Age: %d\n", tickets[i].age);
            printf("Train: %s\n", tickets[i].train);
            printf("Train No: %d\n", tickets[i].trainNo);
            printf("Date: %s\n", tickets[i].date);
            printf("Seat: %d\n", tickets[i].seat);
            found = 1;
            break;
        }
    }
    
    if(found == 0) {
        printf("PNR %d not found!\n", searchPnr);
    }
}

void deleteTicket() {
    int cancelPnr;
    int i, j;
    int found = 0;
    
    if(total == 0) {
        printf("No tickets to cancel!\n");
        return;
    }
    
    printf("Enter PNR to cancel: ");
    scanf("%d", &cancelPnr);
    
    for(i = 0; i < total; i++) {
        if(tickets[i].pnr == cancelPnr) {
            printf("Cancelling ticket of %s\n", tickets[i].name);
            
            for(j = i; j < total-1; j++) {
                tickets[j] = tickets[j+1];
            }
            
            total--;
            found = 1;
            printf("Ticket cancelled!\n");
            break;
        }
    }
    
    if(found == 0) {
        printf("PNR %d not found for cancellation!\n", cancelPnr);
    }
}

void saveData() {
    FILE *f;
    int i;
    
    f = fopen("tickets_data.bin", "wb");
    if(f == NULL) {
        printf("Cannot save file!\n");
        return;
    }
    
    fwrite(&total, sizeof(int), 1, f);
    fwrite(&pnrStart, sizeof(int), 1, f);
    
    for(i = 0; i < total; i++) {
        fwrite(&tickets[i], sizeof(struct Passenger), 1, f);
    }
    
    fclose(f);
}

void loadData() {
    FILE *f;
    int i;
    
    f = fopen("tickets_data.bin", "rb");
    if(f == NULL) {
        printf("Starting new...\n");
        return;
    }
    
    fread(&total, sizeof(int), 1, f);
    fread(&pnrStart, sizeof(int), 1, f);
    
    for(i = 0; i < total; i++) {
        fread(&tickets[i], sizeof(struct Passenger), 1, f);
    }
    
    fclose(f);
    printf("Loaded old data!\n");
}
