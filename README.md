# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# Date: 20-11-2026
# AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM
cdex3.l
```
%{
#include "y.tab.h"
%}

digit   [0-9]
%%
[ \t\n]+        ; // Ignore whitespace
{digit}+        { yylval = atoi(yytext); return NUMBER; }
[\+\-\*/]       { return *yytext; }
\(              { return '('; }
\)              { return ')'; }
.               { return 0; }
%%
int yywrap() { return 1; }
```

cdex3.y
```
%{
#include <stdio.h>
#include <stdlib.h>
void yyerror(const char *s);
int yylex(void);
%}

%token NUMBER

%%
expr:   expr '+' term
        | expr '-' term
        | term
        ;

term:   term '*' factor
        | term '/' factor
        | factor
        ;

factor: '(' expr ')'
        | NUMBER
        ;

%%

void yyerror(const char *s) {
    printf("Invalid arithmetic expression.\n");
}

int main() {
    printf("Enter an arithmetic expression: ");
    if (yyparse() == 0)
        printf("Valid arithmetic expression.\n");
    return 0;
}
```
# OUTPUT
https://private-user-images.githubusercontent.com/150931013/491530774-e8b89680-1ef8-40e5-8ec2-ff14348ffd45.png?jwt=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3OTUxNTYwNDEsIm5iZiI6MTc5NTE1NTc0MSwicGF0aCI6Ii8xNTA5MzEwMTMvNDkxNTMwNzc0LWU4Yjg5NjgwLTFlZjgtNDBlNS04ZWMyLWZmMTQzNDhmZmQ0NS5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjYxMTIwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI2MTEyMFQwNjIyMjFaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT01MzE2NjU2M2I4Y2M5Y2JkYWZkMjMzNjk0ZDFiNjBlOTYyZGY1MGNkNDA2NGEwZGY4ZWMwZWY0MWY0ZTlkZmZmJlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCZyZXNwb25zZS1jb250ZW50LXR5cGU9aW1hZ2UlMkZwbmcifQ.OFsBXFAfegFM6hD_ai9uGOdILfcDEVQEDQnfoVZsr7s
# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
