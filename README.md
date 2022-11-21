# basic_calculator_py

````py
class Solution:
    def calculate(self, s: str) -> int:
        stack = []
        op = 0 
        res = 0 # on going result
        sign  = 1 # positive
        
        for ch in s: 
            if ch.isdigit():
                op = (op * 10) + int(ch)
            
            elif ch == '+': 
                res += sign * op
                sign = 1
                op = 0
                
            elif ch == '-':
                res += sign * op
                sign = -1
                op = 0
            
            elif ch == '(':
                stack.append(res)
                stack.append(sign)
                sign = 1
                res = 0
                
            elif ch == ')': 
                res += sign * op
                res *= stack.pop()
                res +=stack.pop() # stack pop 2, operand
                op = 0
        return res + sign * op
        
        
        
        Algorithm

Iterate the expression string one character at a time. Since we are reading the expression character by character, we need to be careful when we are reading digits and non-digits.
The operands could be formed by multiple characters. A string "123" would mean a numeric 123, which could be formed as: 123 >> 120 + 3 >> 100 + 20 + 3. Thus, if the character read is a digit we need to form the operand by multiplying 10 to the previously formed continuing operand and adding the digit to it.
Whenever we encounter an operator such as + or - we first evaluate the expression to the left and then save this sign for the next evaluation.

If the character is an opening parenthesis (, we just push the result calculated so far and the sign on to the stack (the sign and the magnitude) and start a fresh as if we are calculating a new expression.
If the character is a closing parenthesis ), we first calculate the expression to the left. The result from this would be the result of the expression within the set of parenthesis that just concluded. This result is then multiplied with the sign, if there is any on top of the stack. Remember we saved the sign on top of the stack when we had encountered an open parenthesis? This sign is associated with the parenthesis that started then, thus when the expression ends or concludes, we pop the sign and multiply it with result of the expression. It is then just added to the next element on top of the stack.
````
