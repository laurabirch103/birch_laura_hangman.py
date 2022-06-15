def get_word(): file = open('word_list.txt') 
#opens word_list file words = file.readlines() 
#reads lines word = random.choice(words) 
#randomly selects word from file word = str(word).strip('\n') #strips each word at start of new line file.close() 
#closes the read file return word 
#provides the word
def get_word(): file = open('word_list.txt') #opens word_list file words = file.readlines() #reads lines word = random.choice(words) #randomly selects word from file word = str(word).strip('\n') #strips each word at start of new line file.close() #closes the read file return word #provides the word

#Function to play Hangman def play_game(): alphabet = 'abcdefghijklmnopqrstuvwxyz'
word = get_word() #Calls the function to get the random word from the file letters_guessed = [] #sets list up for letters guessed tries = 7 #sets number of tries guessed = False #sets boolean to be used for While loop

import random                       #imports random function

# Function to import the word from the provided list
def get_word():
    file = open('word_list.txt')    #opens word_list file
    words = file.readlines()        #reads lines
    word = random.choice(words)     #randomly selects word from file
    word = str(word).strip('\n')    #strips each word at start of new line
    file.close()                    #closes the read file
    return word                     #provides the word

#Function to play Hangman
def play_game():
    alphabet = 'abcdefghijklmnopqrstuvwxyz'     
    word = get_word()                       #Calls the function to get the random word from the file
    letters_guessed = []                    #sets list up for letters guessed
    tries = 7                               #sets number of tries
    guessed = False                         #sets boolean to be used for While loop

    print('The word contains', len(word), 'letters.')               #says how many letters in word at start
    print(len(word) * '*')                                          #prints word but replaces everything with stars
    while guessed == False and tries > 0:                           #while loop to keep cycling through while guessing
        guess = input('Please enter your next guess: ').lower()     #asks for next guess by user
        #1 - user inputs a letter
        if len(guess) == 1:                                         #checks if guess is just 1 character long
            if guess not in alphabet:                               #checks if is a letter
                print('You have not entered a letter.')
            elif guess in letters_guessed:                          #checks if already guessed the letter
                print('You have already guessed that letter before.')
            elif guess not in word:                                 #checks if in word
                print('Sorry, that letter is not part of the word :(')
                letters_guessed.append(guess)                       #adds guessed letter to list of letters guessed
                tries -=1                                           #reduces life by 1
            elif guess in word:                                     #correct letter guessed  
                print('Well done, that letter exists in the word!')
                letters_guessed.append(guess)

        #2 - user inputs the full word
        elif len(guess) == len(word):                           #if user guesses whole word in one go
            if guess == word:                                   #If correctly got word, user wins
                print('Congratulations you win!')
                guessed = True
            else:
                print('You Lose :(')                            #If incorrectly guessed letters and run out of tries, user loses
                tries -= 1

        #3 - user inputs letters where the total number of letters does not equal total number of letters in the word.  
        else:
            print('The length of your guess is not the same as the length of the word we\'re looking for.')

        #Section to print the starred out word with correctly guessed letters added in
        status = ''                                 
        if guessed == False:
            for letter in word:
                if letter in letters_guessed:
                    status += letter
                else:
                    status += '*'
            print(status)

        #Section to see if user has guessed word, one letter at a time, within tries limit
        if status == word:
            print('Congratulations you win!')
            guessed = True
        elif tries == 0:
            print('You Lose')

play_game()                                             
