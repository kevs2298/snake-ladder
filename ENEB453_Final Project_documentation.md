***ENEB453- Web-Based Application Development Final Project***

# Setup

a. Download\
   &nbsp;i. Phone\
      &nbsp;&nbsp;1. nRF Connect Mobile app\
   ii. Laptop
      2. Docker Desktop app.
      2. MongoDB Compass.
b. Use the cd command to go to the folder of the project.
c. Install @abandonware/bleno package for Bluetooth connection with ble to the existing app.
   i. Type “npm install @abandonware/bleno – save” on the terminal pointing to the folder

# Created an interface for a Bluetooth Low-Energy (BLE) device.

a. Created a BLE interface that provides a service that existing Bluetooth low energy (BLE) devices can make a connection to and send data to the game. To do so, bleno is the BLE package provided by the nodejs that was used.
   i. Steps
      1. Required the bleno package.
      2. Created a bleno primary service that had a device named “ENEB453”, a service UUID and a characteristic UUID. The properties of the characteristics were ‘read’ and ‘write’. Next, we defined bleno.on so that when the app is run the service starts advertising. This enables the service to be discoverable by other BLE devices that are nearby
b. Validated incoming data from the BLE device to make sure it was numeric and in the range from 1 to 6.
   i. Steps
      1. When receiving data from bluetooth from BLE, in the useEffect function, we check that the input is between 1 and 6. This check also ensures that the input is numeric.

# Propagated data to react and make the game interactable

a. Propagated the data from BLE to the frontend interface, to move the second player.
   i. Steps
      1. After validating the data, we use the ipcRenderer.on to propagate the BLE data to the second player. This data is used as the value of the dice for that player. Data can come from any BLE device that is connected to the service, so it allows users to play the game wirelessly.
b. Added sound on a dice roll and when a player wins.
   i. Steps
      1. Import the audio files using Audio(‘path to audio’).
      2. Created two functions, one for roll dice music and another one for winning music. When one of the two events happens, the corresponding function gets called. The function uses Audio.play(). So, in the function gameRollDice, the startmusicdice() function is called, and in the PlayerUpdatePosition function, when a player wins, the startmusicwin() function is called.
c. Added user-friendly design to the application. Such as a congratulations pop-up message when a player wins.
   i. Pop up screen shows the winner.
      1. Steps
         a. PlayerUpdatePosition function, when a player wins, we send a message to react. React then responds to the event and shows a dialog box that displays congratulations to the player that won the game.

   ii. Separate control panel for two players.
      1. Steps
         a. In the player dashboard component, we added a new div that contains the control panel for the second player. Added all the tags such as component name, roll and move buttons, and interface.

# Stored Game data in MongoDB.

a. Stored the game’s progress in MongoDB, like the position of every player every time it moves, and if a player wins.
   i. Steps
      1. Everytime a player moves, we post the player’s position to mongoDB using a mongoose model. Especifically, we use the ‘save’ method to save the message in MongoDB. The messages are stored in the test database.
      2. When a particular player wins, a message is also posted to MongoDB, using the same method as above.

# To start the game
a. Open the docker application, and then run the command “docker-compose up” to start the database.
b. Open nRF Connect Mobile app for BLE device simulator, and use the scanner to scan the nearby device.
c. Connect to the device name called ENEB453.
d. The player can write a value to the game as shown below. As the example in the screenshot, 3 will appear on the second control panel.
   i. image.png
e. Open the Mongo DB Compass and then set up an advanced connection. The username and password can be found in docker-compose.yml.
   i. image.png

# Pushed the final project to a new Git Repository.
a. Create a public repository and push your final project in that.
   i. Steps
      1. Check if there is a current remote by checking the version
         a. git remote -v
      2. To remove any existing remote use this:
         a. git remote remove origin
      3. Run the command to push code to the desired GitHub repository.
         a. echo "# repository name >> README.md
         b. git init
         c. git add .
         d. git commit -m "first commit"
         e. git branch -M main
         f. git remote add origin followed by repository address
         g. git push -u origin main
