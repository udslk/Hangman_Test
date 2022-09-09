# Example Project Documentation Guideline
# Hangman Project Report
#### This project implements the Hangman game using Python programming language. The Hangman game asks the user to resolve the computer chosen word by asking the letters in the word interactively. If the user successfully resolves the word puzzle it will congratulate the user and stops the game. If the user fails to resolve the word puzzle by selecting the letter of the word incorrectly in five attempts (max), it will visualise the Hangman in stages for each failed attempt until it displays the Hangman completely at end of the game. This game uses the random Python library to select a word randomly from a given word list. This game is implemented using five project Milestones. It also uses Git DevOps tool to control the version of the source code and stores it in centralised repository system called GitHub.  

## Milestone1: Setup the Environment
- Setup the development environment with following necessary tools:
    - Visual Studio Code: Coding tool for Python Programming
    - Git: A tool that controls the version of source code in a repository
    - GitHub: A centralised repository system that track the changes to the code and stores it in  online.
    - Git Bash: A command line application runs on windows platform. This is used in the project to execute the Git commands

## Milestone 2: Implementation of ask_letter() method
- Copied the hangman_template.py to the local folder  by cloning the GitHub repository folder Hangman_Test as shown below:
    ```bash    
    udslk@DESKTOP-UAJ9FVT MINGW64 ~/Desktop
    $ git clone https://github.com/udslk/Hangman_Test.git
    ```
- Created another instance of the hangman_template.py file and renamed it as hangman_solution.py:
    ```bash
    udslk@DESKTOP-UAJ9FVT MINGW64 ~/Desktop/Hangman_Test/Hangman (main)
    $ ls -l
    total 20
    -rw-r--r-- 1 udslk 197609 4397 Aug 31 21:19 hangman_Template.py
    -rw-r--r-- 1 udslk 197609 8984 Sep  3 19:46 hangman_solution.py
    ```
- Implementation of ask_letter() method: This method asks the user interactively to enter a character. This function does following:
    - It checks whether user enters a valid single character, if not it prints "Please, enter just one character"
    - It checks whether letter has been tried already and if it has been tried it will print " The letter was already tried"
    - If it is a valid character it calls the check_letter() function to check whether character is in the word
- Below snippet shows the python code for this method:
  ```python
  def ask_letter(self):
        '''
        Asks the user for a letter and checks two things:
        1. If the letter has already been tried
        2. If the character is a single character
        If it passes both checks, it calls the check_letter method.
        '''
        while True:
            letter = input('Enter a single character:')
            if len(letter) > 1:
                print('Please, enter just one character')
            elif len(letter) == 1:
                    if self.list_letters.find(letter) == -1:
                        self.list_letters += letter
                        self.check_letter(letter)
                        break
                    else:                 
                        print(f'The letter \'{letter}\' was already tried')
            else:
                print('Please enter a character')

        # TODO 1: Ask the user for a letter iteratively until the user enters a valid letter
        # TODO 1: Assign the letter to a variable called `letter`
        # TODO 1: The letter has to comply with the following criteria: It has to be a single character. If it is not, print "Please, enter just one character"
        # TODO 2. It has to be a letter that has not been tried yet. Use the list_letters attribute to check this. If it has been tried, print "{letter} was already tried".
        # TODO 3: If the letter is valid, call the check_letter method
        pass
    ```

- Below screenshot shows the output of ask_letter() method:
>![image](images/ask_letter-method-output.png)

## Milestone 3: Initialisation of __init__ method
- This method initialises the following attributes of the game class:
    -  word: This is a string variable and getting initialised by choosing a word randomly from a word list by using "random" python library
    -  word_guessed: This is a list variable and been used to store letters which have been guessed correctly by the user. This is created first with the length of number of characters in the word and then assigns each item of the list with '_'.
    -  num_letters: This is an integer variable which stores the number of unique letters in the word.
    -  num_lives: This is an integer variable and used to store number of remaining attempts that user have to guess the letter. This is initialised with max attempts five.
    -   list_letters: This is a string variable and is used to store the letters that have already been tried. This is initialised with empty character ' '.       
-  Below snippet shows the python code for this method:
   ```python
   def __init__(self, word_list, num_lives=5):
        self.word = random.choice(word_list)
        self.num_letters = len(set(self.word))
        self.word_guessed = ['_']*len(self.word)
        self.num_lives = num_lives
        self.list_letters = ''
        
        print(f'The mystery word has {len(self.word)} characters')
        print(f'The word guessed is {self.word_guessed} ')
        
        # TODO 2: Initialize the attributes as indicated in the docstring
        # TODO 2: Print two message upon initialization:
        # 1. "The mystery word has {len(self.word)} characters" (The number of letters is NOT the UNIQUE number of letters)
        # 2. {word_guessed}
        pass
    ```
## Milestone 4: Implementation of Check_letter() method
- In this milestone the check_letter () is implemented to do following:
    - It takes user entered character in an input variable called 'letter' from ask_letter() method    
    - It checks if the user entered character is in the word
    - If the user enters a character from the word, it replaces the '_' in the guessed_word list with this character. Here it replaces at the same positions where this character is found in the word. 
    - Further it prints a message to let user know that character is in the word and prints the contents of guessed_word list variable
    - If the character in not found in the word, it reduces the num_lives variable by one and then it prints a message to let user know that the character is not found in the word and another message which shows the remaining attempts that the use can try to guess the letter correctly.
- Below snippet shows the python code for this method:
    ```python
    def check_letter(self, letter) -> None:
        '''
        Checks if the letter is in the word.
        If it is, it replaces the '_' in the word_guessed list with the letter.
        If it is not, it reduces the number of lives by 1.

        Parameters:
        ----------
        letter: str
            The letter to be checked
        '''
        if self.word.find(letter.lower()) != -1:
            print(f'Nice! \'{letter.lower()}\' is in the word!')
            for i, ch in enumerate(self.word): 
                if ch == letter.lower(): self.word_guessed[i] = ch
            self.num_letters -=1
            print(f'{self.word_guessed}, where guessed word now has unveiled the letter(s)')
        else:
            self.num_lives -= 1
            print(f'Sorry, \'{letter}\' is not in the word!')
            if self.num_lives != 0:
                print(f'You have {self.num_lives} lives left...')
                self.draw_hangman_stages()
        # TODO 3: Check if the letter is in the word. TIP: You can use the lower() method to convert the letter to lowercase
        # TODO 3: If the letter is in the word, replace the '_' in the word_guessed list with the letter
        # TODO 3: If the letter is in the word, the number of UNIQUE letters in the word that have not been guessed yet has to be reduced by 1
        # TODO 3: If the letter is not in the word, reduce the number of lives by 1
        # Be careful! A word can contain the same letter more than once. TIP: Take a look at the index() method in the string class
        pass
    ```

## Milestone 5: Implementation of logic the game and adding extra methods to draw the hangman
- Following logic is added in the main play_game() method: 
    -   It gives maximum five attempts to the user to guess the correct word and if the user guesses the word correctly it prints "CONGRATULATIONS! you won" and stops the game. 
    -   If the user guesses the letter in the word incorrectly it starts to draw the Hangman's body in stages. It starts with head then neck, etc., for each failed attempt. If the user loses all five attempts, it draws complete Hangman's body and stops the game.
- Below snippet shows the python code for play_game() method:
    ```python
    def play_game(word_list):
    # As an aid, part of the code is already provided:
    game = Hangman(word_list, num_lives=5)
    
    while game.num_lives > 0:
        game.ask_letter()
        if ''.join(game.word_guessed) == game.word :
            print('CONGRATULATIONS! you won')
            break
        elif game.num_lives == 0:
            print(f'You ran out of lives. The word was {game.word}')
            game.draw_hangman_stages()
            break
    
    # TODO 1: To test this task, you can call the ask_letter method
    # TODO 2: To test this task, upon initialization, two messages should be printed 
    # TODO 3: To test this task, you call the ask_letter method and check if the letter is in the word
    # TODO 4: Iteratively ask the user for a letter until the user guesses the word or runs out of lives
    # If the user guesses the word, print "Congratulations, you won!"
    # If the user runs out of lives, print "You ran out of lives. The word was {word}"

    pass
    ```
- Below snippet shows the python code for the methods used to draw the Hangman
    ```python
    def draw_hangman_head(self):
        ch = ''
        for i in range(0,10): ch += ' '
        for i in range(0,10): ch += '_'
        print(ch)
        
        ch = ''
        for i in range(0,10): ch += ' '
        ch += '|'
        for i in range(0,8): ch += ' '
        ch += '|'
        print(ch)

        ch = ''
        for i in range(0,10): ch += ' '
        ch += '|'
        for i in range(0,8): ch += ' '
        ch += 'O'
        print(ch)
        pass

    def draw_hangman_neck(self):
        ch = ''
        for i in range(0,10): ch += ' '
        ch += '|'
        for i in range(0,8): ch += ' '
        ch += '|'
        print(ch)
        pass

    def draw_hangman_arms(self):
        ch = ''
        for i in range(0,10): ch += ' '
        ch += '|'
        for i in range(0,7): ch += ' '
        ch += '/'
        if(self.num_lives == 2):
            ch += ' '
        else: 
            ch += '|'
        ch += '\\'
        print(ch)
        pass

    def draw_hangman_back(self):
        ch = ''
        for i in range(0,10): ch += ' '
        ch += '|'
        for i in range(0,8): ch += ' '
        ch += '| '
        print(ch)
        pass

    def draw_hangman_legs(self):
        ch = ''
        for i in range(0,10): ch += ' '
        ch += '|'
        for i in range(0,7): ch += ' '
        ch += '/'
        ch += ' '
        ch += '\\'
        print(ch)
        pass

    def draw_hangman_post(self,k):
        ch =''
        for i in range(0,10): ch += ' '
        ch += '|'
        for i in range(0,k): print(ch)
        print('--------------------')        
        pass

    def draw_hangman_stages(self):
        if (self.num_lives == 4):
            self.draw_hangman_head()
            self.draw_hangman_post(6)
        elif (self.num_lives == 3):
            self.draw_hangman_head()
            self.draw_hangman_neck()
            self.draw_hangman_post(5)
        elif (self.num_lives == 2):
            self.draw_hangman_head()
            self.draw_hangman_neck()
            self.draw_hangman_arms()
            self.draw_hangman_post(4)
        elif (self.num_lives == 1):
            self.draw_hangman_head()
            self.draw_hangman_neck()
            self.draw_hangman_arms()
            self.draw_hangman_back()
            self.draw_hangman_post(3)
        else:
            self.draw_hangman_head()
            self.draw_hangman_neck()
            self.draw_hangman_arms()
            self.draw_hangman_back()
            self.draw_hangman_legs()
            self.draw_hangman_post(2)      
        pass
    ```
 - Below screenshot shows the output when the user wins the game:
>![image](images\Success-Hangman.png)   
- Below screenshot shows the output when the user loses the game:
>![image](images\failure-Hangman.png) 

## Conclusions
- This project teaches how to write a simple python program. It teaches about,
    - what is a class and its contents, attributes, and methods
    - how to write a function
    - what is __init__ function 
    - how to write a while loop and for loop statements
    - how to define and use strings and list variables
- This code needs optimisation in-terms of using the memory efficiently, mainly using the list and string variables and the functions written for drawving the Hangman
