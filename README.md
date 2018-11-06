WE MOVIN TO TU-GITLAB CAUSE COPYRIGHT
====================================================================

https://gitlab.tubit.tu-berlin.de/stefankubisa/Muchos_Pejperos/blob/master/README.md

IZ HERE












# Muchos_Pejperos
Pejpers and Spalationz

Recommender System Creation: 
=============================================================

* Analyse receipts to determine who should get recommendations at all using decision tree induction because avoiding bad recommendations is nr1 priority, some don't need them, some hate inaccuracy 

* Analyse clickstream to determine individual prefference and probable products he might want to buy as well from known complementary goods pairs 

* Analyse product taxometry to recommend best sellers within customers interests and new products he might be aware of or willing to buy 

* Business efficient products out of result lot are chosen

[80/100]


Techlead - Let's do server maintenance (migration of a database server)
=============================================================
- **reason**: 
    1. company wants to get rid of all server in the area where Techlead's server is.
- **solution**:
    1. Get a new database server
    2. Setup the server: e.g. install DB software (here MySQL) 
    3. Migrate the data:
         1. **Problems**:
             - live database - all websites using the db server have to go offline before migration can start
             - data size - Techlead's DB weights ca. 500GB
             - copying technique - [*rsync*](https://en.wikipedia.org/wiki/Rsync)  vs *mysql dump*
             - storage method - InnoDB engine (part of MySQL since version 5.5) likes to store all tables in one big file, but                you can change the settings for one file per table.
         2. **Workflow**:
             - first initial rsync call that moves most of the less frequently used data , while the websites and the server are still on.
             - take the websites and server down
             - perform  further rsync calls on the rest of the data, use checksums to know what data has changed
             - when starting MySQL and trying to execute querys before **100%** of data is copied, errors about corrupted                    data and malfunctions can happen.
             - once everything is copied and doublechecked, that it worked corectly, start MySQL server and run a couple                    count queries on most used tables to *warm up* the database - the tables will be loaded into memory
             - once the database is *warmed up*, start the websites/other services using the database

