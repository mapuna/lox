jLox
====
Following the amazing book by **Robert Nystorm**, [***Crafting the Interpreter***](https://t.ly/8d1o0). This repo
closely follows the book, including enhancement proposed as challenge questions.

Required `Java >= 13` if one does not want to refactor the code.

# 1. The Lox Grammar

## Start
```program        → declaration* EOF ;```

## Declarations
```
declaration    → classDecl
               | funDecl
               | varDecl
               | statement ;

classDecl      → "class" IDENTIFIER ( "<" IDENTIFIER )?
                 "{" function* "}" ;
funDecl        → "fun" function ;
varDecl        → "var" IDENTIFIER ( "=" expression )? ";" ;
```
## Statements
```
statement      → exprStmt
               | forStmt
               | ifStmt
               | printStmt
               | returnStmt
               | whileStmt
               | block ;

exprStmt       → expression ";" ;
forStmt        → "for" "(" ( varDecl | exprStmt | ";" )
                           expression? ";"
                           expression? ")" statement ;
ifStmt         → "if" "(" expression ")" statement
                 ( "else" statement )? ;
printStmt      → "print" expression ";" ;
returnStmt     → "return" expression? ";" ;
whileStmt      → "while" "(" expression ")" statement ;
block          → "{" declaration* "}" ;` 
```
Note that `block` is a statement rule, but is also used as a nonterminal in a couple of other rules for things like function bodies.

## Expressions
```
expression     → assignment ;

assignment     → ( call "." )? IDENTIFIER "=" assignment
               | logic_or ;

logic_or       → logic_and ( "or" logic_and )* ;
logic_and      → equality ( "and" equality )* ;
equality       → comparison ( ( "!=" | "==" ) comparison )* ;
comparison     → term ( ( ">" | ">=" | "<" | "<=" ) term )* ;
term           → factor ( ( "-" | "+" ) factor )* ;
factor         → unary ( ( "/" | "*" ) unary )* ;

unary          → ( "!" | "-" ) unary | call ;
call           → primary ( "(" arguments? ")" | "." IDENTIFIER )* ;
primary        → "true" | "false" | "nil" | "this"
               | NUMBER | STRING | IDENTIFIER | "(" expression ")"
               | "super" "." IDENTIFIER ;

```

## Utility Rules
Keep the other rules cleaner.
```
function       → IDENTIFIER "(" parameters? ")" block ;
parameters     → IDENTIFIER ( "," IDENTIFIER )* ;
arguments      → expression ( "," expression )* ; 
```

# 2. Lexical Grammar
```
NUMBER         → DIGIT+ ( "." DIGIT+ )? ;
STRING         → "\"" <any char except "\"">* "\"" ;
IDENTIFIER     → ALPHA ( ALPHA | DIGIT )* ;
ALPHA          → "a" ... "z" | "A" ... "Z" | "_" ;
DIGIT          → "0" ... "9" ;

```

# 3. Tree-Walk Interpreter progress
- `20230830`: Lexer done!
  * Added support for C-style `/* ... */` block comments (challenge problem!)
- `20230831`: Building AST with Visitor Pattern
- `20230901` Expression parser done!
  * TODO: challenge problems -- `comma` operator support, Ternary `?:` operator support
- `20230902`: Expression evaluator done.
- `20230903`: Take #1 -- statement parsing and evaluation done. Global variable handling is done.
- `20220904`: Take #2 -- variable assignment done. Next TODO: Scoping.
- `20230908`: Take #3 -- completed statement execution with scoping.
  * TODO: Fix REPL to execute expressions and statements
  * Fix implicit assignment to `nil` -- make it an error if a var is not assigned in a scope.
- `20230908`: Completed control flow (`if`/`else`, `while`, `for`)
- `20230910`: Completed function decls and calls. Starting with closures, resolving and binding."
- `20230910`: Closures work!