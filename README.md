#txt code for game in bash

#!/bin/bash



# Define game rooms as files

room1="kitchen.txt"

room2="bedroom.txt"



# Function to create room files if they don't exist

create_rooms() {

  if [[ ! -e "$room1" ]]; then

    echo "You find yourself in a kitchen. There is a door to the left and a window to the right." > "$room1"

  fi



  if [[ ! -e "$room2" ]]; then

    echo "You find yourself in a bedroom. There is a bed in the center and a closet on the side." > "$room2"

  fi

}



# Function to display room description and choices

display_room() {

  cat "$1"

}



# Function to display current CPU and memory usage

display_system_resources() {

  echo "Current System Resources:"

  echo "CPU Usage: $(top -bn1 | grep "Cpu(s)" | awk '{print $2 + $4 "%"}')"

  echo "Memory Usage: $(free -m | awk 'NR==2 {print $3 "MB used / " $2 "MB total"}')"

}



# Function to handle player choices

handle_choice() {

  if [[ "$1" -eq 1 ]]; then

    echo "You chose to explore the next room."

    next_room="$room2"

  elif [[ "$1" -eq 2 ]]; then

    echo "You decided to stay in this room."

    exit 0

  elif [[ "$1" -eq 3 ]]; then

    echo "You checked the current system resources."

    display_system_resources

  else

    echo "Invalid choice. Please try again."

    read -p "Enter your choice: " choice

    handle_choice "$choice"

  fi

}



# Main game logic

create_rooms



clear

echo "Welcome to the Enhanced Text-Based Adventure Game!"

echo "You find yourself in a kitchen. What would you like to do?"

echo "1. Explore the next room"

echo "2. Stay in this room"

echo "3. Check current system resources"



# Adding a delay of 2 seconds before displaying the next message

sleep 2



# Read player's choice

read -p "Enter your choice: " choice

handle_choice "$choice"

display_room "$next_room"



# Adding another delay of 2 seconds before displaying system resources

sleep 2

display_system_resources



# End of game

echo "Game over. Thanks for playing!"
