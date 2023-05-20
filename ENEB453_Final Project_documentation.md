***ENEB453- Web-Based Application Development Final Project***

# Setup

a. Download\
   &nbsp;i. Phone\
      &nbsp;&nbsp;1. nRF Connect Mobile app\
   &nbsp;ii. Laptop\
      &nbsp;&nbsp;1. Docker Desktop app.\
      &nbsp;&nbsp;2. MongoDB Compass.\
b. Use the cd command to go to the folder of the project.\
c. Install @abandonware/bleno package for Bluetooth connection with ble to the existing app.\
   &nbsp;i. Type “npm install @abandonware/bleno – save” on the terminal pointing to the folder\

# Created an interface for a Bluetooth Low-Energy (BLE) device.

a. Created a BLE interface that provides a service that existing Bluetooth low energy (BLE) devices can make a connection to and send data to the game. To do so, bleno is the BLE package provided by the nodejs that was used.\
   &nbsp;i. Steps\
      &nbsp;&nbsp;1. Required the bleno package.\
      &nbsp;&nbsp;2. Created a bleno primary service that had a device named “ENEB453”, a service UUID and a characteristic UUID. The properties of the characteristics were ‘read’ and ‘write’. Next, we defined bleno.on so that when the app is run the service starts advertising. This enables the service to be discoverable by other BLE devices that are nearby\
b. Validated incoming data from the BLE device to make sure it was numeric and in the range from 1 to 6.\
   &nbsp;i. Steps\
      &nbsp;&nbsp;1. When receiving data from bluetooth from BLE, in the useEffect function, we check that the input is between 1 and 6. This check also ensures that the input is numeric.\

# Propagated data to react and make the game interactable

a. Propagated the data from BLE to the frontend interface, to move the second player.\
   &nbsp;i. Steps\
      &nbsp;&nbsp;1. After validating the data, we use the ipcRenderer.on to propagate the BLE data to the second player. This data is used as the value of the dice for that player. Data can come from any BLE device that is connected to the service, so it allows users to play the game wirelessly.\
b. Added sound on a dice roll and when a player wins.\
   &nbsp;i. Steps\
      &nbsp;&nbsp;1. Import the audio files using Audio(‘path to audio’).\
      &nbsp;&nbsp;2. Created two functions, one for roll dice music and another one for winning music. When one of the two events happens, the corresponding function gets called. The function uses Audio.play(). So, in the function gameRollDice, the startmusicdice() function is called, and in the PlayerUpdatePosition function, when a player wins, the startmusicwin() function is called.\
c. Added user-friendly design to the application. Such as a congratulations pop-up message when a player wins.
   &nbsp;i. Pop up screen shows the winner.\
      &nbsp;&nbsp;1. Steps\
         &nbsp;&nbsp;&nbsp;a. In the PlayerUpdatePosition function, when a player wins, we send a message to react. React then responds to the event and shows a dialog box that displays congratulations to the player that won the game.\

   &nbsp;ii. Separate control panel for two players.\
      &nbsp;&nbsp;1. Steps\
         &nbsp;&nbsp;&nbsp;a. In the player dashboard component, we added a new div that contains the control panel for the second player. Added all the tags such as component name, roll and move buttons, and interface.\

# Stored Game data in MongoDB.

a. Stored the game’s progress in MongoDB, like the position of every player every time it moves, and if a player wins.\
   &nbsp;i. Steps\
      &nbsp;&nbsp;1. Everytime a player moves, we post the player’s position to mongoDB using a mongoose model. Especifically, we use the ‘save’ method to save the message in MongoDB. The messages are stored in the test database.\
      &nbsp;&nbsp;2. When a particular player wins, a message is also posted to MongoDB, using the same method as above.\

# To start the game
a. Open the docker application, and then run the command “docker-compose up” to start the database.\
b. Open nRF Connect Mobile app for BLE device simulator, and use the scanner to scan the nearby device.\
c. Connect to the device name called ENEB453.\
d. The player can send a value by going to the UTF-8 tab and writing a value between 1 and 6.\
e. Open the Mongo DB Compass and then set up an advanced connection. The username and password can be found in docker-compose.yml.Navigate to the 'test' database and you will see the game data\

# Pushed the final project to a new Git Repository.
a. Create a public repository and push your final project in that.\
   &nbsp;i. Steps\
      &nbsp;&nbsp;1. Check if there is a current remote by checking the version\
         &nbsp;&nbsp;&nbsp;a. git remote -v\
      &nbsp;2. To remove any existing remote use this:\
         &nbsp;&nbsp;&nbsp;a. git remote remove origin\
      &nbsp;3. Run the command to push code to the desired GitHub repository.\
         &nbsp;&nbsp;&nbsp;a. echo "# repository name >> README.md\
         &nbsp;&nbsp;&nbsp;b. git init\
         &nbsp;&nbsp;&nbsp;c. git add .\
         &nbsp;&nbsp;&nbsp;d. git commit -m "first commit"\
         &nbsp;&nbsp;&nbsp;e. git branch -M main\
         &nbsp;&nbsp;&nbsp;f. git remote add origin followed by repository address\
         &nbsp;&nbsp;&nbsp;g. git push -u origin main\
