# SQL_Exploratory
# OVERVIEW
This project provided me with the opportunity to explore multiple datasetes in a relational database using various forms of SQL commands.  This project is also my opportunity to demonstrate the knowledge and abilities I have learned throughout my 4 month Data Engineering Bootcamp through Per Scholas.  As well as demonstrate my ability to read and comprehend documentation.  I worked with the following technologies to manage an ETL process for a Credit Card Dataset: Python, MariaDB, Apache Spark.

The Credit Card System database is a system developed for managing activities such as registering new customers and approving or canceling requests.  Below are the three files that contain the customer's transaction information and inventories in the credit card information that was used in this project:
- CDW_SAPP_CUSTOMER.JSON: This file contains existing customer details
- CDW_SAPP_CREDITCARD.JSON: This file contains information about credit card transactions
- CDW_SAPP_BRANCH.JSON: This file contains the information of each branch

# STEP 1- EXTRACT AND LOAD DATA:
Majority of this project will be done in SQL I first loaded the data into MARIADB.  To begin I imported the following Python modules into my py script file: findspark, pyspark.sql and pyspark.sql.functions, pandas, and os.  Then I created a Spark Session and assigned it to my spark variable.  Using spark.read.json() to read my json files and assigning each one to a different variable.  I then used my system variables to hide my MYSQL password and user name, used os.environ.get() to get my username and password and assign it to variables.  Then I created a MYSQL connection using sparks .write.format() and calling my username and password variables instead of my actual username and password so I could connect to MARIADB.

# STEP 2- TRANSFORM DATA:
Once data was loaded into database I begin transforming the data based on the mapping document.  For example, to change the format of the phone number column from XXXXXXX to (XXX)XXX-XXXX in CDW_SAPP_CUSTOMER, I used ALTER TABLE AND MODIFY to change to datatype to VARCHAR.  Then I used UPDATE and SET to CONCAT the  '(', ')', and substring to form the phone number in he proper format and than had it equal the CUST_PHONE column. To convert DAY,MONTH, and YEAR into a TIMEID column (YYYYMMDD) in CDW_SAPP_CUSTOMER.  First, I used ALTER TABLE and MODIFY COLUMN to change datatype of MONTH column to VARCHAR, then ysed UPDATE and SET to concat '0' infront of all months where the length of the MONTH is equel 1 then set it equal to the MONTH COLUMN.  I repeated the steps for the DAY column.  To create a new column I used ALTER TABLE and ADD to add the TIMEID column, UPDATE, and SET to set the TIMEID column equal to the concatination of the YEAR, MONTH, and DAY column.  Lastly I droped the YEAR, MONTH, and DAY individual columns using DROP COLUMN.  To set default to (99999) if the source value is null in BRANCH_ZIP column of the CDW_SAPP_BRANCH table.  First, I used ALTER TABLE and MODIFY COLUMN to change BRANCH_ZIP datatype to an integer and used DEFAULT to set the default to 99999, then insertted 99999 into BRANCH_ZIP where there were nulls.

# STEP 3- SQL EXPLORATION:
Using queries the explore data questions like 'Which branch made the maximum number of Transactions each day?, 'The top 3 months with the largest transaction data, 'The highest Transactions type for each State for branches?', etc.  I order to solve the I used a combinations of joins, and inner joins as well joins in one query.  I also created stored procedures that modify existing account details of a customer, check account details of an existing customer, delete data from a table, select data from table based on given Transaction type, etc.
