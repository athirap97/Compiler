# Compiler
A sample compiler that we generated

Group-4
Name:Arjun C Ramesh(13)
     Arundhati Kurup(14)
     Athira S Pillai(15)
     Athul Raj(16)
     
COMPILER
A compiler is a software program that transforms high-level source code that is written by a developer in a high-level programming language into a low level object code (binary code) in machine language, which can be understood by the processor. The process of converting high-level programming into machine language is known as compilation.
The processor executes object code, which indicates when binary high and low signals are required in the arithmetic logic unit of the processor.

DESIGN PHASES
 1.Lexical analysis 
	 The compiler converts the sequence of characters that appear in the source code into a series of strings of characters (known as tokens), which are associated by a specific rule by a program called a lexical analyzer. A symbol table is used by the lexical analyzer to store the words in the source code that correspond to the token generated.
2.Syntax analysis 
	Syntax analysis is performed, which involves preprocessing to determine whether the tokens created during lexical analysis are in proper order as per their usage. The correct order of a set of keywords, which can yield a desired result, is called syntax. The compiler has to check the source code to ensure syntactic accuracy.
3.Semantic analysis 
	This step is comprised of several intermediate steps. First, the structure of tokens is checked, along with their order with respect to the grammar in a given language. The meaning of the token structure is interpreted by the parser and analyzer to finally generate an intermediate code, called object code.
4.Intermediate code generation (Three address code)
	Three address code is an intermediate code used by optimizing compilers to aid in the implementation of code-improving transformations. Each three address code  instruction has at most three operands and is typically a combination of assignment and a binary operator. Since three-address code is used as an intermediate language within compilers, the operands will most likely not be concrete memory addresses or processor registers, but rather symbolic addresses that will be translated into actual addresses during register allocation.

LEX 
•	The main job of a lexical analyzer (scanner) is to break up an input stream into more usable elements (tokens)   for eg: a = b + c * d;
 			ID ASSIGN ID PLUS ID MULT ID SEMI 
•	Lex is an utility to help you rapidly generate your scanners
•	Lexical analyzers tokenize input streams 
•	Tokens are the terminals of a language
YACC (Yet Another Compiler Compiler)
•	Tool which will produce a parser for a given grammar 
•	YACC is a program designed to compile a LALR(1) grammar 
•	Produces the source code of the syntactic analyzer of the language produced by a grammar

COMPILER DESIGN
Introduction

This compiler was designed with the primary objective of evaluation different types of expressions. The various types of instructions considers for designing
 
1.Arithmetic expressions with nested parenthesis  (Sample input : ((1+2)*((4*5)+3))) 
2.Trigonometric expressions   (Sample input : sin(30)+cos(0))
3.Mathematical expressions  (Sample input : sqrt(5)/sqrt(2) )
4.Logical expressions ( Sample input : 1&1 , !1 , (1|1)&(!0) *combinations sin(30)+12-5*cos(90))
The designed phases include :
Lexical Analysis
Syntax Analysis
Semantic Analysis
Intermediate Code generation (3 Address form )
Methodology
The objective at hand was thoroughly discussed and analysed .Various test inputs were formulated . After suitable collection of materials and a  clear understanding of the working environment /tools , the underlying language and grammar was written . The language and grammar were coded to generate the compiler using lex/yacc tools . Based on various  inputs , suitable modifications were made to the design in successive iterations

PHASE 1 - Lex Source Program (using lex tool) 
•	Lex source program is a table of regular expressions and corresponding program fragments
•	The table is translated to a C program (lex.yy.c) which reads an input stream partitioning the input into strings which match the given expressions and copying it to an output stream if necessary.
•	Lex source is separated into three sections by % % delimiters

calc.l
%{
#include<stdio.h>
#include<stdlib.h>
#include <math.h>
%}
DIGIT [0-9]+\.?|[0-9]*\.[0-9]+
%%
{DIGIT} 	{yylval=atof(yytext);return NUM;}
"exit" 		{return exit_command;}
cos|COS 	{return COS;}
sin|SIN 	{return SIN;}
tan|TAN 	{return TAN;}
log|LOG 	{return LOG;}
sqrt|SQRT 	{return SQRT;}
\n|. 		{return yytext[0];}
PHASE 2- YACC source program (using yacc tool)
calc.y 
S : S E '\n' { printf("Answer: %g \nEnter next expression:\n", $2); }
 | S '\n' | | error '\n' { yyerror("Error: Enter once more...\n" );yyerrok; } ; 
E : E '+' E { $$ = $1 + $3; }    | E'-'E { $$=$1-$3; }     | E'*'E { $$=$1*$3; }   |E'/'E { $$=$1/$3; }
 |E'&'E	 { $$=(int)$1&(int)$3; }	 	|E'|'E	 { $$=(int)$1|(int)$3; } 		
| '('E')' { $$=$2; } 
| NUM | COS'('E')' {$$=cos($3);} 	
| SIN'('E')' {$$=sin($3);}	 
| TAN'('E')' {$$=tan($3);}	 
| LOG'('E')' {$$=log($3);} 	
| SQRT'('E')' {$$=sqrt($3);} 
| exit_command {exit(EXIT_SUCCESS);} ; 

PHASE 3 (3 address generation)
prog : prog expr '\n' {printf("%c = %c\n",p,p-1);}|;
expr : STR| expr '+' expr {if(i==0){ printf("%c = %d %c %d\n",p,$1,'+',$3); p++;i++;}
else{ printf("%c = %c %c %d\n",p,p-1,'+',$3);p++;}}
| expr '-' expr {if(i==0){ printf("%c = %d %c %d\n",p,$1,'-',$3); p++;i++;}
else{ printf("%c = %c %c %d\n",p,p-1,'-',$3);p++;}}
| expr '*' expr {if(i==0){ printf("%c = %d %c %d\n",p,$1,'*',$3); p++;i++;}
else{ printf("%c = %c %c %d\n",p,p-1,'*',$3);p++;}}
| expr '/' expr {if(i==0){ printf("%c = %d %c %d\n",p,$1,'/',$3); p++;i++;}
else{ printf("%c = %c %c %d\n",p,p-1,'/',$3);p++;}}
| expr '%' expr {if(i==0){ printf("%c = %d %c %d\n",p,$1,'%',$3); p++;i++;}
else{ printf("%c = %c %c %d\n",p,p-1,'%',$3);p++;}}
| expr '&' expr {if(i==0){ printf("%c = %d %c %d\n",p,$1,'&',$3); p++;i++;}
else{ printf("%c = %c %c %d\n",p,p-1,'&',$3);p++;}}

CONSTRAINTS AND FUTURE SCOPE
● Three address including trigonometric expressions 
● Variable assignments using symbol table and further evaluations 
● Semantic checking for complex logical expressions and including relational expressions 
● Including more math functions like power , roots (except square root) , ncr,npr etc.

REFERENCES
1.	A Reference for Lex Specifications - lex & yacc, 2nd Edition [Book] - https://www.safaribooksonline.com/library/view/lex-yacc/9781565920002/ch06.html
2.	Lex & Yacc for Compiler Writing -     https://www.cs.clemson.edu/course/cpsc827/material/LexYacc/Introduction.pdf
3.	https://stackoverflow.com/questions/
4.	Compilers - OpenClassroom - Stanford University- openclassroom.stanford.edu/MainFolder/DocumentPage.php?course=Compilers
5.	https://www.mkssoftware.com/docs/rn/relnotes_ly331.htm


