# SQL-EPL-MatchData-MySQL-Beginner
This repository is created to demonstrate hands-on learning of SQL; as well as the infrastructure required to set it up.

STEP 1: CREATED AND SET UP DATABASE SERVER ON THE CLOUD PLATFORM

Free MS Azure Subscription is used to create resources on Azure, including a Linux Database server along with associated network components.

<img width="940" height="511" alt="image" src="https://github.com/user-attachments/assets/28da11c2-1629-4e50-91af-ab7c11490959" />


STEP 2: SETTING UP USER AND LOGGING ONTO THE SERVER USING SSH ENCRYPTED KEYS AND INSTALL MYSQL ON THE SERVER

Windows Subsystem for Linux (WSL) on home pc was used to access the server on Azure cloud. Server is Linux Ubuntu based.

<img width="940" height="394" alt="image" src="https://github.com/user-attachments/assets/dbc368f6-d225-4429-b5e2-a56eb9bf18b3" />


Upon accessing the Server, Mysql was instaled on the server.

<img width="940" height="377" alt="image" src="https://github.com/user-attachments/assets/7d665eaf-a7c0-4db1-b79d-91e6aedfb76a" />



STEP 3: Data downloaded from Kaggle.com in the .csv format. Transferred data onto the server. 

English Premier League (EPL) Match Data 2000-2025:
Data was downloaded from this link https://www.kaggle.com/datasets/marcohuiii/english-premier-league-epl-match-data-2000-2025.

<img width="940" height="458" alt="image" src="https://github.com/user-attachments/assets/43c24b73-647e-4de0-a596-02f6551aca26" />

<img width="940" height="409" alt="image" src="https://github.com/user-attachments/assets/718eea09-7c46-4374-9251-deb540c2225c" />


Data was securely copied from the local machine to the server.

<img width="1045" height="28" alt="image" src="https://github.com/user-attachments/assets/de9eeeb2-da68-4c4c-8fdb-e9b277d8db12" />


STEP 4: Database and table creation, mounting data from .csv to sql tables.

Below commands were used to create database 'cloud_sql_demo' and table 'epl_2025' with required fields.

<img width="530" height="849" alt="image" src="https://github.com/user-attachments/assets/f2152171-ad67-4b80-a1f7-fc3adf4404e6" />


SHOW DATABASE; - OUTPUT

<img width="394" height="348" alt="image" src="https://github.com/user-attachments/assets/33701075-2475-4edd-822b-9242d1e71f62" />


USE cloud_sql_demo SHOW TABLES; - OUTPUT

<img width="939" height="189" alt="image" src="https://github.com/user-attachments/assets/24599eab-4f3f-4a1b-9733-0d18fdc04d2d" />

<img width="516" height="223" alt="image" src="https://github.com/user-attachments/assets/a2d65f64-4874-4ef4-9ec6-1e826bed1d1a" />


Transfer of data from .csv on the local machine to the server, and then mounting on the database was completing after overcoming challenges as mySQL does not allow copying data from anywhere on the server. It needs to be on a specific location. 

MySQL server has a security feature enabled called --secure-file-priv. This option restricts file import/export operations (like LOAD DATA INFILE) to only work with files located in a specific directory, which is set by the server configuration to prevent unauthorized file access.

<img width="940" height="62" alt="image" src="https://github.com/user-attachments/assets/5c63b743-f863-4bd2-a5c6-8f22a99b143c" />


STEP 5: Querying the database

From the table, showing the first 10 records.

SELECT * FROM epl_2025 LIMIT 10;

<img width="990" height="351" alt="image" src="https://github.com/user-attachments/assets/5b49fecc-a832-440e-9fb5-999c3c843915" />


Counting total records in the table.

SELECT COUNT(*) AS total_rows FROM epl_2025;

<img width="782" height="225" alt="image" src="https://github.com/user-attachments/assets/6fb9360a-1938-464a-8384-28e5ad121a63" />


Being a Liverpool supporter, I am interested in Liverpool and want to extract data of their last 10 winning matches. Irrespective of the fact that they are away or home. 

SELECT HomeTeam, AwayTeam, FullTimeResult FROM epl_2025 WHERE HomeTeam = 'Liverpool' AND FullTimeResult = 'H' OR AwayTeam = 'Liverpool' AND FullTimeResult = 'A'

<img width="940" height="199" alt="image" src="https://github.com/user-attachments/assets/4e9e2f79-4a04-4a11-9d0c-80b56b0f532f" />


I am interested in the number of fouls committed. Show the date, home/away teams, home/away fouls, and the FullTimeResult. Sample first 10 records.

SELECT MatchDate, HomeTeam, AwayTeam, HomeFouls, AwayFouls, FulltimeResult FROM epl_2025 LIMIT 10;

<img width="940" height="291" alt="image" src="https://github.com/user-attachments/assets/84bbb6b0-5c18-4003-a8b3-b6ea7da14475" />


A manager at one of the team may be interested to know which teams have adopted a physical game strategy at home, to get a win. Playing physical could lead to more fouls and at a home game it is usually a defensive strategy. So he might be interest in last 10 games where Home team made more fouls than the Away team, and ended on the winning side.

SELECT MatchDate, HomeTeam, AwayTeam, HomeFouls, AwayFouls, FulltimeResult FROM epl_2025 WHERE HomeFouls > AwayFouls AND FullTimeResult = 'H' ORDER BY MatchDate DESC LIMIT 10;

<img width="1053" height="202" alt="image" src="https://github.com/user-attachments/assets/0ba5bb93-2bba-43a1-9fba-ec3deaeb59d2" />


STEP 6: Installing the MySQL Desktop version and making the database publically available

Host IP 4.200.26.109 on Port 3306 is to be used to access the database. Username is guest. No password.

<img width="940" height="615" alt="image" src="https://github.com/user-attachments/assets/7d8a42b9-f9bf-412b-9794-398846dc034e" />


Database on MySQL Desktop version

<img width="940" height="527" alt="image" src="https://github.com/user-attachments/assets/22484a80-9167-4839-8cb5-6fd570ea8eea" />



