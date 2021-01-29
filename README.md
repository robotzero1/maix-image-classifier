# maix-starwars-model
Create and train a Star Wars character classification model with Maixhub. Using the online model training you can create a model for either object classification or detection.


Preparing the Dataset
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

Setting up for Model Training at MaixHub
To use the online model training you have to provide a key from your hardware. Note that following this procedure permanently disables the JTAG port.
Download the key_gen_v1.2.bin binary from this repo
Windows users can download the kflash-gui from this repo  (or from SiPEED here - https://dl.sipeed.com/MAIX/tools/kflash_gui/kflash_gui_v1.6.5)
Plug in your Maix board, choose the correct Port, click 'Open File' and selected the key_gen binary and click 'Download' to upload to your board
In a serial terminal (you can use the Arduino serial monitor for this) check for the key when you reset the board.

MaixHub Account Setup


