# TileMapper (Proof of Concept)
Please note this is a rough proof of concept that was used to generate the maps needed for a game that I was porting to the web.  The functionality is far from complete including its usability.  Many of the options available to the options bar do not work.  Further work is planed to complete the project.

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

To load the index htm it needs to be accessed from a web-server due to access to the layout image so you will need to run from a simple http server such as using the a one liner from a terminal such as:

$ python -m SimpleHTTPServer 8000

Obviously this will need python installed.

$ sudo apt install python

Other http servers that can be run from a terminal with a single line can be found at https://gist.github.com/willurd/5720255

1. Clone the repo 
2. Open a terminal and cd to the project directory 
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
There are two parts to producing a tile set.  Producing the tiles themselves and creating the map for postitioning the tiles to make up the map itself.

When the application opens the predefined map will load and will be sectioned into tiles. Each tile is checked for a duplicate in tile collection array by creating a checksum of the pixel data.  If no duplicate is found then an index is assigned to the tile, added to the collection and a map is updated noting the tiles location and the index to use.  If the title is found in the collection then it discarded and the index of the found tile is used
The tiles will appear in the bottom left hand corner.  This will be used as the tile set file for you to include into your games.

Additional tiles can be merged to create an updated map with less indexes and a smaller tile collection by selecting a section of the map and then ctrl clicking other sections.  Clicking the merge button will allow the tiles to be merged.  Clicking the rebuild will rebuild both the tile collection and the map.  

To download the map and tile set click on the download button on the far right and copy the content of the textarea.

Redesign

At the moment the redesign focuses on layout without any functionality.