# Sipeed MaixPy Star Wars Character Detection Training
Train an image classification model with Maixhub to detect characters from Star Wars. Using online model training you can create a model for either object classification or detection. Note that this is AI 'on the edge' running on a microcontroller with MicroPython without internet connectivity.

![vader full](https://user-images.githubusercontent.com/60509953/106392797-d663ce80-63f3-11eb-8ffc-e784ee890f65.jpg)

## Preparing the Dataset for Classification
Following the instructions in the Collecting Images section from here - https://github.com/robotzero1/tf2-retrain-easy to bulk download some images of your favourite Star Wars characters.  
Remove anything that will confuse the machine learning algorithm.  
Use a bulk image resize tool to resize all the images to 224x224 (I used Fireworks. This is for GIMP https://alessandrofrancesconi.it/projects/bimp/ or most image editors offer this).

Create a folder structure like this  
-datasets  
 --c3po  
 --r2d2  
 --vader  
 --yoda  
containing the files for each character. Zip this structure so you have a file called datasets.zip  

## Setting up for Model Training at MaixHub
To use the online model training you have to provide a key from your hardware. Note that following this procedure permanently disables the JTAG port.  
Download the key_gen_v1.2.bin binary from this repo.  
Download kflash-gui from SiPEED here - https://dl.sipeed.com/MAIX/tools/kflash_gui/kflash_gui_v1.6.5.  
Unzip and run kflash_gui.exe in the kflash_gui folder.  
Plug in your Maix board, choose the correct Port, click 'Open File' and selected the key_gen binary and click 'Download' to upload to your board.  
In a serial terminal (you can use the Arduino serial monitor for this) check for the key when you reset the board.  

## MaixHub Account Setup
Go to https://www.maixhub.com/ and create an account.  
Log in and go to the model training page here: https://www.maixhub.com/mtrain.html.  
Enter your login email, the key from your board and choose Object Classification and click 'Next'.  
Upload the datasets.zip file you created earlier and click 'Start Training'.  
It should start training within a few minutes. If nothing has happened after an hour, try again.  
The model and other files with be sent as a link to your email address.  

## Running the Detection on your Board
Check the warning.txt in the folder linked in the email for any serious problems.  
I found that the labelling was wrong and I had to put this line in alphabetical order:  
labels = ["c3po", "r2d2", "vader", "yoda"]  
Copy the entire contents of the directory to a FAT (not FAT32 or exFat) formatted microSD card. The partition size must be less than 4GB to format a FAT partition. The easiest option is to use a 4GB card.  
Insert the card into the board.  
Download the firmware from this repo or download the latest from here: https://dl.sipeed.com/shareURL/MAIX/MaixPy/release/master You need a version with '_mimimum' in the filename to leave space for the model file.  
Flash the firmware in the same way as the key_gen in the first section.  
Reset the board and you should see the splash screen and then be able to test the detection.  
If it doesn't start, try connecting to a serial monitor to look for error messages.

![results](https://user-images.githubusercontent.com/60509953/106311191-0892f600-6265-11eb-9a53-b60bb8c28444.jpg)  

Quick video of testing the detection is here: https://youtu.be/K3XFobQzlH4


## Preparing for Object Detection
Object detection adds the ability to find the location and size of the object. The dataset requires manual labelling by a human for this to work.  
VoTT from Microsoft can be used for this. Download from here: https://github.com/Microsoft/VoTT/releases (For Windows use the -win32.exe download).  
Add all the 224px x 224px images into one directory.  
Follow the instructions here to add the directory and label the images: https://github.com/microsoft/VoTT#using-vott  
I found it worked with 107 tagged regions with about 35 for each of the three characters. Sipeed recommend 100 per object so in this test 300 tags.  
Export the labels in TensorFlow format. You should have this structure:  
-datasets
 --0.tfrecord
 --1.tfrecord
 --2.tfrecord
  ---tf_label_map.pbtxt  
Zip the datasets folder  
Assuming you have followed Maix Account Setup above, this time choose Object Detection and click 'Next'.  
Upload the datasets.zip file and click 'Start Training'.  
It should start training within a few minutes. If nothing has happened after an hour, try again.  
The model and other files with be sent as a link to your email address.  



