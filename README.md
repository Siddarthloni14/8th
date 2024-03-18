# 8thDevelop a menu driven Program in C for the following operations on Doubly Linked List
(DLL) of Employee Data with the fields: SSN, Name, Dept, Designation, Sal, PhNo
a. Create a DLL of N Employees Data by using end insertion.
b. Display the status of DLL and count the number of nodes in it
c. Perform Insertion and Deletion at End of DLL
d. Perform Insertion and Deletion at Front of DLL
e. Demonstrate how this DLL can be used as Double Ended Queue.
f. Exi

#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Structure to represent employee data
struct Employee {
    char SSN[20];
    char Name[50];
    char Dept[50];
    char Designation[50];
    float Sal;
    long long int PhNo;
    struct Employee *prev;
    struct Employee *next;
};

// Function prototypes
struct Employee* createNode();
void endInsert(struct Employee **head);
void displayList(struct Employee *head);
int countNodes(struct Employee *head);
void endInsert(struct Employee **head);
void frontInsert(struct Employee **head);
void endDelete(struct Employee **head);
void frontDelete(struct Employee **head);

int main() {
    struct Employee *head = NULL;
    char choice;

    do {
        printf("\nDoubly Linked List Operations Menu:\n");
        printf("a. Create a DLL of N Employees Data by using end insertion\n");
        printf("b. Display the status of DLL and count the number of nodes in it\n");
        printf("c. Perform Insertion at End of DLL\n");
        printf("d. Perform Insertion at Front of DLL\n");
        printf("e. Perform Deletion at End of DLL\n");
        printf("f. Perform Deletion at Front of DLL\n");
        printf("g. Demonstrate how this DLL can be used as Double Ended Queue\n");
        printf("h. Exit\n");
        printf("Enter your choice: ");
        scanf(" %c", &choice);

        switch (choice) {
            case 'a':
                endInsert(&head);
                break;

            case 'b':
                displayList(head);
                printf("Number of nodes: %d\n", countNodes(head));
                break;

            case 'c':
                endInsert(&head);
                break;

            case 'd':
                frontInsert(&head);
                break;

            case 'e':
                endDelete(&head);
                break;

            case 'f':
                frontDelete(&head);
                break;

            case 'g':
                printf("Demonstrating Double Ended Queue functionality...\n");
                endInsert(&head);
                frontInsert(&head);
                endDelete(&head);
                frontDelete(&head);
                break;

            case 'h':
                printf("Exiting program.\n");
                break;

            default:
                printf("Invalid choice! Please enter a valid option.\n");
        }
    } while (choice != 'h');

    // Free memory allocated for nodes before exiting
    struct Employee *temp;
    while (head != NULL) {
        temp = head;
        head = head->next;
        free(temp);
    }

    return 0;
}

// Function to create a new node
struct Employee* createNode() {
    struct Employee *newNode = (struct Employee*)malloc(sizeof(struct Employee));
    if (newNode == NULL) {
        printf("Memory allocation failed.\n");
        exit(1);
    }
    newNode->prev = NULL;
    newNode->next = NULL;
    return newNode;
}

// Function to insert a node at the end of the doubly linked list
void endInsert(struct Employee **head) {
    struct Employee *newNode = createNode();
    printf("Enter SSN: ");
    scanf("%s", newNode->SSN);
    printf("Enter Name: ");
    scanf(" %[^\n]", newNode->Name);
    printf("Enter Department: ");
    scanf(" %[^\n]", newNode->Dept);
    printf("Enter Designation: ");
    scanf(" %[^\n]", newNode->Designation);
    printf("Enter Salary: ");
    scanf("%f", &newNode->Sal);
    printf("Enter Phone Number: ");
    scanf("%lld", &newNode->PhNo);

    if (*head == NULL) {
        *head = newNode;
    } else {
        struct Employee *current = *head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newNode;
        newNode->prev = current;
    }

    printf("Employee data inserted at the end of the list.\n");
}

// Function to display the doubly linked list
void displayList(struct Employee *head) {
    if (head == NULL) {
        printf("Doubly Linked List is empty.\n");
        return;
    }

    struct Employee *current = head;
    printf("Doubly Linked List Status:\n");
    while (current != NULL) {
        printf("SSN: %s, Name: %s, Department: %s, Designation: %s, Salary: %.2f, Phone Number: %lld\n", current->SSN, current->Name, current->Dept, current->Designation, current->Sal, current->PhNo);
        current = current->next;
    }
}

// Function to count the number of nodes in the doubly linked list
int countNodes(struct Employee *head) {
    int count = 0;
    struct Employee *current = head;
    while (current != NULL) {
        count++;
        current = current->next;
    }
    return count;
}

// Function to insert a node at the front of the doubly linked list
void frontInsert(struct Employee **head) {
    struct Employee *newNode = createNode();
    printf("Enter SSN: ");
    scanf("%s", newNode->SSN);
    printf("Enter Name: ");
    scanf(" %[^\n]", newNode->Name);
    printf("Enter Department: ");
    scanf(" %[^\n]", newNode->Dept);
    printf("Enter Designation: ");
    scanf(" %[^\n]", newNode->Designation);
    printf("Enter Salary: ");
    scanf("%f", &newNode->Sal);
    printf("Enter Phone Number: ");
    scanf("%lld", &newNode->PhNo);

    if (*head == NULL) {
        *head = newNode;
    } else {
        newNode->next = *head;
        (*head)->prev = newNode;
        *head = newNode;
    }

    printf("Employee data inserted at the front of the list.\n");
}

// Function to delete a node from the end of the doubly linked list
void endDelete(struct Employee **head) {
    if (*head == NULL) {
        printf("Doubly Linked List is empty. Cannot delete.\n");
        return;
    }

    if ((*head)->next == NULL) {
        printf("Deleted employee data: SSN: %s, Name: %s, Department: %s, Designation: %s, Salary: %.2f, Phone Number: %lld\n", (*head)->SSN, (*head)->Name, (*head)->Dept, (*head)->Designation, (*head)->Sal, (*head)->PhNo);
        free(*head);
        *head = NULL;
        return;
    }

    struct Employee *current = *head;
    while (current->next != NULL
