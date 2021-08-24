# 계산기

1. 중위 표기법을 후위 표기법으로 변경

|      | isp  | icp  |
| ---- | ---- | ---- |
| )    | -    | -    |
| *, / | 2    | 2    |
| +, - | 1    | 1    |
| (    | 0    | 3    |

- icp > isp이면 push, top이 낮은 겨우이면 pop
- 빈 스택이면 push
- 닫힌 괄호일 때 여는 괄호를 만날 때까지 pop

2. 후위 표기법을 스택으로 계산

   - 연산자를 만난 경우 스택 상위 2개를 꺼내어 계산하고 다시 stack에 넣는다

```python
test_cases = 10


def make_postfix(expr: str):
    op = {
        '(': 0,
        '+': 1,
        '*': 2,
    }

    stack = []
    postfix = ''
    for e in expr:
        if e.isdecimal():
            postfix += e
        else:
            if e == '(':
                stack.append(e)
            elif e == ')':
                while stack and stack[-1] != '(':
                    postfix += stack.pop()
                stack.pop()
            else:
                while stack and op[e] <= op[stack[-1]]:
                    postfix += stack.pop()
                stack.append(e)
    while stack:
        postfix += stack.pop()

    return postfix


def solve_postfix(pf: str):
    stack = []
    for e in pf:
        if e.isdecimal():
            stack.append(int(e))
        else:
            num2 = stack.pop()
            num1 = stack.pop()
            if e == '+':
                stack.append(num1 + num2)
            elif e == '*':
                stack.append(num1 * num2)

    return stack[0]


for t in range(1, test_cases + 1):
    length = int(input().strip())
    expression = input().strip()
    postfix = make_postfix(expression)
    result = solve_postfix(postfix)
    print('#{} {}'.format(t, result))

```



