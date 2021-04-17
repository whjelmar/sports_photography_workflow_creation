[![Code Coverage Status](https://codecov.io/gh/whjelmar/sports_photography_workflow_creation/branch/master/graph/badge.svg)](https://codecov.io/github/whjelmar/sports_photography_workflow_creation?branch=main)
[![lifecycle](https://img.shields.io/badge/lifecycle-EXPERIMENTAL-orange)](https://www.tidyverse.org/lifecycle/#experimental)
[![lifecycle](https://img.shields.io/github/issues/whjelmar/sports_photography_workflow_creation)](https://img.shields.io/github/issues/whjelmar/sports_photography_workflow_creation)

# My sports photography workflow - 2021-04-14

## Beginning a new season

### Create a new season directory

The root file path for baseball photos should be under F:\__Baseball.

Create a new directory of the form {4 digit year} - {season} - {team name} - {age specifier (14U, Freshman, etc.)}

### Create the code replacement file for the team

Photo Mechanic, a program that will be used as a strategic part of this workflow, has a function called code replacement allows for systematic text replacement to ease the process of syncing the meta-data on your photos.  Code replacement uses a tab-delimited file (TSV) to transform codes like y7#2 into "New York Yankees's Leftfielder, Mickey Mantle (#7)"

Here are a list of good YouTube referesher tutorials on the code replacement function:

  - https://www.youtube.com/watch?v=fg00PF_F2GY - initial video is on the variable and ingestion process, code replacement information begins at the 13:33 mark, but good all around video on the workflow.
  - https://www.youtube.com/watch?v=INrouhWiH_w

Create a tab-delimited file with the following field structure:

  - jersey number
  - first name
  - last name
  - full name
  
**Be sure to save the file as a tab delimited file** in the season directory that you just created.
  
Run the create_roster_code_replacement.R script located in F:\__Baseball, this will prompt you to select the tab-delimited file that you just created.  This R script will create a file located in the same directory as your roster file, that we can use as short cuts when we create out captions and other meta-data in the photo files.

Start up Photo Mechanic, if not already running, and hit **Control-Alt-C** or from the menus select **Edit -> Settings -> Set Code Replacements**. In the resulting dialog box, add the newly created season code replacement file, and remove any unnecessary files from the list.
  

### Create the default IPTC template for the team

Start up Photo Mechanic, if not already running, and hit **Control-I** or from the menus select **Image -> Metadata (IPTC) Template...**. This will pop up a dialog box, containing all of the parameters that will be written to the XMP file when the **Control-Shift-I** or from the menus select **Image -> Apply Metadata (IPTC) Template to Photos** is selected.

At the bottom of the dialog box, click on the **Load...** button and load the file f:\__Baseball\default_IPTC_metadata_template.XMP.

This should be a good starting point to customize the file for this specific season.  From here you need to add / change the following data fields:
  - Change the default **Keywords** to be: baseball, {year4}, spring, {featuredorgname}, {event} - __obviously spring should be the name of the actual season that your are playing__
  - Add the name of the team to the **Featured Org. Name** field: e.g. 2021 New York Yankees - AAA team
  - select the **Seqn...** button and hit **reset** to set the starting number back to 001
  - Change **Event** to  "{featuredorgname} vs "
  - Change **State/Province** to "CT"
  - Change **Country** to US
  - **Title/Object Name** to "{filename}"
  - Verify that the image attribution and copywrite information is correct
  - Verify that the contact information is correct
  

Save the template as default_IPTC_metadata_template.XMP, in your season directory.

TODO: This is a text file so we should just be able to create it with the defaults that we want.


Here are a list of good YouTube referesher tutorials on the IPTC template function:

  - https://www.youtube.com/watch?v=fg00PF_F2GY - This is the first part of the video listed above


### Match the labels in Photo Mechanic and Lightroom

In order to ensure that the meta transfer between Photo Mechanic and Lightroom works well, you will need to match the color labels set in the two programs.  This is something that you probably won't need to change often, but it good to check that it matches as the beginning of each new season to ensure that you didn't use them for another purpose since the ending of the previous season.  The color mapping that we will use is:

  - Red - Lots of edits required on a photo that with nice composition
  - Yellow - Some light cropping needed
  - Green - Files ready to print
  - Blue - Unknown as to whether I want to keep it or not
  - Purple - Trash it
  
Here are a list of good YouTube refresher Photo Mechanic and Lightroom workflow:

  - https://www.youtube.com/watch?v=iO07PIIiRHM - the color labeling piece is at the 1:00 mark
  
### Ensure that the changes made in Lightroom are reflected in the XMP data

In Lightroom verify that you have selected the __Automatically write changes into XMP__ option in the __Catalog Settings__ preferences, to ensure that the changes that you make in Lightroom are represented in the .XMP sidecar file to ensure that Photo Mechanic can read the changes if you go back to it.  Things like the star-rating and color selections are important to replicate.  **WARNING** Lightroom does not always write changes to the XMP file immediately!** Sometimes this action can be delayed and you may want to make the changes manually or verify they have been written before moving on to a step that requires the latest information in the workflow.

Here is a YouTube refresher:

  - https://www.youtube.com/watch?v=iO07PIIiRHM - same as previous file this is at the 3:45 mark

### Ensure that you have the correct IPTC/XMP settings in Photo Mechanic

In the Photo Mechanic preferences (Edit -> Preferences) make sure that the following settings are set correctly:

  - When writing IPTC/XMP:

      - **For JPEG, TIDD, PSD, DNG photos**: Add embedded IPTC (XMP will always be written)
      
      - For TIFF-based RAW photos:
      
        - **Allow RAW files to be modified **: unchecked
        - **Add embedded metadata**: unchecked
        - **Always create and/or update XMP sidecar file**: checked (should be greyed out as it is the default with the above 3 options unchecked)
      
  - **Default IPTC Encoding**: Microsoft Latin1+Euro
  - **Write IPTC as Unicode**: unchecked
  - **IPTC Line endings**: CR (recommended)
  - **When viewing photos in RAW+JPEG mode use the metadata from the**: JPEG file
  - **For JPEGs with multiple IPTC records**:  Read/update the last one
  - Use a **comma** to separate repeating files (Keywords, Caption Writers, etc.) 
  - **Spell check text fields using the following system-provided dictionary**: checked and **en-US**
  - **When updating XMP, add Structure Keywords to hierachical keywords field only**: unchecked 
  - **Always use today's date in Metadata (IPTC) Template**: unchecked 
  - **Metadata (IPTC) Info Data and Time uses**: IPTC Data and Time

If you make changes to any of your preferences, please make a backup by clicking on the **Export** button and saving the resulting file in f:\__Baseball\PhotoMechanic_preferences_export\PM_Export_{year}{zero padded month}{zero padded day}.pmx, this should allow us to recreate the preferences as necessary.


Here is a YouTube refresher:

- https://www.youtube.com/watch?v=iO07PIIiRHM - same as previous file this is at the 6:15 mark


# Day of shooting

Snap away!

## Non-game shot check list

Here's an idea of some non-game related shots that we should try and capture at each event:

  - Warm ups
  - Infield / Outfield - this is a great opportunity to get action photos of individuals as you generally know exactly where the ball is going.  Prioritize getting Outfield first as the I/O generally ends for them first and they are align to their normal position stance; where as during the warm ups between innings they are throwing to each other and thus, not generally facing the normal direction that the position would dictate as infielders generally are in their normal position stance at this point, throwing the ball to first base
  - Line up exchanges
  - National anthem
  - Dugouts
  - Field wide shoots
    - Backstop
    - Catcher's view
    - Field dimensions
    - Flag poles
    - Score board
    - Light poles
    - Bullpens
    - Batter's box
    - Chalk lines
    - The flag
    - Sunsets??
  - Equipment
    - Catcher's gear
    - Baseballs
    - Helmets
    - Bats
    - Gloves
    - Cleats
    - Uniform close ups
  - Umpires
  - Coaches - especially when giving feedback / directing the team, either one-to-one or as a group
  - Players socializing
  - Announcer / Press box
  - Concession stand
  - Fans
  - Post game high 5s
  - Celebration
  - Coach's meeting
  - In between games of a double header - nice time to get pictures of them with their guards down just being kids and interacting with their friends.
  
## In game photo shot list

  - Starting pitchers should be a priority for the 1st Inning
  - Position players -- cheat by using infield / outfield and defensive inning warm ups to get key photos for position players
  - Each of the batters
    - Cleaning spikes
    - Settling into the batter's box
    - Anticipation of the pitch
    - Bat on ball
    - Follow through
  - Coach giving signs
  - Throw over to first
  - Catcher 
    - Giving signs -- difficult on most fields even with the 500mm
    - Blocking balls in the dirt
    - Throw down to 2b -- you can cheat this photo as by catching the throw down before "balls in" gets called at the start of each defensive inning
  - First Base
    - Holding a runner on
    - Throw over tag
    - Dive back to the back
    - Rounding the base for a double
  - Second Base / Shortstop
    - Turning double play
    - Stealing 2nd
    - Slide into 2nd
  - High 5s as players score or come back to the dugout - these player relationships moments end up being nice moments
  - Dugout photos
    - Players putting on / taking off equipment
      - Catcher getting the gear on
      - Putting on the batting gloves and helment
  
  

# Photo ingestion

## Create the IPTC information for the specific event

A lot of the work has already been prepped for you in the work we did setting up the season's IPTC information, but we will want to make our lives even more simpiler, but adjusting the IPTC template for each individual game.  We will be updating the information in the Event and Location pane.  Under the **Event and Location** section, make the following changes:

  - **Event** - this should be checked, from our earlier work, contain "{featuredorgname} vs " as a value.  Go ahead and flush that out with the opponent's team name, e.g.  "{featuredorgname} vs Boston Red Socks"
  - **Date** - leave this unchecked as we are using the date the photo was taken elsewhere; the only time you'd want to use this is if there was a problem with the in camera datestamp being incorrect.
  - **City** - the city in which the game was played
  - **Location** - the school or field name where the game was played
  - **State/Province** - the state in which the game was played (should already default to CT)
  - **Country** - I cannot forsee this ever not being "US", for my needs, but still...
  
The remaining fields can be left as is.  Now through the magic of variables, when you apply the template to a group of photos that you are ingesting, you get things like the Description/caption field of the photos containing " during the New York Yankees vs Boston Red Sox game at Yankee Stadium, Bronx, NYU, September 11, 2021. Photo: Walter Hjelmar"...Nice!  Now for individual photos all you need to do is pre-prend the player involved and you have a fully-formed rich photo caption that is stored in the XMP sidecard file and can be used in Lightroom or other programs, with minimal effort on your part.  Using the code replacement feature even the tagging of players to photos is easy and we'll do that in just a little bit.

## Ingest

**Control-G** or **File -> Ingest** from the menus will begin the ingestion process.

**Sources**: Disks, whichever you have shot on...duh...

Verify that the **Destination Folder Roots** are correct:
  
  - **Primary** should be set to the f:\__Baseball\{4 digit year} - {season} - {team name} - {age specifier (14U, Freshman, etc.)}
  - **Secondary** should be set to the NAS Appliance\home\{4 digit year} - {season} - {team name} - {age specifier (14U, Freshman, etc.)}
  
Filter Files:

  - **Copy Locked and Unlocked Photos**
  - **Copy RAW and non-RAW Photos**
  
**Appy Metadata Template to photos** should be checked
  - **Use Local Template** selected

**Rename Ingested photos as:** should be checked
  - {iptcyear4}{iptcmonth0}{iptcday0}_{event}_{seqn}
  - Sequence = 001
  
**Open contact sheets during ingest**  

**Source Directory Structure**:
  - preserve all source directories
  
**Copy Photos**:
  - into folder with name
  - **Folder Name**: {iptcyear4}{iptcmonth0}{iptcday0}_{event}

Click on **Metadata (IPTC) Template...** button and load the appropriate IPTC template.  Close the template and click on **Ingest**


## Set up the code replacement file in Photo Mechanic

Hit **Control-Alt-C** or from the menus select **Edit -> Settings -> Set Code Replacements**. In the resulting dialog box, verify that the season-base code replacement file is present, add the game specific one to the list (if required), and remove any previous game specific or otherwise unnecessary files from the list.


## Contact sheet triage

Notice how quick Photo Mechanic ingests photos?  Nice huh!

Now that you have a contact sheet showing all of the pictures that you've ingested, let's quickly go through and do a triage of the unusable shoots. Select the first photo and the preview window opens.  The zoom feature allows you to zoom in and check your focus on the shots. **Z** will toggle you back-and-forth between the selected zoomed in view and the original zoomed out look. The **T** key will allow you to **tag** certain shots. Use the **tag** feature to select allow the photos that do not have basic composition or focus issues, so that you know not to spend any time on the photos that are not **tagged**.  You can then also start rating your photos now, or wait to do a second pass and tag them afterwards.  You can use either the **color class** and/or the **star rating**.

The **color class** can be set either by right clicking on the photo and selecting **Color Class -> color selection** or by hitting **control 1-9** for the color that you want to flag it with.  The **star rating** is done using **Alt 1-5** or right clicking and selecting **Rating -> start rating**

**left and right arrow keys** will take you through the remaining photos in your contact list.  After you've decided whether or not you want to tag each shot, hit **escape** to get back to the contact sheet view.

In the contact view you can now filter to only displaying the **Tagged** photos.

If you have not selected the **color class** or **star rating** previously, now is the time to go back and do it.

## Individual File Captioning

We've done a lot of work already to set up our descriptions and other Metadata fields, but we still want to add information that is unique to __this particular photo__.  To do that we select the photo and either click on the button with the **i in a circle**, in the lower left corner of the particular picture on the contact sheet or hit **Control I** to bring back up the familar IPTC template window.  Assuming that you've followed along to date you should be 90% of the way there to having good metadata for the photo.  Now we will use **Code Replacement** to complete the remain 10%.  In the **Persons shown**: section, hit **\** the player's jersey number and **\** again.  This should immediately replace the \#\ with the full name of the player.  Hit enter and click on the **downward triangle** next to the field this should bring up a menu that asks if you want to add that players name to the list of values, add it and now, you have a pick list that you can select multiple players from to round out who else stars in this photo.

In the **Description/Caption**: field you should see " during the {event} game at {location}, {city}, {state}, {iptcmonthname}-{iptcday}, {iptcuear4}. {credit}".  Place your cursor before the space in front of "during" and type **\** the player's jersey number and the abbreviation for the position the player is currently playing in the photo (or b for batter) and **\**.  e.g. \7b\ would change the line to "Mickey Mantle (New York Yankees) at the plate during the ..."

Awesome!

You can hold the **Shift Key** and the **OK** button turns into an **Eval** button click it and all of the variables get filled in and you will be able to see what the final metadata for the photo looks like! __NOTE: You may need to apply it more than once to fill everything out as it does not alway recurse the way it should.__

Rise and repeat for the remaining pictures...this can take awhile, but the value is immense down the road, so don't despair.  __NOTE: You can select multiple photos that have a similar subject matter and fill out the metadata once and select **Apply Template to Selected** to cut down on the work.__


# Photo adjustments

## Bringing the photos into Lightroom

## Ensuring that Lightroom has the latest metadata

If we change the metadata outside of Lightroom to the metadata once the photos have been imported into Lightroom we can always do a **Control A** to select all of the photos and right click and go to **Metadata** and select **Read metadata from files**.  

## Writing metadata changes in Lightroom

If we change the metadata inside of Lightroom and we want to ensure that is written to the files we can always do a **Control A** to select all of the photos and right click and go to **Metadata** and select **Write metadata to files**.  


