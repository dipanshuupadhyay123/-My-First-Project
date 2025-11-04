# Linked List Operation
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *next;
};

struct node *start = NULL;

// Insert at beginning
void insert_beg() {
    int item;
    struct node *ptr = (struct node *)malloc(sizeof(struct node));
    if (ptr == NULL) {
        printf("Memory overflow\n");
        return;
    }
    printf("Enter value to insert at beginning: ");
    scanf("%d", &item);
    ptr->data = item;
    ptr->next = start;
    start = ptr;
    printf("Node inserted at beginning\n");
}

// Insert at random position
void insert_random() {
    int i, item, loc;
    struct node *ptr, *temp;
    ptr = (struct node *)malloc(sizeof(struct node));
    if (ptr == NULL) {
        printf("Overflow\n");
        return;
    }
    printf("Enter element to add: ");
    scanf("%d", &item);
    ptr->data = item;
    printf("Enter location after which to insert: ");
    scanf("%d", &loc);

    temp = start;
    for (i = 0; i < loc; i++) {
        if (temp == NULL) {
            printf("Position not found\n");
            free(ptr);
            return;
        }
        temp = temp->next;
    }
    ptr->next = temp->next;
    temp->next = ptr;
    printf("Node inserted\n");
}

// Insert at end
void insert_last() {
    struct node *ptr, *temp;
    int item;
    ptr = (struct node *)malloc(sizeof(struct node));
    if (ptr == NULL) {
        printf("Overflow\n");
        return;
    }
    printf("Enter a value: ");
    scanf("%d", &item);
    ptr->data = item;
    ptr->next = NULL;

    if (start == NULL) {
        start = ptr;
    } else {
        temp = start;
        while (temp->next != NULL)
            temp = temp->next;
        temp->next = ptr;
    }
    printf("Node inserted at end\n");
}

// Delete beginning
void delete_begining() {
    struct node *ptr;
    if (start == NULL) {
        printf("List is empty\n");
        return;
    }
    ptr = start;
    start = start->next;
    free(ptr);
    printf("Node deleted from beginning\n");
}

// Delete last
void delete_last() {
    struct node *ptr, *ptr1;
    if (start == NULL) {
        printf("List is empty\n");
        return;
    } else if (start->next == NULL) {
        ptr = start;
        start = NULL;
        free(ptr);
        printf("Only node deleted\n");
    } else {
        ptr = start;
        while (ptr->next != NULL) {
            ptr1 = ptr;
            ptr = ptr->next;
        }
        ptr1->next = NULL;
        free(ptr);
        printf("Last node deleted\n");
    }
}

// Delete at random position
void delete_random() {
    struct node *ptr, *ptr1;
    int loc, i;
    printf("Enter position of node to delete: ");
    scanf("%d", &loc);

    if (start == NULL) {
        printf("List is empty\n");
        return;
    }

    ptr = start;
    if (loc == 0) {
        start = ptr->next;
        free(ptr);
        printf("Deleted node at position 0\n");
        return;
    }

    for (i = 0; i < loc; i++) {
        ptr1 = ptr;
        ptr = ptr->next;
        if (ptr == NULL) {
            printf("Position not found\n");
            return;
        }
    }
    ptr1->next = ptr->next;
    free(ptr);
    printf("Deleted node at position %d\n", loc);
}

// Search
void search() {
    struct node *ptr = start;
    int item, pos = 0, found = 0;

    if (ptr == NULL) {
        printf("List is empty\n");
        return;
    }
    printf("Enter value to search: ");
    scanf("%d", &item);

    while (ptr != NULL) {
        if (ptr->data == item) {
            printf("Element %d found at position %d\n", item, pos);
            found = 1;
            break;
        }
        ptr = ptr->next;
        pos++;
    }
    if (!found){
        printf("Element not found\n");
    }
}

// Display
void display() {
    struct node *temp = start;
    if (temp == NULL) {
        printf("List is empty\n");
        return;
    }
    printf("Linked list: ");
    while (temp != NULL) {
        printf("%d -> ", temp->data);
        temp = temp->next;
    }
    printf("NULL\n");
}

int main() {
    int choice;
    while (1) {
        printf("\n--- LINKED LIST MENU ---\n");
        printf("1. Insert at beginning\n");
        printf("2. Insert at random position\n");
        printf("3. Insert at end\n");
        printf("4. Delete at beginning\n");
        printf("5. Delete at random position\n");
        printf("6. Delete at end\n");
        printf("7. Display\n");
        printf("8. Search\n");
        printf("9. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1: insert_beg(); break;
            case 2: insert_random(); break;
            case 3: insert_last(); break;
            case 4: delete_begining(); break;
            case 5: delete_random(); break;
            case 6: delete_last(); break;
            case 7: display(); break;
            case 8: search(); break;
            case 9: exit(0);
            default: printf("Invalid choice!\n");
        }
    }
    return 0;
}

