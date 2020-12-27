# TileMapper
A web base application to create tile maps out of large image files.  Its main aim is to allow the main image of the playfield or map to be loaded and sectioned into tiles of a predined dimension. After this process the tiles are put through a optimisation process to identify delete duplicate images replacing them within the map with a single tile reference. This keep file size and complexity of the map to a minimum.  A number of other tools will be available in due course. I have create a number of game design related tools in the past for both current and retro computers as this is an attempt to create 'one that rules them all'. 


## Content 
The project has two directories;

Original
This is the bear minimum and 'spike' project that holds simplistic and ugly code, the bare minimum to allow me to create a tile map for the game "Ice Cold Beer" (The progress of which can be found here in my VLogs )

Redesign
The directory contains two areas of interest.

redesign.html
This file is the first steps to a redesign.  It has no javascript code to control the options but is a redesign of the original using a more responsive and clean layout.

redesign (Vue)
This is the starts of the full redesign using the framework vue.js

## Installation (Original)

For the original and the redesign.html

To load the index htm can just be double clicked on.

1. Clone the repo 
2. Open a terminal and cd to the projecct directory 
3. Run the http server one-liner i.e. $ python -m SimpleHTTPServer 8000 
4. Open up a browser window and navigate to http://localhost:8000/original/index.html or http://localhost:8000/original/redesign.html (Replace the port with the port you have supplied). 

## Installation (Redesign)

The main redesign is in Vue.js in the redesign/tiller (vue) directory. You will need npm to install the project

sudo apt install npm

1. Clone the repo
2. Open a terminal in vsCode and CD to the tiller (vue) directory
3. npm install
4. npm run serve

The site will go through the build process and will then echo back what ip address and port the app is running on e.g.

App running at:
  - Local:   http://localhost:8080/ 
  - Network: http://192.168.1.129:8080/

Navigate to the URL to load the page.



## Usage

Original




Redesign

At the moment the redesign focuses on layout without any functionality.