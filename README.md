# Groovy Liquibase
A pluggable parser for [Liquibase](http://liquibase.org) that allows the creation of changelogs in a Groovy DSL, rather than hurtful XML. If this DSL isn't reason enough to adopt Liquibase, then there is no hope for you.

The DSL syntax is intended to mirror the Liquibase XML syntax directly, such that mapping elements and attributes from the Liquibase documentation to Groovy builder syntax will result in a valid changelog. Hence this DSL is not documented separately from the Liquibase XML format.

## News
*Note:* Version 1.0.0 of this DSL uses Liquibase 3 instead of Liquibase 2.
Before upgrading, we strongly recommend the following procedure for upgrading:

 1. Make sure all databases are up to date using the older version of the
    DSL by running an update on all databases.

 2. Create a new, throw away database and use the new DSL to run all of yor
    change sets. on the new database.  This is because Liquibase 3 introduces
    some subtle differences in the way SQL is generated.  For example, adding a
    default value to a boolean column in MySql using ```defaultValue: "0"```
    worked fine in Liquibase 2, but in Liquibase 3, it generates invalid SQL.
    ```defaultValueNumeric: 0``` needs to be used instead.
 3. When you are sure all the change sets are correct for Liquibase 3, clear
    all checksums calculated by Liquibase 2 by using the ```clearChecksums```
    command in all databases.

 4. Finally, run a ```changeLogSync``` on all databases to calculate new
    checksums.


## License
This code is released under the Apache Public License 2.0, just like Liquibase 2.0.

## TODOs

 * Support for the customChange. Using groovy code, liquibase changes and database SQL in a changeSet.
 * Support for the [property tag](http://www.liquibase.org/manual/changelog_parameters).
 * Support for extensions. modifyColumn is probably a good place to start.
 * Proper testing of validCheckSum under changeSet. It's implemented, but I have not tested it properly.
 * Support for comments in a sql change.
