# cookies
#include <stdio.h>
#include <stdlib.h>
int count = 0;
struct node
{
    int sweetness;
    struct node *next;
};

struct node *head = NULL;
struct node *temp, *temp2;

void insert(int s)
{
    if (head == NULL)
    {
        struct node *newnode = malloc(sizeof(struct node));
        head = newnode;
        newnode->sweetness = s;
        newnode->next = NULL;
    }
    else
    {
        struct node *newnode = malloc(sizeof(struct node));
        newnode->sweetness = s;
        newnode->next = head;
        head = newnode;
    }
}

void sort(struct node **h)
{
    int i, j, a;

    struct node *temp1;
    struct node *temp2;

    for (temp1 = *h; temp1 != NULL; temp1 = temp1->next)
    {
        for (temp2 = temp1->next; temp2 != NULL; temp2 = temp2->next)
        {
            if (temp2->sweetness < temp1->sweetness)
            {
                a = temp1->sweetness;
                temp1->sweetness = temp2->sweetness;
                temp2->sweetness = a;
            }
        }
    }
}

void del()
{
    if (head == NULL)
        return;

    temp = head;
    head = head->next;
    free(temp);
}

void display()
{
    temp = head;
    while (temp != NULL)
    {
        printf("%d ", temp->sweetness);
        temp = temp->next;
    }
}

void operation(int k)
{
    int s;
    temp = head;

    if (temp->sweetness < k)
    {
        s = temp->sweetness + (2 * temp->next->sweetness);
        count++;
        del();
        del();
        insert(s);
        sort(&head);
        operation(k);
    }
    else
    {
        return;
    }
}

int main()
{
    int n, m, k;
    printf("Enter minimum sweetness: ");
    scanf("%d", &k);
    printf("Enter no of cookies: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++)
    {
        printf("Enter the sweetness of cookie %d: ", i + 1);
        scanf("%d", &m);
        insert(m);
    }

    printf("List of cookie sweetness: ");
    display();
    sort(&head);
    printf("\n");
    operation(k);

    printf("List of cookie sweetness after operation : ");
    display();

    printf("\nTotal no of operations performed: %d", count);

    return 0;
}

