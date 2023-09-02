jLox
====

Following the amazing book by **Robert Nystorm**, [***Crafting the Interpreter***](https://t.ly/8d1o0). This repo 
closely follows the book, including enhancement proposed as challenge questions.

Required `Java >= 13` if one does not want to refactor the code.

## 1. Tree-Walk Interpreter
- `20230830`: Lexer done!
  * Added support for C-style `/* ... */` block comments (challenge problem!)
- `20230831`: Building AST with Visitor Pattern
- `20230901` Expression parser done!
  * TODO: challenge problems -- `comma` operator support, Ternary `?:` operator support
- `20230902`: Expression evaluator in progress.