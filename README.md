## maix-starwars-model
Create and train a Star Wars character classification model with Maixhub. Using the online model training you can create a model for either object classification or detection.


#Preparing the Dataset
Following the instructions here to bulk download some images of your favourite Star Wars characters  
Clean up the images to remove anything that will confuse the machine learning algorithm  
Use a bulk image transformation tool to resize all the images to 224x224  

Create a folder structure like this  
datasets  
--c3po  
--r2d2  
--vader  
--yoda  
containing all the files. Zip this structure so you have a file datasets.zip  

#Setting up for Model Training at MaixHub
To use the online model training you have to provide a key from your hardware. Note that following this procedure permanently disables the JTAG port.
Download the key_gen_v1.2.bin binary from this repo
Windows users can download the kflash-gui from this repo  (or from SiPEED here - https://dl.sipeed.com/MAIX/tools/kflash_gui/kflash_gui_v1.6.5)
Plug in your Maix board, choose the correct Port, click 'Open File' and selected the key_gen binary and click 'Download' to upload to your board
In a serial terminal (you can use the Arduino serial monitor for this) check for the key when you reset the board.

MaixHub Account Setup
Go to https://www.maixhub.com/ and create an account  
Log in and go to the model training page here: https://www.maixhub.com/mtrain.html  
Enter your login email, the key from your board and choose Object Classification and click 'Next'  
Upload the datasets.zip file you created earlier and click 'Start Training'  
It should start training within a few minutes. If nothing has happened after an hour, try again.  
The model and other files with be sent as a link to your email address.  

Running the Model on your Board
Check the warning.txt in the folder you downloaded for any serious problems
Copy the entire contents of the directory to a FAT (not FAT32 or exFat) formatted microSD card. The partition size must be less than 4GB to format a FAT partition. The easiest option is to use a 4GB card
Insert the card into the board
Download the firmware from this repo or download the latest from here: https://dl.sipeed.com/shareURL/MAIX/MaixPy/release/master You need a version with '_mimimum' in the filename to leave space for the model file.
Flash the firmware in the same way as the key_gen.

