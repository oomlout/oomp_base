#oomp_base

## What is OOMP?
OOMP is the Oopen Organization Method For Parts.  

It's an attempt to create a taxonomy for parts to make naming and referencing them possible.  

The idea is to give every part a full name which is immutable, similar to the way plants are given latin names.  

Once parts can be named the hope is it will be easier to store and share resources about that part such as images, drawings, labels etc.  

The initial focus is on electronic components and fasteners.  

## How is OOMP organized

### Repos
This is tricky.  

The hope is for OOMP to be flexible enough for many people to use, and for each persons OOMP to have the ability to include the parts that are important to them.

At the moment it's just me so it's parts that are important to me which is basic electronic components (resistors and capacitors) and smaller fasteners and fixings.

However I wanted to structure it in a way that could grow, so heres the current structure.

Note: The repos that prepend oomlout to their name are there as examples of our amatuer implementation of that stage, the ones without are envisioned to serve as source data.

#### This one
This repo only contains this readme to describe other repos.

#### The Dirty
* https://github.com/oomlout/oomlout_oomp_part_src  
This is my monolithic repo that includes all the parts I've defined as well as images, labels, scripts, and experiments. If you just want a specific file and don't mind a proper mess clone this and find what you are after. The code in it will be completly unusable on anyone elses computer. 

#### The Segmented
Ultimately I'd like OOMP to have a foundation that can have details controlled and monitored with revision control. To enable this I've setup some segmented repos. These are currently sanitized versions of my own repo. I split them in ways that I think might be useful to others. 

##### Parts data
These contain parts data in yaml and json format, segmented into class.
* https://github.com/oomlout/oomp_base_electronic
* https://github.com/oomlout/oomp_base_hardware
* https://github.com/oomlout/oomp_base_oobb
* https://github.com/oomlout/oomp_base_packaging

##### Image data
These contain the images for parts.
* https://github.com/oomlout/oomp_base_electronic_image
* https://github.com/oomlout/oomp_base_hardware_image
* https://github.com/oomlout/oomp_base_oobb_image
* https://github.com/oomlout/oomp_base_packaging_image


##### Three D Models
These contain the three d models for parts
* https://github.com/oomlout/oomp_base_electronic_three_d_model
* https://github.com/oomlout/oomp_base_hardware_three_d_model
* https://github.com/oomlout/oomp_base_oobb_three_d_model
* https://github.com/oomlout/oomp_base_packaging_three_d_model

##### Drawings
These contain any relevant drawing files for parts
* https://github.com/oomlout/oomp_base_electronic_drawing
* https://github.com/oomlout/oomp_base_hardware_drawing
* https://github.com/oomlout/oomp_base_oobb_drawing
* https://github.com/oomlout/oomp_base_packaging_drawing

##### Datasheet
These contain datasheets
* https://github.com/oomlout/oomp_base_electronic_datasheet
* https://github.com/oomlout/oomp_base_hardware_datasheet
* https://github.com/oomlout/oomp_base_oobb_datasheet
* https://github.com/oomlout/oomp_base_packaging_datasheet

#### Data Injectors
A data injector has a yaml file in the data directory. These are loaded and all extra details are added to the working.yaml file

##### Distributor Part Numbers
https://github.com/oomlout/oomlout_oomp_data_injector_distributor_part_numbers  
Inserts some select distributor part numbers.  
##### Bolt Part Numbers  
https://github.com/oomlout/oomlout_oomp_data_injector_bolt_part_numbers  
Part numbers for sourcing m3 nuts and bolts in the uk, currently just orbital fasteners, example of spreadsheet, to csv to yaml pipeline.  




#### The Builder
This builds your oomp. It takes a list of repos pulls them and puts all the parts folder into one folder. Currently also has a utility to load the yamls from all directories into a single pickle/yaml file, and one for creating links to make navigating using shorter codes possible.

* https://github.com/oomlout/oomlout_oomp_builder
  * Works within code space

#### Utilities
As each parts data and source files are standardized it is possible to write utilities to do things like generate summary pages or   labels

##### Basic Codes
https://github.com/oomlout/oomlout_oomp_utility_basic_code
Generates a set of basic codes. 
* converts the ID to a name
* generates name and id subsets removing various categories
* generates an md5 hash and adds subsets of it
* adds oomp moji

##### Label Generation
https://github.com/oomlout/oomlout_oomp_utility_label_generation  
Generates labels using a template for each part

##### Navigation Generation
https://github.com/oomlout/oomlout_oomp_utility_navigation_generation
Generates a navigation folder divided by name hierarchy

##### Oomlout Project Bolt
github.com/oomlout/oomlout_oomp_utility_oomlout_project_bolt
Adds the neccesary attributes for project bolt labels

##### Oomlout Short Code
https://github.com/oomlout/oomlout_oomp_utility_oomlout_short_code
Generates an oomlout short code for each item that has a coresponding set of rules

##### PDF From SVG Generation
https://github.com/oomlout/oomlout_oomp_utility_pdf_from_svg_generation
Generates a pdf for every svg file in an oomp folder

##### Readme Generation  
https://github.com/oomlout/oomlout_oomp_utility_readme_generation  
Generates a readme using a template for each part  

##### Working.yaml Remove
https://github.com/oomlout/oomlout_oomp_utility_working_yaml_remove
removes working.yaml to aid in generating a full version with no source working.yaml

#### Data 
Repositories that focus on adding data to parts.  

##### Part number  
* https://github.com/oomlout/oomlout_oomp_data_distributor_part_numbers_lcsc  



### Parts
Each part is a folder with its full name located in the parts/ folder with flat representation.  

This is cumbersome and not very useful.  

The thinking is create a flat base layer that is beyond easy to understand then allow that to be used to construct more useful structures based on an individuals need later.  

#### A Parts Name
Each parts name is a string of all lower case text any punctuation, such as decimals or dashes or spaces, is replaced with an underscore.  
  
Examples:  
* electronic_header_2_5_mm_jst_xh_9_pin_through_hole  
* hardware_screw_countersunk_3_mm_black_18_mm_hex  

This name is a concation of a hierarchical naming of each part.   

#### Files
##### Default Files
###### Base
* working.yaml This is all the part data as genereated by oomlout
* working.json This is working.yaml in json format
* base.yaml This is just the parts defining data that everything can be generated from. (classification, type, size,color, description_main, description_extra, manufacturer, part_number, id)
###### Image
* image.jpg .png An image of the part
* image_reference.jpg .png A reference image either next to a ruler or a size reference.
* drawing.png .pdf .svg A drawing of the part.
* dimension.png .pdf .svg  A dimensional drawing of the part

##### Classification
The class of the part.  
Examples:  
* electronics  
* hardware  

##### Type
The type of the part.  
Examples:  
* header  
* screw_countersunk  

##### Size
The size of the part.  
Examples:  
* 2_mm  
* 2_5_mm_jst_xh  

##### Color:
The color of the part.  
Examples:
* black

##### Description_Main
The main way of describing this part.  
Examples:  
* 9_pin  
* 18_mm  

##### Description_Extra  
An extra way to describe the part. 
Examples:  
* hex
* through_hole

##### Manufacturer
The manufacturer of the part.

##### Part_Number  
The manufacturers part number.



 
