# FIESTA 3.7.2

- Fixed estimate in denominator for esttype = 'RATIO' when the rowvar or colvar is from 
  the tree table (e.g. SPCD).
- Added modGBp2veg to generate estimates for FIA understory vegetation.



# FIESTA 3.7.0

- Overhaul of data summaries to SQL queries to improve efficiency with database inputs.
- Cleaned up code easier reading.
- Created new options in table_options parameter to classify row and/or column variables 
  for estimation (row.classify/col.classify).
- Added database_opts to mod_pop functions to access databases, such as postgreSQL.
- Added dbconn to most functions to allow input of an open database connection.
- Added returndata parameter in mod_pop functions with default as TRUE. If returndata = FALSE,
  and the input data is a database, only queries are returned and passed to estimation functions. 
  The objective is to minimize storing large objects in R memory.
- Fixed process for combining strata and estimation units (See help).

- Created several new parameters in datSum functions (See help for more details):
    datSum_opts - to group parameters with options that are not commonly used.
    woodland - to filter for woodland trees.
    bydomainlst - to sum tree data by domain variables (e.g., SPCD).
    domclassify - to classify domain variables.
    tderive - to derive new variables fro data tables.
    pltidsWITHqry - to filter queries using a WITH query.
    database_opts - to access databases such as postgreSQL.

- Updated vignettes.



# FIESTA 3.6.0

- Added National Volume and Biomass capability


# FIESTA 3.5.0

- fixed functions for accessing new CSV files on FIA Datamart.
- grouped parameters in DBgetPlots and spGetPlots for database layer names (dbTables)
- grouped parameters in the following functions for database evaluation selection, with no change in defaults.
  DBgetPlots, DBgetXY, spGetPlots, spGetXY (xy_opts, dbTabs, eval_opts) 


# FIESTA 3.4.1 

- added function to change class of columns if integer64 or IDate
    if integer64 and columns in(CN,PLT_CN,PREV_PLT_CN) - change to character
    	else, change to numeric
    if IDate, change to character
- fixed bug in DBgetPlots - when using strata from SQLite databases
- added functionality to DBgetStrata to get data from SQLite database
- allow spGetAuxiliary to output unitarea with no input rasters
- added database inputs to datSum* functions.
- spGetPlots - added returndata=FALSE, if exporting to database
- spGetXY - fixed bug when getting INTENSITY=1 plots using CSV files
- datSumTree/datSumTreeDom - changed default rounding from 16 to 5
- spGetSAdoms - added new parameter (byeach) to create SAdoms for each smallbnd
- spGetSAdoms - added new parameter (saveobj) to save object
- added SQLite database for Rhode Island to external data, with example in GB vignette


# FIESTA 3.0.30 

- created anGetData(), to deprecate (anSAdata, anGBdata, anMAdata)
- removed anSApop_ecomap()
- removed anSApop_RAVG()


# FIESTA 3.0.29 

added new function, spGetXY(), to clip XY coordinates before getting plot data.
this function returns spatial sf points (if returnxy=TRUE) or a non-spatial data frame 
	of xy plot identifiers and state information. 
the function is run within spGetPlot() or independently, with intent to separate 
	spatial and non-spatial processes.

spGetPlots 
	added parameter, xy_datsource, to identify datsource of xy data
	changed xy.joinid to xyjoinid
 



# FIESTA 3.0.28 

added functionality for P2VEG adjustment factors in modGBpop()
added new function to calculate P2VEG estimates - modGBp2veg()
added new parameter in datSumTree() and datSumTreeDom() to give flexibility 
	name of adjustment factor, tadjvar, with default="tadjfac"

spGetStrata()/spGetEstUnit()
changed keepxy parameter to returnxy

Deprecated:
spGetModeldat() 
changed to spGetAuxiliary()





# FIESTA 3.0.27 

added anSApop_report() function 
removed checks for sf and rgdal package in installed.packages
changed installed.packages(.Library) to installed.packages() to check for suggests packages
and changed from stop to message when a package does not exist


# FIESTA 3.0.26

changed estimation rawdata output names
unit.rowest to unit_rowest
unit.colest to unit_colest
unit.totest to unit_totest
unit.grpest to unit_grpest


# FIESTA 3.0.25

DBgetPlots()
- add functionality to access sqlite database from DataMart.

modGBpop()
- fix bugs in strata collapsing function



# FIESTA 3.0.23

Model-assisted
- added ratio estimators
- added intensity = modMApop()



# FIESTA 3.0.21 

Fixed bug in spGetStrata when using more than one NODATA value.

Added ability to output results in metric units.
- Added a column to FIESTAutils::ref_estvar, named METRIC, to identify metric units.
- Added a reference table (FIESTA::ref_conversion) to get conversion factors.
- Added a logical parameter, metric (TRUE/FALSE) to datSumTree and datSumTreeDom functions 
	to define output units as English or metric. 
- Added a parameter, areaunits to mod*pop functions to define the units of areavar in unitarea.
- Added a logical parameter, metric (TRUE/FALSE) to mod* functions, to define desired output units as 
	English or metric.
- All mod* functions return areaunits and estunits.

Variable changes in modPBpop and modPB functions
pnt to pntdat
plt.nonsamp.filter to nonsamp.pfilter
pnt.nonsamp.filter to nonsamp.pntfilter
plt.filter to pfilter
pnt.filter to pntfilter


# FIESTA 3.0.20

Fixes bugs in spGetStrata()
if you are using a raster and you already have a variable named STRATUMCD in your data table,
it will now create add make sure the name is not duplicated by adding _1 or _2, etc.\cr
Specified rast.NODATA values were not carried through to plot assignments, but this is fixed.\cr
The NAlst was not returned when keepNA=TRUE, but also fixed.

All overwrite parameters were made into 2 parameter (overwrite_dsn, overwrite_layer) for
overwriting dsn versus overwriting layer in dsn or file (e.g., shp, csv) in outfolder.


spGetPlots()
Changed output names from for consistency when clipxy=TRUE and clipxy=FALSE.
clip_polyv to bndx
clip_tabs to tabs
tabs$clip_* to tabs$*
clip_xyplt to xypltx

Combined pfilter and cfilter into pcfilter



# FIESTA 3.0.13

This release contains updates for core functions and Green Book (GB), Model-Assisted (MA), and Photo-Based (PB) modules. There are also several additional analysis functions for streamlining routines and generating core tables of estimates and core reports.

Next priorities include: (1) updating SA module; (2) adding to core tables and reports; (3) on-the-fly estimation for Growth/Removal/Mortality (GRM), P2 vegetation, and Change; (4) and continued documentation.

1. Changed plt.filter to pfilter
2. Changed cond.filter to cfilter



# FIESTA 3.0.0

1. Removed default connection to Oracle database (creating FIESTAO for FIA use only)

2. Removed RODBC from package Suggests (in DESCRIPTION file)

3. Added capability of writing tables and spatial layers to a SQLite database or geopackage,
	or geodatabase (if arcgisbinding package is installed).

3. Converted sp* functions from using class Spatial* to class sf objects.

4. Switched input of spatial object to dsn instead of layer and switched order of parameters.

4. Changed name of spReprojectSpatial function to spReprojectVector.

5. Changed pltstrat to pltassgn


Changes to functions:
spMakeSpatialPoints 
	- changed parameters: x to xvar; y to yvar
	- removed parameters: EPSGCD and prj4str
	- added parameter: crs (for EPSG or PROJ.4 string inputs) 

DBgetPlots - 
	- spconddat 	- plot-level, condition data (for displaying condition attributes)
	- spxy		- spatial xy coordinates (PLT_CN, x, y)




# FIESTA 2.4.2

1. Changed Oracle database connections and queries from using RODBC package to DBI. 
	DBI package is more versatile for querying Oracle and spatial databases.

2. Added sf package to list in anticipation to use for vector spatial manipulations.

3. Fixed bugs in anGBest_core()



# FIESTA 2.4.1 

1. Model-Assisted estimation module is functioning similar to Green-Book Module,
	with similar format of output.


# FIESTA 2.4.0 

Changes:

1. Added 2 new packages in Suggests 
DBI, RSQLite

2. Changed all input parameters of vector spatial files from 1 parameter to 2 parameters
This change will allow flexibility for different inputs of vector layers. The past options were only for shapefiles or objects. Now we can use options such as GeoPackages or SQLite databases.
