Name: Kaiyue Zhou, Kevin Coello Section: ENEB453

Due date: May 20, 2023

***ENEB453- Web-Based Application Development Final Project***

1\. Setup

1. Download
1. Phone
   1. nRF Connect Mobile app
1. Laptop
1. Docker Desktop app.
1. MongoDB Compass.
2. Use the cd command to go to the folder of the project.
2. Install @abandonware/bleno package for Bluetooth connection with ble to the existing app.

i. Type “npm install @abandonware/bleno – save” on the terminal pointing to the folder

2\. Created an interface for a Bluetooth Low-Energy (BLE) device.

1. Created a BLE interface that provides a service that existing Bluetooth low energy (BLE) devices can make a connection to and send data to the game. To do so, bleno is the BLE package provided by the nodejs that was used.

i. Steps

1. Required the bleno package.
1. Created a bleno primary service that had a device named “ENEB453”, a service UUID and a characteristic UUID. The properties of the characteristics were ‘read’ and ‘write’. Next, we defined bleno.on so that when the app is run the service starts advertising. This enables the service to be discoverable by other BLE devices that are nearby
2. Validated incoming data from the BLE device to make sure it was numeric and in the range from 1 to 6.

i. Steps

1\. When receiving data from bluetooth from BLE, in the useEffect function, we check that the input is between 1 and 6. This check also ensures that the input is numeric.

3\. Propagated data to react and make the game interactable

1. Propagated the data from BLE to the frontend interface, to move the second player.

i. Steps

1\. After validating the data, we use the ipcRenderer.on to propagate the BLE data to the second player. This data is used as the value of the dice for that player. Data can come from any BLE device that is connected to the service, so it allows users to play the game wirelessly.

2. Added sound on a dice roll and when a player wins.

i. Steps

1. Import the audio files using Audio(‘path to audio’).
1. Created two functions, one for roll dice music and another one for winning music. When one of the two events happens, the corresponding function gets called. The function uses Audio.play(). So, in the function gameRollDice, the startmusicdice() function is called, and in the PlayerUpdatePosition function, when a player wins, the startmusicwin() function is called.
3. Added user-friendly design to the application. Such as a congratulations pop-up message when a player wins.
1. Pop up screen shows the winner.

1\. Steps

a. PlayerUpdatePosition function, when a player wins, we send a message to react. React then responds to the event and shows a dialog box that displays congratulations to the player that won the game.

2. Separate control panel for two players.

1\. Steps

a. In the player dashboard component, we added a new div that contains the control panel for the second player. Added all the tags such as component name, roll and move buttons, and interface.

4\. Stored Game data in MongoDB.

a. Stored the game’s progress in MongoDB, like the position of every player every time it moves, and if a player wins.

i. Steps

1. Everytime a player moves, we post the player’s position to mongoDB using a mongoose model. Especifically, we use the ‘save’ method to save the message in MongoDB. The messages are stored in the test database.
2. When a particular player wins, a message is also posted to MongoDB, using the same method as above.
5. Start the game
1. Open the docker application, and then run the command “docker-compose up” to start the database.
1. Open nRF Connect Mobile app for BLE device simulator, and use the scanner to scan the nearby device.
1. Connect to the device name called ENEB453.
1. The player can write a value to the game as shown below. As the example in the screenshot, 3 will appear on the second control panel.

i. ![](Aspose.Words.40d2cf1d-60b5-47ac-9843-a40ef2763965.001.jpeg)

5. Open the Mongo DB Compass and then set up an advanced connection. The username and password can be found in docker-compose.yml.

i. ![](Aspose.Words.40d2cf1d-60b5-47ac-9843-a40ef2763965.002.jpeg)

6. Push your final project to a new Git Repository.

a. Create a public repository and push your final project in that.

i. Steps

1. Check if there is a current remote by checking the version
   1. git remote -v
1. To remove any existing remote use this:
   1. git remote remove origin
1. Run the command to push code to the desired GitHub repository.
1. echo "# repository name >> README.md
1. git init
1. git add .
1. git commit -m "first commit"
1. git branch -M main
1. git remote add origin followed by repository address
1. git push -u origin main
