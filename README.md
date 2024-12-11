# DS1-6th-prgms
1)Develop a Program in C for the following: 
a) Declare a calendar as an array of 7 elements (A dynamically Created array) 
to represent 7 days of a week. Each Element of the array is a structure 
having three fields. The first field is the name of the Day (A dynamically 
allocated String), The second field is the date of the Day (A integer), the 
third field is the description of the activity for a particular day (A 
dynamically allocated String). 
b) Write functions create(), read() and display(); to create the calendar, to 
read the data from the keyboard and to print weeks activity details report on 
screen.
ans->#include <stdio.h>
struct calendar
{
char *dayName;
int date;
char *description;
}week[7];
void create()
{
int i;
for (i = 0; i < 7; i++)
{
week[i].dayName = (char *) malloc(20 * sizeof(char));
week[i].description = (char *) malloc(50 * sizeof(char));
}
}
void read()
{
int i;
for (i = 0; i < 7; i++)
{
printf("\n Enter the name of the day:");
scanf("%s", week[i].dayName);
printf("\n Enter the date of the day:");
scanf("%d", &week[i].date);
printf("\n Enter the description of the activity of the 
day:");
scanf("%s", week[i].description);
}
}
void display()
{
int i;
for (i = 0; i < 7; i++)
{
printf("\n Name of the day: %s",week[i].dayName);
printf("\n Date of the day: %d", week[i].date);
printf("\n Activity of the day: %s", week[i].description);
}
}
void main()
{
create();
read();
display();
}
2)Design, Develop and Implement a Program in C for the following operations on Strings
a. Read a main String (STR), a Pattern String (PAT) and a Replace String (REP)
b. Perform Pattern Matching Operation: Find and Replace all occurrences of PAT in STR with REP if 
PAT exists in STR. Report suitable messages in case PAT does not exist in STR.
Support the program with functions for each of the above operations. Don't use Built-in functions
ans->#include <stdio.h>
char str[100], pat[100], rep[100], ans[100];
int s1, s2, j, c, k, flag = 0;
void read()
{
printf("\nEnter a string \n");
gets(str);
printf("\nEnter a pattern string to search \n");
gets(pat);
printf("\nEnter a replace string \n");
gets(rep);
}
void search()
{
s1 = s2 = c = j = 0;
while (str[c] != '\0')
{
if (str[s1] == pat[s2])
{
s1++;
s2++;
if (pat[s2] == '\0')
{
for (k = 0; rep[k] != '\0'; k++, j++)
ans[j] = rep[k];
s2 = 0;
c = s1;
flag = 1;
}
}
else
{
ans[j++] = str[c++];
s1 = c;
s2 = 0;
} 
} 
if (flag == 0)
{
printf("OOPS!!!Pattern Not found!!!!!\n");
}
else
{
ans[j] = '\0'; 
printf("\nThe resultant string is\n %s", ans);
}
} 
void main()
{
read();
search();
}
3)Design, Develop and Implement a menu driven Program in C for the following operations on STACK of 
Integers (Array Implementation of Stack with maximum size MAX)
a. Push an Element on to Stack
b. Pop an Element from Stack
c. Demonstrate how Stack can be used to check Palindrome
d. Demonstrate Overflow and Underflow situations on Stack
e. Display the status of Stack
f. Exit
Support the program with appropriate functions for each of the above operations
ans->#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
#define MAX 10
int stack[MAX], item, ch, top = -1, count = 0, status = 0, ele;
void push(int item)
{
if (top == MAX - 1)
printf("\n\n*** Stack Overflow ***");
else
{
stack[++top] = item;
status++;
}
}
int pop()
{
if (top == -1)
printf("\n\n*** Stack Underflow ***");
else
{
ele = stack[top--];
status--;
printf("\nPopped element is %d", ele);
}
return ele;
} /*End of pop function*/
/* Function to check stack elements are palindrome of not*/
void palindrome()
{
int i, temp;
temp = status;
if (top != -1)
{
for (i = 0; i < temp; i++)
{
if (stack[i] == pop())
count++;
}
if (temp == count)
printf("\n Stack contents are Palindrome");
else
printf("\n Stack contents are NOT palindrome");
}
else
printf("\n*** No Elements in stack to check for palindrome 
***\n");
}
void display()
{
int i;
if (top == -1)
printf("\nOOPS!!!! Stack is Empty");
else
{
printf("\nThe stack contents are:");
for (i = top; i >= 0; i--)
printf("\n ----\n| %d |", stack[i]);
}
} 
void main()
{
for (;;)
{
printf("\n\n---------MAIN MENU---------\n");
printf("\n1. PUSH \n2. POP \n3. DISPLAY\n");
printf("\n4.PALINDROME \n5. Exit");
printf("\n-------------------------------------\n");
printf("\nEnter Your Choice: ");
scanf("%d", &ch);
switch (ch)
{
case 1:
printf("\nEnter single element to be pushed: ");
scanf("%d", &item);
push(item);
display();
break;
case 2:
ele=pop();
break;
case 3:
display();
break;
case 4:
palindrome();
break;
case 5:
exit(0);
default:
printf("\n Invalid choice \n");
}
}
}
4)Design, Develop and Implement a Program in C for converting an Infix Expression to Postfix Expression. 
Program should support for both parenthesized and free parenthesized expressions with the operators: +, -, 
*, /, %(Remainder), ^(Power) and alphanumeric operands.
ans->#include <stdio.h>
#include <conio.h>
#include <string.h>
int top = -1, pos = 0;
char symbol, temp, infix[20], stack[20], postfix[20];
void push(char symbol)
{
stack[++top] = symbol;
} 
char pop()
{
return (stack[top--]);
}
int preced(char symbol) 
{
int p;
switch (symbol)
{
case '^':
p = 3;
break;
case '/':
case '*':
case '%':
p = 2;
break;
case '+':
case '-':
p = 1;
break;
case ')':
case '(':
p = 0;
break;
case '#':
p = -1;
break;
}
return (p);
} 
void ifix_pfix()
{
int i = 0;
push('#');
while (i < strlen(infix))
{
symbol = infix[i];
switch (symbol)
{
case '(':
push(symbol);
break;
case ')':
temp = pop();
while (temp != '(')
{
postfix[pos++] = temp;
temp = pop();
}
break;
case '^':
case '+':
case '-':
case '*':
case '/':
case '%':
while (preced(stack[top]) >= preced(symbol))
{
postfix[pos++] = pop();
}
push(symbol);
break;
default:
postfix[pos++] = symbol;
break;
}
i++;
}
while (top > 0)
{
postfix[pos++] = pop();
}
} 
void main()
{
printf("Enter the Infix expression--->");
scanf("%s", infix);
ifix_pfix();
printf("Postfix expression is---> %s\n", postfix);
} 
5)Design, Develop and Implement a Program in C for the following Stack Applications
a. Evaluation of Suffix expression with single digit operands and operators: +, -, *, /, %, ^
ans->#include <stdio.h>
#include <math.h>
#include <string.h>
#include <conio.h>
#define MAX 20
float stack[MAX];
char postfix[MAX];
int top=-1;
int isoperand(char x) { 
if (x >= '0' && x <= '9')
return 1; 
else
return 0; 
} 
void push(float x) { 
stack[++top] = x;
}
float pop()
{ 
return stack[top--];
} 
float operate(float op1, float op2, char a) 
{ 
float res;
switch (a) 
{ 
case '+': res = op2 + op1; break; 
case '-': res = op2 - op1; break; 
case '*': res = op2 * op1; break; 
case '/': res = op2 / op1; break; 
case '^': res = pow(op2, op1); break;
} 
return res;
} 
void main() 
{ 
int i = 0; 
float ans, op1, op2; 
char symbol;
printf("Enter Expression:"); 
scanf("%s", postfix); 
while (i < strlen(postfix)) 
{ 
symbol = postfix[i];
if (isoperand(symbol)) 
push(symbol-48); //Convert the character to numeric value 
else
{ 
op1 = pop(); 
op2 = pop(); 
ans = operate(op1, op2, symbol); 
push(ans); 
printf("%.2f %c %.2f = %.2f\n", op2, symbol, op1, ans); 
} 
i++;
} 
printf("%s = %.2f", postfix, stack[top]);
getch();
} 
5b)b. Solving Tower of Hanoi problem with n disks.
ans5b->#include <stdio.h>
#include <conio.h>
void towers(int num, char source, char dest, char aux)
{
if (num == 1)
{
printf("\n Move disk 1 from peg %c to peg %c", source, 
dest);
return;
}
towers(num - 1, source, aux, dest);
printf("\n Move disk %d from peg %c to peg %c", num, source, 
dest);
towers(num - 1, aux, dest, source);
}
void main()
{
int num;
printf("Enter the number of disks : ");
scanf("%d", &num);
printf("The sequence of moves involved in the Tower of Hanoi are 
:\n");
towers(num, 'A', 'C', 'B');
}
6)Design, Develop and Implement a menu driven Program in C for the following operations on Circular 
QUEUE of Characters (Array Implementation of Queue with maximum size MAX) 
a. Insert an Element on to Circular QUEUE 
b. Delete an Element from Circular QUEUE
c. Demonstrate Overflow and Underflow situations on Circular QUEUE 
d. Display the status of Circular QUEUE
e. Exit.
Support the program with appropriate functions for each of the above operations
ans->
#include <stdio.h>
#include <stdlib.h>
#define MAX 3
int q[MAX], i, rear = -1, front = -1;

void insert(int x)
{
    if (front == (rear + 1) % MAX)
    {
        printf("Q is Full!!\n");
    }
    else if (front == -1 && rear == -1)
    {
        front = rear = 0;
        q[rear] = x;
    }
    else
    {
        rear = (rear + 1) % MAX;
        q[rear] = x;
    }
    printf("\nCircular Queue Status:Rear = %d Front = %d \n", rear, front);
}

void delete ()
{
    if (front == -1 && rear == -1)
    {
        printf("Q is Empty!!\n");
    }
    else if (front == rear)
    {
        printf("The deleted item is %d\n", q[front]);
        front = rear = -1;
    }
    else
    {
        printf("The deleted item is %d\n", q[front]);
        front = (front + 1) % MAX;
    }
    printf("\nCircular Queue Status:Rear = %d Front = %d \n", rear, front);
}

void display()
{
    int i;
    if (rear == -1 && front == -1)
        printf("Queue is empty\n");
    else
    {
        printf("Q Contents are: ");
        for (i = front; i != rear; i = (i + 1) % MAX)
            printf("%d\t", q[i]);
        printf("%d\n", q[rear]);
    }
}

void main()
{
    int ch, num;
    for (;;)
    {
        printf("\nMAIN MENU \n 1.INSERTION \n 2.DELETION \n"); 
        printf(" 3.DISPLAY \n 4.EXIT");
        printf("\nENTER YOUR CHOICE : ");
        scanf("%d", &ch);
        switch (ch)
        {
            case 1:printf("\nENTER THE QUEUE ELEMENT : ");
                   scanf("%d", &num);
                   insert(num);
                   display();
                   break;
            case 2: delete (); 
                    break;
            case 3: display(); 
                    break;
            case 4: exit(0); 
            default: printf("\nInvalid Choice.");
        } 
    } 
}

