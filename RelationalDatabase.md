Databases are most critical component of any system. They make or break a system

> Everything revolutionary starts with Financial Applications

### Properties of DB
1. Data Consistency
2. Data Durability
3. Data Integrity
4. Constraints
5. Everything in one place

The reason relational db are popular is because they give ACID guarantee
ACID - Atomicity, Consistency, Isolation, Durability

1. Atomicity
All statements within a transaction takes effect or none. (either all success or no success, there is no partial transaction/process)
* if 100 rs are updated and after 50th rows system crashes then no record gets updated
* publish a post and increase total posts count. 
> Start transaction => Wrapped transaction => Commit

2. Consistency
data will never go incorrect, no matter what
constraints, cascades, triggers  
Coscades: when parent gets deleted, child deltes automatically. User, posts option  
Ex: you won't be allow to delete a parent, if child exsists (foreign key checks)

3. Durability
when trnsaction commits, the changes outlives outage

4. Isolation
when multiple transaction are executing parallely, the isolation level determines how much changes of one transaction are visible to other
> there are 4 isolation levels

> you pick relational databases for relations and acid


##### SQL Server
SQL Terminal
> mysql -u root -p

###### Other commands
> show databases;
> create database <db name>


