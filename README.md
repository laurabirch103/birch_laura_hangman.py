import random

def play_again():
    answer = input('Would you like to play again? yes/no').lower()
    if answer == 'y' or answer =='yes':
        play_game()
    else:
        pass

def get_word():
    file = open('word_list.txt') 
    words = file.readlines() 
    word = random.choice(words) 
    word = str(word).strip('\n') 
    file.close()
    return word

def play_game():
    alphabet = 'abcdefghijklmnopqrstuvwxyz'
    word = get_word()
    letters_guessed = []
    tries = 7
    guessed = False

    print('The word contains', len(word), 'letters.')
    print(len(word) * '*')
    while guessed == False and tries > 0:
        print('You have ' + str(tries) + ' tries')
        guess = input('Please enter your next guess: ').lower()
        #1 - user inputs a letter
        if len(guess) == 1:
            if guess not in alphabet:
                print('You have not entered a letter.')
            elif guess in letters_guessed:
                print('You have already guessed that letter before.')
            elif guess not in word:
                print('Sorry, that letter is not part of the word :(')
                letters_guessed.append(guess)
                tries -=1
            elif guess in word:
                print('Well done, that letter exists in the word!')
                letters_guessed.append(guess)
            #   k = word.count(guess) #k stores the number of times the guessed letter occurs in the word
            #   for _ in range(k):    
            #        letterGuessed += guess # The guess letter is added as many times as it occurs
            #    # Print the word
            #    for char in word:
            #        if char in letterGuessed and (Counter(letterGuessed) != Counter(word)):
            #            print(char, end = ' ')
            #            correct += 1
            else:
                print('No idea why we get this message, should be investigated further!')

        #2 - user inputs the full word
        elif len(guess) == len(word):
            if guess == word:
                print('Congratulations you win!')
                guessed = True
            else:
                print('You Lose :(')
                tries -= 1

        #3 - user inputs letters where the total number of letters =/= total number of letters in the word.  
        else:
            print('The length of your guess is not the same as the length of the word we\'re looking for.')

        status = ''
        if guessed == False:
            for letter in word:
                if letter in letters_guessed:
                    status += letter
                else:
                    status += '*'
            print(status)

        if status == word:
            print('Congratulations you win!')
            guessed = True
        elif tries == 0:
            print('You Lose')

    play_again()

play_game()
