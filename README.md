# Tutorial Mod

This is a Content Patcher compatible mod for the game Stardew Valley.  It's intended to help introduce players to the modifying the game Stardew Valley by creating an event with a dialogue between Kent and Vincent.  


## Getting Started

First thing is first.  We want to run the mod to see what we're working with.

 1. Make sure you have [SMAPI for developers](https://github.com/Pathoschild/SMAPI/releases/download/3.5/SMAPI-3.5.0-installer-for-developers.zip) and Content Patcher Installed. The Dev SMAPI has the more verbose console and lets us debug our mods.
 2. Download this repository as a zip and unpack it to a working directory on your Hard Drive.  *If you can fork and create a local repo, more power to you, but this tutorial assumes you haven't worked with software version control.*
 3. Within the folder you'll have a zip file called [CP] Hannah Mod.  This is the actual packaged mod.  Unzip this to your Stardew Valley Mods folder.  *Something like C:\Program Files (x86)\Steam\steamapps\common\Stardew Valley\Mods*
 4. Create a new save file.  We'll be doing some stuff that will break the game a bit when testing, so you don't really want to mess up that year 5 iridium ancient fruit wine setup that's raking in oodles of g.
 5. You may need to go into town and have a conversation with Vincent to register him as a character.  After that type the following commands into the SMAPI console window and hit enter after each command:
	 1. debug day 28
	 2. debug season winter
6. Go to bed for the night.
7. When you wake up on Spring 1, Year 2, kent will be at your door.  Click through his dialogue and then enter the following commands into the SMAPI console window:
	1. debug friend Vincent 1000
	2. debug friend Kent 1000
	3. debug time 1200
8.  This will get you to the 4 hearts you need with both of them to trigger the event and set the time of day to noon which is the earliest the event will fire.
9.   Walk to town via the bus stop and watch the exchange between father and son.     
10. Close out SDV, don't save or go to bed. 

## Writing your own dialogue
You're going to want to open up a text editor of your choice, but I recommend one that's designed for programming, especially [Visual Studio Code from Microsoft](https://code.visualstudio.com/).  It'll let you know if you have any file breaking issues like missing braces, but won't necessarily debug your code.
When you get that downloaded, go ahead and open the content.json and manifest json files in your working directory.  You can edit directly in your modding directory, but I tend to keep the WIP files seperate from active mod files as not to inadvertantly crash the game.  

Reading JSON Tip:
Everything inside braces is an object (think of it as a box)
Everything inside brackets is an array of things (think of it as a collection of like things)
Everything has Key : Value pairs.  Everything in front of the colon is a Key and it's how the program looks up a piece of data, everything after the colon is the value and it can be a word, a number, a boolean condition (true or false) another object { } or an array [ ].  

**manifest.json**
This contains all the mod definitions.  Most of this is pretty self explanitory.  If you want a better description of each of these fields, see the [Stardew Valley Wiki on Manifest Files](https://stardewvalleywiki.com/Modding:Modder_Guide/APIs/Manifest)  You won't have to modify anything in here until you're ready to upload your mod.

**content.json**  This is the meat and potatoes of a content patcher mod.  You can read more about how Content Patcher works on Pathoschild's Git, but the short version of this file, is we're going to edit the events that happen in town and add an event. In particular, we have one EditData action and one entry associated with this action.  Everything to the left of the colon in the key is the conditions which trigger the event.  Everything to the right is the individual instructions that comprise the event.  Each instruction is separated by a slash "/" 

Don't worry about the commands like pause or emote.  We'll get to that at a later point.  Right now just find all the ones that have the format: /speak \<NPC\> \\"Some Dialogue\\"/  There should be 11 in the starter example.  Visual Studio Code has a good find/replace function that you can activate by pressing Ctrl+F on the keyboard and just typing in "speak."  Go ahead and fill in the dialogue with the story that you've written.  The portraits, emotes, and movements probably won't fit, but we can tweak that as you refine the mod.

Save your content.json file in your working directory, and then replace the content.json file in your mod directory with the modified content.json from your working directory.  Go ahead and fire up SDV and use the save we created earlier.  You'll have to go through the intro with Kent and enter the debug commands to get 4 hearts and time warp to noon again before you head into town and watch the changes you've made take place.

## Tweaking the portraits, emotes, and movements
I won't go into too much detail now, but if you make it this far and want to dive in more, the Stardew Valley Wikki modding guide has two great resources:
[Modding Dialogue](https://stardewvalleywiki.com/Modding:Dialogue) - this will help understand the structure of conversations and how to change the portraits.
[Modding Events](https://stardewvalleywiki.com/Modding:Event_data) - this gives you the complete library of commands you can use and explains things like emote and jump 
