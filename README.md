# BigTalk: SmallTalk Semantic Analyzer & Code Generator — NMU CS322 Final Project Fall 2024 Semester

Clone and open with [Squeak.](https://squeak.org)

BigTalk is a statically typed structured programming language. The language structures supported are demonstrated below.
#### Program Declaration
```
program
do
    writeString "Hello, World!"

program
variables
    fact7 : integer
    msg : string
    count : integer

methods
    function factorial(n : integer) : integer
    do
        [if n = 0 then
            factorial <- 1
        else
            factorial <- n * factorial(n - 1)]

    procedure doIt(count : integer, msg : string)
    variables
        tmpVar:integer
    do
       [tmpVar <- 9
       while tmpVar > 0 do
          tmpVar <- tmpVar - 1]
        
    function nine():integer
    do nine <- 9

do
    [fact7 <- factorial( 7 )
     writeString "Factorial 7 is "
     writeInteger fact7
     writeln]   
```
#### Variable Declarations
```
msg : string
count : integer
isDone : boolean
```
#### Compound Statement
Multiple statements may be aggregated into a compound statment that may be used anywhere a statement is expected.
```
[count <- 9
msg <- "Hello there!"
doSomeWork()]
```
#### Conditional Statements
There are two kinds of conditional statements, if/then and it/then/else.
```
if isHungry() then
   eat()

if isHungry() then
   eat()
else
   sleep()
```
#### Loop Statement
The only supported loop statement is the while loop.
```
while 3 < 4 do writeString "looping"
```
#### Assignment Statement
```
answer <- 42
```
#### Procedure Definition
```
procedure procWithNoTemps(myParam : integer) 
do 
    writeInteger myParam

procedure procWithTemps(myParam : integer)
variables
    count : integer
    answer : integer
do
    [writeInteger count
    writeLine]
```
#### Function Definition
```
function messageOfTheDay() : string
do
    messageOfTheDay <- "Good Morning!"
    
```
#### Binary Operators
```
 < > = 
 + - * / MOD 
 AND OR
```
#### Unary Operator
```
NOT <boolean expression>
```
### Literal values (string integer boolean)
```
"This is a string."
0 1 2 3
true false
```
#### Procedure call statement
```
procWithTemps(9)
```
#### Function call expression
```
msg <- messageOfTheDay()
```
#### Complex Expressions
```
(3 + 2) * 4 - 2
```
# Ohm Grammar Definition

```
BigTalk {

	Program
    	= "program" VariableDeclarations? MethodDeclarations? "do" Statement+
        
    VariableDeclarations
    	= "variables" VariableDeclaration+
    
    VariableDeclaration
    	= identifier ":" Type
        
    MethodDeclarations 
    	= "methods" (FunctionDeclaration | ProcedureDeclaration)+
    
    FunctionDeclaration 
    	= "function" identifier ParameterList ":" Type "do" Statement
        
    ProcedureDeclaration
    	= "procedure" identifier ParameterList VariableDeclarations? "do" Statement+
        
    CompoundStatement
    	= "[" Statement+ "]"
        
    Statement
    	= CompoundStatement
        | ConditionalStatement
        | AssignmentStatement
       	| ProcedureCallStatement
        | LoopStatement
        | IOStatement
        
    IOStatement
    	= "writeString" (identifier | string) --writeString
        | "writeInteger" (identifier | number) --writeNumber
        | "writeln"
    
    ParameterList 
    	= "(" ListOf<Parameter, ","> ")"
    
    Parameter
    	= identifier ":" Type
        
    Type
    	= "boolean"
        | "integer"
        | "string"
        
    ProcedureCallStatement
    	= identifier ArgumentsList
    
    ArgumentsList
    	= "(" ListOf<Expression, ","> ")"
    
    ConditionalStatement
    	= IfThenElseStatement
        | IfThenStatement
    
    IfThenStatement
    	= "if" Expression "then" Statement
    
    IfThenElseStatement
    	= "if" Expression "then" Statement "else" Statement
    
    LoopStatement
    	= "while" Expression "do" Statement
    
    Expression
    	= BinaryExpression
        | UnaryExpression
        | FunctionExpression
        | identifier
        | Literal
        
    
    AssignmentStatement
    	= identifier "<-" Expression

	word 
    	= letter alnum*
        
    keyword
    	= binaryOperator
        | unaryOperator
        | boolean
        | "methods"
        | "function"
        | "if"
        | "then"
        | "else"
        | "while"
        | "writeString"
        | "writeInteger"
        | "writeln"
        | "variables"
    
    identifier (an identifier)
    	= ~keyword word
    
    BinaryExpression = Expression binaryOperator Expression
    
    UnaryExpression = unaryOperator Expression
    
    FunctionExpression = identifier ArgumentsList
        
    binaryOperator
    	= "<"
        | ">"
        | "="
		| "+"
        | "-"
        | "*"
        | "/"
        | "MOD"
        | "AND"
        | "OR"
        
    unaryOperator
    	= "NOT"
        
    Literal
    	= string
        | boolean
        | number
    
    number (a number)
        = digit+
        
    boolean
    	= "true"
        | "false"
        
    string
    	= "\"" (~"\"" any | "\"\"")* "\""

}
```
