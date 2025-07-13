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