# projectrosen
This is my cryptology project
import random

# Function to display reward
def display_reward(amount):
    print("""
    ***************************************
    *                                     *
    *   Congratulations! You have won    *
    *           {} RUBLES!                *
    *                                     *
    ***************************************
    """.format(amount))

# Function to encode a message using numbers (A=1, B=2, ..., Z=26)
def encode_message(message):
    encoded = []
    for char in message.upper():
        if char.isalpha():
            # Convert the character to its corresponding number
            encoded.append(str(ord(char) - ord('A') + 1))
        else:
            # For spaces and non-alphabet characters, just append
            encoded.append(' ')
    return ' '.join(encoded)

# Function to ask the final question
def final_question():
    correct_answer = "John Hanson"
    
    print("\nNow that you've won the guessing game, let's move on to the final question!")
    print("Answer correctly, and you will claim your 2000 RUBLES prize!")
    
    # Game loop for final question
    while True:
        answer = input("Who is the first president of the United States? ").strip()
        if answer.lower() == correct_answer.lower():
            print("Correct! You've won the 2000 RUBLES!")
            return 2000  # Return the prize amount if they answer correctly
        else:
            print("Incorrect answer. Try again.")

# Function to ask the decoding challenge question
def decoding_challenge():
    # Message to decode (encoded as numbers)
    encoded_message = encode_message("If you have decoded this, you have quadrupled your payment")
    
    print("\nNow, for the final challenge! Decode the following message:")
    print(encoded_message)
    
    # Game loop for decoding challenge
    while True:
        decoded_message = input("Enter the decoded message: ").strip()
        
        # The correct decoded message
        correct_decoded_message = "If you have decoded this, you have quadrupled your payment"
        
        if decoded_message.lower() == correct_decoded_message.lower():
            print("Congratulations! You've decoded the message correctly.")
            return 8000  # Quadruple the reward
        else:
            print("That's not quite right. Try again.")

# Function to play the number guessing game
def guess_the_number():
    # Generate a random number between 1 and 100
    number_to_guess = random.randint(1, 100)
    attempts = 0
    guessed = False

    print("Welcome to the Guess the Number game!")
    print("I am thinking of a number between 1 and 100.")
    
    # Game loop for number guessing
    while not guessed:
        # Prompt the player for a guess
        player_guess = input("Enter your guess: ")
        
        # Check if input is a valid number
        if player_guess.isdigit():
            player_guess = int(player_guess)
        else:
            print("Please enter a valid number.")
            continue
        
        # Increment the attempt counter
        attempts += 1

        # Compare the player's guess to the number
        if player_guess < number_to_guess:
            print("Too low! Try again.")
        elif player_guess > number_to_guess:
            print("Too high! Try again.")
        else:
            print(f"Congratulations! You've guessed the right number {number_to_guess} in {attempts} attempts.")
            # Proceed to the final question after guessing the number correctly
            prize = final_question()
            if prize == 2000:
                # If they answered the final question correctly, they move on to decoding
                prize = decoding_challenge()
            display_reward(prize)  # Show the final reward amount
            guessed = True  # End the game when the they guess correctly

# Start the game
if __name__ == "__main__":
    guess_the_number()
