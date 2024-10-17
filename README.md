
# Ex-2-GENERATION OF LEXICAL TOKENS LEX FLEX TOOL
# Name:DAPPILI VASAVI
# Register Number: 212223040030
# AIM
## To write a lex program to implement lexical analyzer to recognize a few patterns.
# ALGORITHM

1.	Start the program.

2.	Lex program consists of three parts.

     a.	Declaration %%

     b.	Translation rules %%

     c.	Auxilary procedure.

3.	The declaration section includes declaration of variables, maintest, constants and regular definitions.
4.	Translation rule of lex program are statements of the form

    a.	P1 {action}

    b.	P2 {action}

    c.	…

    d.	…

    e.	Pn {action}

5.	Write a program in the vi editor and save it with .l extension.

6.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l $ cc lex.yy.c
7.	Compile that file with C compiler and verify the output.

# INPUT
```
#include <stdio.h>
#include <ctype.h>
#include <string.h>

int isKeyword(char buffer[]) {
    char keywords[5][10] = {"if", "else", "while", "for", "int"};
    for (int i = 0; i < 5; ++i) {
        if (strcmp(buffer, keywords[i]) == 0) {
            return 1;
        }
    }
    return 0;
}

int main() {
    char ch, buffer[15];
    char operators[] = "+-*/=";
    int i = 0;

    printf("Enter your input: ");

    while ((ch = getchar()) != EOF) {
        // Handle the double operator "=="
        if (ch == '=') {
            char next = getchar();
            if (next == '=') {
                printf("Operator: ==\n");
            } else {
                printf("Operator: =\n");
                ungetc(next, stdin); // Put back the character if it's not a part of "=="
            }
        } 
        // Identify single character operators
        else if (strchr(operators, ch)) {
            printf("Operator: %c\n", ch);
        } 
        // Handle alphanumeric characters
        else if (isalnum(ch)) {
            buffer[i++] = ch;
        } 
        // Handle end of tokens (keywords/identifiers/numbers) upon encountering a delimiter
        else if ((ch == ' ' || ch == '\n' || ch == '\t' || ch == ';' || ch == '(' || ch == ')') && i != 0) {
            buffer[i] = '\0'; // End the token string
            i = 0; // Reset index for the next token

            // Check if the token is a keyword
            if (isKeyword(buffer)) {
                printf("Keyword: %s\n", buffer);
            } 
            // Check if it's a number
            else if (isdigit(buffer[0])) {
                printf("Number: %s\n", buffer);
            } 
            // Otherwise, it's an identifier
            else {
                printf("Identifier: %s\n", buffer);
            }
        }
        
        // Skip over characters like parentheses, braces, etc.
        else if (ch == '(' || ch == ')' || ch == '{' || ch == '}') {
            continue;
        }
    }

    return 0;
}
```
# OUTPUT
![image](https://github.com/user-attachments/assets/36a75d84-2ec0-49a4-b0a5-e4b6f41b6a44)


# RESULT
The lexical analyzer is implemented using lex and the output is verified.
