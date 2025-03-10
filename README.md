#include <stdio.h>
#include <stdlib.h>

struct Node {
    int number;
    int password;
    struct Node *next;
};

struct Node* createCircularLinkedList(int n, int passwords[]) {
    struct Node *head = NULL;
    struct Node *prev = NULL;
    for (int i = 0; i < n; i++) {
        struct Node *newNode = (struct Node*)malloc(sizeof(struct Node));
        newNode->number = i + 1;
        newNode->password = passwords[i];
        if (head == NULL) {
            head = newNode;
        } else {
            prev->next = newNode;
        }
        prev = newNode;
    }
    if (prev != NULL) {
        prev->next = head; 
    }
    return prev; 
}

void josephus(struct Node **current, int m, int n) {
    int remaining = n;
    while (remaining > 0) {
        int step = m % remaining;
        if (step == 0) {
            step = remaining;
        }
        
        for (int i = 0; i < step - 1; i++) {
            *current = (*current)->next;
        }
      
        struct Node *toDelete = (*current)->next;
        printf("%d ", toDelete->number);
        m = toDelete->password; 
        (*current)->next = toDelete->next;  
        free(toDelete);
        remaining--;
    }
}

int main() {
    int m_initial, n;
    printf("请输入初始报数上限值m: ");
    scanf("%d", &m_initial);
    printf("请输入人数n: ");
    scanf("%d", &n);
    int passwords[30];
    printf("请输入%d个人的密码: ", n);
    for (int i = 0; i < n; i++) {
        scanf("%d", &passwords[i]);
    }
    struct Node *current = createCircularLinkedList(n, passwords);
    josephus(&current, m_initial, n);
    printf("\n");
    return 0;
}# -
