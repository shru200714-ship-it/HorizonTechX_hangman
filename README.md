# HorizonTechX_hangman
# ============================================
#           HANGMAN GAME IN PYTHON
# ============================================

import random

word_list = [
    "python",
    "computer",
    "keyboard",
    "hangman",
    "programming"
]


def play_game():

    # Select a random word
    secret_word = random.choice(word_list)

    # Store guessed letters
    guessed_letters = []

    # Maximum incorrect guesses
    max_attempts = 6
    attempts_left = max_attempts

    print("\n" + "=" * 45)
    print("          WELCOME TO HANGMAN")
    print("=" * 45)
    print("Guess the hidden word one letter at a time.")
    print(f"You have {max_attempts} incorrect guesses.\n")

    # Main game loop
    while attempts_left > 0:

        # Display current word
        display_word = ""

        for letter in secret_word:
            if letter in guessed_letters:
                display_word += letter + " "
            else:
                display_word += "_ "

        print("\nWord :", display_word)
        print("Guessed Letters :", " ".join(guessed_letters))
        print("Attempts Left :", attempts_left)

        # Check if player won
        if "_" not in display_word:
            print("\n🎉 Congratulations!")
            print("You guessed the word:", secret_word.upper())
            return

        # User input
        guess = input("\nEnter a letter: ").lower().strip()

        # Validate input
        if len(guess) != 1:
            print("Please enter only ONE letter.")
            continue

        if not guess.isalpha():
            print("Please enter alphabet letters only.")
            continue

        # Already guessed
        if guess in guessed_letters:
            print("You already guessed that letter.")
            continue

        guessed_letters.append(guess)

        # Correct guess
        if guess in secret_word:
            print("Correct!")
        else:
            attempts_left -= 1
            print("Wrong!")

    # If loop ends, player loses
    print("\nGame Over!")
    print("The correct word was:", secret_word.upper())


# ============================
# Play Again Loop
# ============================

while True:

    play_game()

    choice = input("\nDo you want to play again? (yes/no): ").lower()

    if choice != "yes":
        print("\nThanks for playing Hangman!")
        print("Have a great day!")
        break
