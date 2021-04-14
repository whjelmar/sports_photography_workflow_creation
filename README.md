[![Code Coverage Status](https://codecov.io/gh/whjelmar/sports_photography_workflow_creation/branch/master/graph/badge.svg)](https://codecov.io/github/whjelmar/sports_photography_workflow_creation?branch=main)
[![lifecycle](https://img.shields.io/badge/lifecycle-EXPERIMENTAL-orange)](https://www.tidyverse.org/lifecycle/#experimental)
[![lifecycle](https://img.shields.io/github/issues/whjelmar/sports_photography_workflow_creation)](https://img.shields.io/github/issues/whjelmar/sports_photography_workflow_creation)

# My sports photography workflow - 2021-04-14

## Beginning a new season

### Create a new season directory

The root file path for baseball photos should be under {root_directory}.

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
  
** Be sure to save the file as a tab delimited file** in the season directory that you just created.
  
Run the create_roster_code_replacement.R script located in {root_directory}, this will prompt you to select the tab-delimited file that you just created.  This R script will create a file located in the same directory as your roster file, that we can use as short cuts when we create out captions and other meta-data in the photo files.

Start up Photo Mechanic, if not already running, and hit **Control-Alt-C** or from the menus select **Edit -> Settings -> Set Code Replacements**. In the resulting dialog box, add the newly created season code replacement file, and remove any unnecessary files from the list.
  

### create the default IPTC template for the team

Start up Photo Mechanic, if not already running, and hit **Control-I** or from the menus select **Image -> Metadata (IPTC) Template...**. This will pop up a dialog box, containing all of the parameters that will be written to the XMP file when the **Control-Shift-I** or from the menus select **Image -> Apply Metadata (IPTC) Template to Photos** is selected.

At the bottom of the dialog box, click on the **Load...** button and load the file {root_directory}\default_IPTC_metadata_template.XMP.

This should be a good starting point to customize the file for this specific season.  From here you need to add / change the following data fields:
  - Change the default **Keywords** to be: baseball, {year4}, spring, {featuredorgname} - __obviously spring should be the name of the actual season that your are playing__
  - Add the name of the team to the **Featured Org. Name** field: e.g. 2021 New York Yankees - Freshman team
  - select the **Seqn...** button and hit **reset** to set the starting number back to 001

Save the template as default_IPTC_metadata_template.XMP, in your season directory.

TODO: This is a text file so we should just be able to create it with the defaults that we want.


Here are a list of good YouTube referesher tutorials on the IPTC template function:

  - https://www.youtube.com/watch?v=fg00PF_F2GY - This is the first part of the video listed above


### Match the labels in Photo Mechanic and Lightroom

In order to ensure that the meta transfer between Photo Mechanic and Lightroom works well, you will need to match the color labels set in the two programs.  This is something that you probably won't need to change often, but it good to check that it matches as the beginning of each new season to ensure that you didn't use them for another purpose since the ending of the previous season.  The color mapping that we will use is:

  - Red - ???
  - Yellow - ???
  - Green - ???
  - Blue - ???
  - Purple - ???
  
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

If you make changes to any of your preferences, please make a backup by clicking on the **Export** button and saving the resulting file in {root_directory}\PhotoMechanic_preferences_export\PM_Export_{year}{zero padded month}{zero padded day}.pmx, this should allow us to recreate the preferences as necessary.


Here is a YouTube refresher:

- https://www.youtube.com/watch?v=iO07PIIiRHM - same as previous file this is at the 6:15 mark


# Day of shooting

# Photo ingestion

## Set up the code replacement file in Photo Mechanic

Hit **Control-Alt-C** or from the menus select **Edit -> Settings -> Set Code Replacements**. In the resulting dialog box, verify that the season-base code replacement file is present, add the game specific one to the list (if required), and remove any previous game specific or otherwise unnecessary files from the list.

# Photo Mechanic

