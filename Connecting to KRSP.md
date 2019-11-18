# How to connect to the KRSP database using R and RStudio

## REMINDERS:
* Username and password information should never be contained within your code.
* You should not downlaod a local instance of the database, but instead your code should pull directly from the cloud instance of the database.


## Old System
We used to connect to the database by creating a cnf file, storing it on your computer and using the krsp_connect function in the krsp package.
For instructions on this see [here](https://github.com/KluaneRedSquirrelProject/krsp/blob/master/vignettes/mysql-aws.md#r)
```r
krsp_connect(group="krsp-aws")
```

There is currently a KNOWN PROBLEM associated with this approach that seems to be cuased by particular operating systems (i.e. not a problem with the database, KRSP package, RStudio, etc.).

## New Solution

This is now the *preferred* method of connection.  See https://db.rstudio.com/best-practices/managing-credentials/ for more details.
1. Create a file (i.e. in RStudio File>NewFile>Text File) with the following:
```r
krsp_user = "xxx"
krsp_password = "XXX"
```
Replace xxx with your username and password as provided by McAdam.

2. Save this file as ".Renviron" in your home directory.  When asked whether you want to save a file that begins with ".", say "yes"

3. Restart R

Now your krsp user name and password are saved in your system settings.

Be sure to NEVER publish your .Renviron file, or commit this file to GitHub or your username and password will be compromised.

Now you can use code such as the following to connect to the krsp database:
```r
con <- krsp_connect (host = "krsp.cepb5cjvqban.us-east-2.rds.amazonaws.com",
                     dbname ="krsp",
                     username = Sys.getenv("krsp_user"),
                     password = Sys.getenv("krsp_password")
)
```
NOTE that in the future I will convert all of the krsp functions so they look in your system settings for your username and password, rather than the interactive input of username and password, which is tendious.


## Other Possible Work-Arounds (not preferred):
1. Use Mac Keychain
```r
install.packages("keyring")
library (keyring)
krsp_connect (host = "krsp.cepb5cjvqban.us-east-2.rds.amazonaws.com",
                    dbname ="krsp",
                    user="xxxxxxx",
                    password = keyring::key_get("krsp")
)
```
This code looks for an application password in Keychain on a Mac computer called krsp, which contains your password.  This Mac Keychain work-around now seems to also no longer be working.

2.  Use askForPassword in R Studio.
```r                     
krsp_connect (host = "krsp.cepb5cjvqban.us-east-2.rds.amazonaws.com",
                     dbname ="krsp",
                     username = rstudioapi::showPrompt(title = "Username", message = "Username", default = ""),
                     password = rstudioapi::askForPassword("Password")
)
```
         
This will result in a pop-up box in RStudio that will ask the user to input their username and password at this place in the code.  This is a good work-around and what McAdam currently uses.  The downside of this is that Rmd files will not knit to PDF, etc. when interrupted by this sort of interactive interface.


##  krsp versus krsp2019
Note that in any connection to the database the user can connect to the long-term database (e.g. `krsp`) or the cloud version of the annual database (e.g. `krsp2019`), which McAdam updates as data dumps are sent from the Yukon.  Users are tyoically given access to both the long-term database and the annual database in their priviledges.  To connect to the annual databsae simply replace the name of the database (e.g. `krsp2019`) for `krsp` in the code.
