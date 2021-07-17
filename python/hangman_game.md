# hangman 게임 만들기

- csv 파일을에서 단어와 힌트 묶음을 읽음
- 묶음에서 5개 랜덤 뽑기
- 5 문제 중 3문제를 맞히면 성공 

```python
import time
import csv
import random

name = input("What is your name? ")

print("Hi, {}, Let's play a hangman".format(name))

print('Loading...')
time.sleep(1)
print()

words = []
with open('resource/word_list.csv', 'r') as f:
    reader = csv.reader(f)
    next(reader)
    for word in reader:
        words.append(word)

random.shuffle(words)
words = random.sample(words, 5)

print('Three out of five questions need to be answered.')
rounds = 5
success = 0
for i, word in enumerate(words):
    print('round {}'.format(i + 1))
    answer = word[0]
    hint = word[1]

    turns = 10
    guesses = ''
    while turns > 0:
        failed = 0
        for char in answer:
            if char in guesses:
                print(char, end='')
            else:
                print("_", end='')
                failed += 1
        print()

        if failed == len(answer) and turns < 10:
            print('Hint: {}'.format(hint))

        if failed == 0:
            print('Success')
            success += 1
            print()
            break

        print('You have {} chances'.format(turns)) if turns > 0 else print('You have no chance')
        guess = input('Guess a word: ')
        print()
        guesses += guess
        turns -= 1

    rounds -= 1
    if success == 3:
        print("Welcome, You're a genius.")
        print()
        break
    elif rounds < 4:
        print("Oops, You've got {} rounds left and you've got {}.".format(rounds, success))
        print()

```

