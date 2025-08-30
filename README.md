def precedence(op):
    if op in ('+', '-'):
        return 1
    if op in ('*', '/'):
        return 2
    if op == '^':
        return 3
    return 0

def infix_to_postfix(expression):
    stack = []  
    output = []
    
    for char in expression:
        if char.isalnum():
            output.append(char)
        
        elif char == '(':
            stack.append(char)
        
        elif char == ')':
            while stack and stack[-1] != '(':
                output.append(stack.pop())
            stack.pop()  
        else:
            while (stack and precedence(stack[-1]) >= precedence(char)):
                output.append(stack.pop())
            stack.append(char)
    
    while stack:
        output.append(stack.pop())
    
    return ''.join(output)

expr = input("Enter an infix expression: ")
print("Infix Expression: ", expr)
print("Postfix Expression: ", infix_to_postfix(expr))
