# Rachelle Bassen

# print game instructions including background and direction commands
def game_instructions():
    print(
        "A paramecium is on the hunt for dinner across 8 different areas of the ocean.\n"
        "It must eat 6 microorganisms before its predator, the amoeba, will eat it for dinner instead!\n"
        "Eat all 6 food items without entering the area with the amoeba (the villain) to win the game.\n"
        "You are currently in the beach waves. Start the game by entering a direction to move to the next area.\n")
    print(
        "To move between regions of the ocean, enter the following commands: \"up,\" \"down,\" \"right,\" \"left\".\n"
        "You will need to enter the name of the food to grab it for dinner before moving to the next area.\n"
        "Enter \"exit\" to quit.")


# create a nested dictionary that links room names to directions and food items
all_areas = {
    'beach waves': {'up': 'tidal pool', 'right': 'coral reefs'},
    'tidal pool': {'down': 'beach waves', 'right': 'intertidal zone', 'food': 'bacterium'},
    'coral reefs': {'up': 'intertidal zone', 'right': 'sand bar', 'left': 'beach waves', 'food': 'chlorophyte'},
    'sand bar': {'down': 'ocean floor', 'up': 'rip tides', 'left': 'coral reefs', 'food': 'rhodophyte'},
    'rip tides': {'down': 'sand bar', 'right': 'fishing zone', 'food': 'yeast'},
    'ocean floor': {'up': 'sand bar', 'food': 'detritus'},
    'fishing zone': {'left': 'rip tides', 'food': 'cryptophyte'},
    'intertidal zone': {'down': 'coral reefs', 'left': 'tidal pool'}
}

# create empty area variable and inventory list to call inside loop and functions below
current_area = ()
inventory = []


# create function that prints status of paramecium including current area and inventory
def para_status(current_area, inventory):
    print('\tYou swam into the {}.'.format(current_area))
    print('\tWhat have you eaten?:', inventory)

# create function that determines the next area based on user-entered direction and dictionary key
# if different input is entered, return none (make user input again)
def get_new_area(direction, current_area):
    if direction in all_areas[current_area]:
        next_area = all_areas[current_area][direction]
        return next_area
    else:
        return None


# create function that calls food for current area in dictionary
def get_food(current_area):
    food = all_areas[current_area].get('food')

    while True:  # create loop to build inventory (food list) and exceptions

        if 'food' in all_areas[current_area]:  # if food is in the dictionary area...
            if food not in inventory:  # and if food has not yet been added to inventory...

                food_input = input("You found '{}'. Enter the name to eat it: ".format(food)).lower()
                # prompt for user input of food item (convert to lowercase)

                if food_input == food:  # If the input matches the dictionary food, add it to the inventory
                    inventory.append(food_input)
                    break  # break this loop to move onto next area

                else:
                    print('Invalid food name. Enter again.\n')  # must enter correct food name

            else:
                print("You already ate here.\n")
                break  # break loop to enter next direction if food already in inventory

        else:
            return False  # if there's no food in this area, return False (continue to next direction)

    return False  # return False to continue the game


# play again function to restart the game
def play_again():
    while True:
        repeat_input = input('Play again? "yes" or "no": ')

        if repeat_input.lower() == 'no':
            print('Exiting game.\n')
            return False  # if user enters no (convert to lower case), stop completely

        elif repeat_input.lower() == 'yes':  # if user enters yes, restart outer loop (lower case entry)
            return False, False

        else:
            print('Invalid input. Please enter "yes" or "no": ')
            # exception for incorrect entry


# create outer loop and print game instructions, starting area and empty inventory
while True:
    game_instructions()
    current_area = 'beach waves'
    inventory = []
    print('*************************************\n')    # separation line

    while len(set(inventory)) < 6:  # create inner loop that runs until inventory reaches 6 items
        print('\nParamecium status:')
        para_status(current_area, inventory)   # print paramecium status at loop repeat
        print('*************************************\n')
        next_direction = input("Enter a direction: ").lower()
        # print paramecium status and prompt user to enter a direction (convert to lower case)

        # exception: break loop anytime that user enters exit
        if next_direction == 'exit':
            break

        # update next_area using get_new_area function
        next_area = get_new_area(next_direction, current_area)

        # exception: if next_area is None then the direction is invalid. User must enter again.
        if next_area is None:
            print('Invalid entry.')
            continue

        # exception: if user enters area with amoeba, it is game over
        elif next_area.lower() == 'intertidal zone':
            print('You swam into the intertidal zone with the AMOEBA! It ate you for dinner!,\n')
            no_prompt, yes_prompt = play_again()  # trigger play again function
            if yes_prompt:
                continue  # this will break the outer loop and restart the game
            if not no_prompt:
                break  # this will stop the code completely (user enters "no")

        else:
            current_area = next_area
            para_status(current_area, inventory)
            # with no exceptions, next_area becomes the current_area
            # print paramecium status

        if 'food' in all_areas[current_area]:
            get_food(current_area)
        # if there is food in this area, start the get_food function to add new food to the inventory list

    else:
        print("\n***** \tYou found all six items to eat today! You'll live another day!\t *****")
        if not play_again(): # trigger play again function
            break # Return True to end the game, and True to restart if desired
