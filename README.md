# Using-the-KRSP-Cloud-Database
Instructions for getting set-up to use the KRSP database from the cloud instance.

This repository is designed to provide you with information on how to get up and running using the cloud instance of the KRSP database.
We have written an R package that will be helpful for you for accessing and using the database.  You can download it using:

```r
install.packages("devtools")
devtools::install_github("KluaneRedSquirrelProject/krsp")
```

More information on getting set-up with the database can be found [here](https://github.com/KluaneRedSquirrelProject/krsp/blob/master/vignettes/mysql-aws.md)


## Best Practices:
1.  Everyone needs their own username and password.  It would be inappropriate to share your username and password with anyone.  Have them contact me for access to the database.

2.  Your username and password should never be contained within your code.

3.  Every year we identify and correct many errors in the database.  As a database user, it is essential that you track all errors that you find in the database and communicate them [here](https://github.com/KluaneRedSquirrelProject/KRSP-Database-Errors/issues)

4.  You should NOT download a copy of the databse to your local computer and work from that.  You should instead write your code to pull directly from the cloud instance of the database.  This ensures that all code is completely transferrable to others and prevents any accidental changes to local instances of the database.



