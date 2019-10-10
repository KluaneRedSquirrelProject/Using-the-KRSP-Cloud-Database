#How to connect to the KRSP database using R and RStudio

##REMINDERS:
Username and password information should never be contained within your code.
You should not downlaod a local instance of the database, but instead your code should pull directly from the cloud instance of the database.


The preferred method to connect to the database is by creating a cnf file, storing it on your computer and using the krsp_connect function in the krsp package.
For instructions on this see here: https://github.com/KluaneRedSquirrelProject/krsp/blob/master/vignettes/mysql-aws.md#r

##Preferred Connection:
krsp_connect(group="krsp-aws")

There is currently a KNOWN PROBLEM associated with this approach that seems to be cuased by particular operating systems (i.e. not a problem with the database, KRSP package, RStudio, etc.).

##Possible Work-Arounds:
1. Use Mac Keychain

This Mac Keychain work-around now seems to also no longer be working.

2.  Use askForPassword in R Studio.
krsp_connect (host = "krsp.cepb5cjvqban.us-east-2.rds.amazonaws.com",
                     dbname ="krsp",
                     user= rstudioapi::askForPassword("Username"),
                     password = rstudioapi::askForPassword("Password"))
         
This will result in a pop-up box in RStudio that will ask the user to input their username and password at this place in the code.  This is a good work-around and what McAdam currently uses.  The downside of this is that Rmd files will not knit to PDF, etc. when interrupted by this sort of interactive interface.

