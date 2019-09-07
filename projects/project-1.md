---
layout: project
type: project
image: images/honolulu_seal.png
title: Pookela
permalink: projects/pookela
# All dates must be YYYY-MM-DD format!
date: 2019-07-31
labels:
  - Python
  - ArcGIS
  - Automation
summary: Developed a Python script to detect location and time conflicts of city projects/events and automatically email project organizers.
---

<div class="ui small rounded images">
  <img class="ui image" src="../images/ArcGIS_logo.png">
  <img class="ui image" src="../images/honolulu_seal.png">
  <img class="ui image" src="../images/esri.jpg">
</div>

The City and County of Honolulu's Pookela Internship program places college students in various departments within the city government and pair those students with several mentors within that department.  
As part of the City and County of Honolulu's Pookela internship program, I worked on several projects to use Python automation to improve the planning of projects and events for the various departments within the city government.

For this project, I was the lead programmer who was responsible for programming the various capabilities of the mouse.  I started by programming the basics, such as sensor polling and motor actuation using interrupts.  From there, I then programmed the basic PD controls for the motors of the mouse.  The PD control the drive so that the mouse would stay centered while traversing the maze and keep the mouse driving straight.  I also programmed basic algorithms used to solve the maze such as a right wall hugger and a left wall hugger algorithm.  From there I worked on a flood-fill algorithm to help the mouse track where it is in the maze, and to map the route it takes.  We finished with the fastest mouse who finished the maze within our college.

I am legally not allowed to provide the code as it is property of the City and County of Honolulu. The following is an example of how Python was used with [ArcGIS](https://pro.arcgis.com/en/pro-app/tool-reference/analysis/spatial-join.htm).

```py
# Import system modules
import arcpy
import os

# Set local variables
workspace = r"C:\gpqa\mytools\spatialjoin\usa.gdb"
outWorkspace = r"C:\gpqa\mytools\spatialjoin\output.gdb"
 
# Want to join USA cities to states and calculate the mean city population
# for each state
targetFeatures = os.path.join(workspace, "states")
joinFeatures = os.path.join(workspace, "cities")
 
# Output will be the target features, states, with a mean city population field (mcp)
outfc = os.path.join(outWorkspace, "states_mcp2")
 
# Create a new fieldmappings and add the two input feature classes.
fieldmappings = arcpy.FieldMappings()
fieldmappings.addTable(targetFeatures)
fieldmappings.addTable(joinFeatures)
 
# First get the POP1990 fieldmap. POP1990 is a field in the cities feature class.
# The output will have the states with the attributes of the cities. Setting the
# field's merge rule to mean will aggregate the values for all of the cities for
# each state into an average value. The field is also renamed to be more appropriate
# for the output.
pop1990FieldIndex = fieldmappings.findFieldMapIndex("POP1990")
fieldmap = fieldmappings.getFieldMap(pop1990FieldIndex)
 
# Get the output field's properties as a field object
field = fieldmap.outputField
 
# Rename the field and pass the updated field object back into the field map
field.name = "mean_city_pop"
field.aliasName = "mean_city_pop"
fieldmap.outputField = field
 
# Set the merge rule to mean and then replace the old fieldmap in the mappings object
# with the updated one
fieldmap.mergeRule = "mean"
fieldmappings.replaceFieldMap(pop1990FieldIndex, fieldmap)
 
# Delete fields that are no longer applicable, such as city CITY_NAME and CITY_FIPS
# as only the first value will be used by default
x = fieldmappings.findFieldMapIndex("CITY_NAME")
fieldmappings.removeFieldMap(x)
y = fieldmappings.findFieldMapIndex("CITY_FIPS")
fieldmappings.removeFieldMap(y)
 
#Run the Spatial Join tool, using the defaults for the join operation and join type
arcpy.SpatialJoin_analysis(targetFeatures, joinFeatures, outfc, "#", "#", fieldmappings)
```

Please visit the [Pookela Program Website](https://www.honolulu.gov/hr/pookela.html) for more details.



