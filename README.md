# README.md

## LINK TO VIDEO https://youtu.be/-GZi4bjsTJA
## Overview


This project implements a **Backgammon Analyser** web application that allows users to input Backgammon board positions, specify dice rolls, and analyze the best moves.


1. **Evaluate Page**: Allows users to interact with the board, input dice rolls, and receive move suggestions.
2. **Instructions Page**: Provides detailed guidelines on how to use the webapp effectively.


---


## Getting Started




### Prerequisites
Before running the application, ensure the following are installed:
- [Docker](https://www.docker.com/)
- [NGINX](https://www.nginx.com/) (optional, if using a reverse proxy)


### Installation Steps


1. **Download Project Files**: Ensure all necessary files are accessible on your system.


2. **Run the Backgammon Web API**:
  ```bash
  docker run -p 8081:8081 foochu/bgweb-api:latest
  ```


3. **(Optional) Set Up NGINX Reverse Proxy**:
  - Create an NGINX configuration file with the following content:
    ```nginx
    server {
        listen 8080;


        location /api/ {
            proxy_pass http://localhost:8081/;
            proxy_set_header Host $host;
        }
    }
    ```
  - Save the file as `backgammon.conf` in your NGINX configuration directory.
  - Reload NGINX:
    ```bash
    sudo nginx -s reload
    ```


4. **Start the Webapp**:
  - Use a live server extension in your code editor or a simple HTTP server:
    ```bash
    python -m http.server
    ```
  - Open [http://127.0.0.1:5500/index.html](http://127.0.0.1:5500/index.html) in your browser.


5. **Stopping Services**:
  - List running Docker containers:
    ```bash
    docker ps
    ```
  - Stop the container:
    ```bash
    docker stop <container_id>
    ```
  - Stop NGINX:
    ```bash
    sudo nginx -s stop
    ```


---


## Using the Webapp


### Navigation


The webapp features a navigation bar for switching between the main pages:


- **Evaluate Page**: For interactive board setup and move analysis.
- **Instructions Page**: For detailed usage guidance and tips.


### Evaluate Page Features
The main **Evaluate** page provides:
- **Interactive Backgammon Board**: Allows placement of up to six checkers per point.
- **Dice Roll Input**: A text field to specify dice rolls.
- **Action Buttons**: For placing and deleting checkers
 - **"Get Best Move"**: Submits the position to the API for analysis.
 - **"Clear Board"**: Resets the board to its initial state.


### Instructions for Using the Analyzer


#### Placing Checkers
1. Click the **"White"** or **"Black"** button to select the checker color.
2. Click any blank spot on the board to place a checker of the selected color.


#### Deleting Checkers
1. Click the **"Delete"** button to remove misplaced checkers.
2. Alternatively, use **"Clear Board"** to reset the entire board.


#### Board Orientation
For accurate analysis:
- The player’s #1 point should be in the bottom-right corner.
- Movement of the game is counterclockwise, with #24 in the top-right.
- Mirror positions accordingly if your board orientation differs.


#### Inputting Dice Rolls
Enter dice rolls in the format `#, #` (e.g., `3, 5`).


#### Submitting a Position
1. Ensure the board setup and dice roll are correct.
2. Click **"Get Best Move"** to analyze the position.


### Results and Suggestions
- The top engine move is visualized on the board:
 - Start and end points are highlighted.
- A textual breakdown of the top 1-3 moves is displayed below the board, along with:
 - Winning percentage
 - Gammon percentage (WinG)
 - Backgammon percentage (WinBG)
- Visual highlights disappear after 5 seconds, but textual results remain.


---


## Error Handling
The application provides feedback for:
- Incorrect dice roll formats.
- Incorrect dice numbers.
- Missing or excess checkers (15 per color required).
- Invalid board configurations.


---


## FAQ


### Is my browser data saved or shared?
No, all data is processed locally in your browser. The app does not store or share any personal data.


### Why is the "Get Best Move" button not working?
This button works properly only after:
- The board setup is valid (15 checkers per color).
- A valid dice roll has been entered.
- Use the alerts to fix any mistakes.


### How can I analyze positions during the bear-off phase?
This application focuses on the beginning and middle stages of backgammon, where analysis is most beneficial. It is less suited for late-game scenarios like bearing off checkers.
---


Thank you for using the Backgammon Webapp!
