# Cyber_IR_db

## Brief Description

Designed and implemented a relational database to track and manage cybersecurity incidents, threats, and responses with MySQL. Developed a comprehensive Entity Relationship Diagram (ERD), and relational schema. Created, executed, and documented SQL queries to analyze and manage cybersecurity data efficiently.

## Walkthrough - Intro Explanation (Diagrams)

My objective here was to take the knowledge learned fromy my Database Systems and Administration course to learn how to efficiently use SQL to create database that can be used in real-life. With my interests falling in cybersecurity, I decided to create my own database revolving around Incident Response, thus creating this database for this simulated scenario. This simulated scenario undergoes a fictional company known as SecureTech and their Cybersecurity Incident Response Database.

The first thing that was necessary was creating an Entity Relationship diagram along with a relational schema to understand how to effectively draft out this database before creating one with MySQL. Both Entity Relationship Diagram and Relational Schema was created with the website ERDplus.com

<div align="center"><b>Entity Relationship Diagram</b>
<br/>
<img src="https://i.imgur.com/uxOa04Q.png"/>
</div><br/>
<div align="center"><b>Relational Schema</b>
<br/>
<img src="https://i.imgur.com/YtqUtGR.png"/>
</div><br/>

After creating our two diagrams, we can then create the database in MySQL based off our designs. Shown below will be each of the tables made, along with the SQL queries used to create them.

## Walkthrough - Database Tables (CREATE and INSERT Queries)

### 1. Users Table
<img src="https://i.imgur.com/bfvBW2l.png"/>

### CREATE Users Table Query
```sql
CREATE TABLE Users (
U_ID INT PRIMARY KEY,
Name VARCHAR(255),
Contact VARCHAR(255),
Role VARCHAR(255)
);
```
### INSERT INTO Users Query
```sql
INSERT INTO Users (U_ID, Name, Contact, Role) VALUES
(1, ‘Mohammad Khan’, ‘khanm@securetech.org’, ‘Network Analyst’),
(2, ‘Arufa Meherin’, ‘meherina@securetech.org’, ‘Security Specialist’),
(3, ‘Liam Murphy’, ‘murphyl@securetech.org’, ‘IT Support Manager’),
(4, ‘Maria Lopez’, ‘lopezm@securetech.org’, System Administrator),
(5, ‘Emily Smith’, ‘smithe@securetech.org’, ‘Cybersecurity Consultant’);
```
### 2. Devices Table
<img src="https://i.imgur.com/XQ2lbks.png"/>

### CREATE Devices Table Query
```sql
CREATE TABLE Devices (
D_ID INT PRIMARY KEY,
IP VARCHAR(255),
OS VARCHAR(255),
Location VARCHAR(255),
D_Type VARCHAR(255)
);
```
### INSERT INTO Devices Query
```sql
INSERT INTO Devices (D_ID, IP, OS, Location, D_Type) VALUES
(1, ‘192.168.1.10’, ‘Windows 10’, ‘HQ Office’, ‘Workstation’),
(2, ‘192.168.1.20’, ‘Ubuntu 20.04’, ‘HQ Data Center’, ‘Server’),
(3, ‘192.168.1.30’, ‘macOS Catalina’, ‘Remote Office’, ‘Laptop’),
(4, ‘192.168.1.40’, ‘iOS 14’, ‘HQ Office’, ‘Mobile Device’),
(5, ‘192.168.1.50’, ‘Red Hat Enterprise Linux’, ‘HQ Data Center’, ‘Server’);
```
### 3. Threat Intelligence Table
<img src="https://i.imgur.com/5phcznu.png"/>

### CREATE Threat Intelligence Table Query
```sql
CREATE TABLE Threat_Intelligence (
Int_ID INT PRIMARY KEY,
Signature VARCHAR(255),
Mal_IP VARCHAR(255),
Hash VARCHAR(255),
Threat_Type VARCHAR(255)
);
```
### INSERT INTO Threat Intelligence Query
```sql
INSERT INTO Threat_Intelligence (Int_ID, Signature, Mal_IP, Hash, Threat_Type) VALUES
(1, ‘Trojan:Win32/Emotet’,  ‘203.0.113.1’, ‘5f4dcc3b5aa765d61d8327deb882cf99’, ‘Trojan’),
(2, ‘Ransom-WannaCry’, ‘203.0.113.2’, ‘7b52009b64fd0a2a49e6d8a939753077792b0554’, ‘Ransomware’),
(3, ‘Exploit:Java/CVE-2010-4476’, ‘203.0.113.3’, ‘6c569aabbf7775ef8eb7e3b0db5ef3c3’, ‘Exploit’),
(4, ‘Backdoor:PHP/Shell.P’, ‘203.0.113.4’, ‘e99a18c428cb38d5f260853678922e03’, ‘Backdoor’),
(5, ‘SQL Injection Attack’, ‘203.0.113.5’, ‘d41d8cd98f00b204e9800998ecf8427e’, ‘SQL Injection’);
```
### 4. Incidents Table
<img src="https://i.imgur.com/D1JV5BM.png"/>

### CREATE Incidents Query
```sql
CREATE TABLE Incidents (
I_ID INT PRIMARY KEY,
Int_ID INT,
I_Type VARCHAR(255),
Description TEXT,
Detect_Time TIMESTAMP,
Status VARCHAR(255),
Severity INT,
FOREIGN KEY (Int_ID) REFERENCES Incidents(I_ID) ON DELETE CASCADE
);
```
### INSERT INTO Incidents Query
```sql
INSERT INTO Incidents (I_ID, Int_ID, I_Type, Description, Detect_Time, Status, Severity) VALUES
(1, 1, ‘Unauthorized Access’, ‘Detected unusual login pattern.’, ‘2023-07-15 09:00:00’, ‘New’, 5),
(2, 2, ‘Phishing Attempt’, ‘Reported phishing emails targeting company accounts.’, ‘2023-07-15 10:30:00’, ‘New’, 4),
(3, 1, ‘Malware Infection’, ‘Malware detected by antivirus software.’, ‘2023-07-16 08:45:00’, ‘New’, 5),
(4, 3, ‘Attempted Exploited’, ‘Attempted exploitation of known Java vulnerability.’, ‘2023-07-16 13:15:00’, 4),
(5, NULL, ‘Suspicious Activity’, ‘Network traffic anomalies observed.’, ‘2023-07-17’, 07:30:00, ‘New’, 3);
```
### 5. Response Table
<img src="https://i.imgur.com/lc1OLTG.png"/>

### CREATE Response Table Query
```sql
CREATE TABLE Response (
A_ID INT PRIMARY KEY,
Inc_ID INT,
Resp VARCHAR(255),
A_Type VARCHAR(255),
Resp_Personnel VARCHAR(255),
Res_Time TIMESTAMP,
FOREIGN KEY (Inc_ID) REFERENCES Incidents(I_ID) ON DELETE CASCADE
);
```
### INSERT INTO Response Query
```sql
CREATE TABLE Response (
A_ID INT PRIMARY KEY,
Inc_ID INT,
Resp VARCHAR(255),
A_Type VARCHAR(255),
Resp_Personnel VARCHAR(255),
Res_Time TIMESTAMP,
FOREIGN KEY (Inc_ID) REFERENCES Incidents(I_ID) ON DELETE CASCADE
);
```
### 6. Involves Table
<img src="https://i.imgur.com/l5immkJ.png"/>

### CREATE Involves Table Query
```sql
CREATE TABLE Involves (
I_ID INT,
U_ID INT,
PRIMARY KEY (I_ID, U_ID),
FOREIGN KEY (I_ID) REFERENCES Incidents(I_ID) ON DELETE CASCADE,
FOREIGN KEY (U_ID) REFERENCES Users(U_ID) ON DELETE CASCADE
);
```
### INSERT INTO Involves Query
```sql
INSERT INTO Involves (I_ID, U_ID) VALUES
(1, 1),
(2, 2),
(3, 3),
(4, 4),
(5, 5);
```
### 7. Impacts Table
<img src="https://i.imgur.com/dVpfTUJ.png"/>

### CREATE Impacts Table Query
```sql
CREATE TABLE Impacts (
I_ID INT,
D_ID INT,
PRIMARY KEY (I_ID, D_ID),
FOREIGN KEY (I_ID) REFERENCES Incidents(I_ID) ON DELETE CASCADE,
FOREIGN KEY (D_ID) REFERENCES Devices(D_ID) ON DELETE CASCADE
);
```
### INSERT INTO Impacts Query
```sql
INSERT INTO Impacts (I_ID, D_ID) VALUES
(1, 1),
(2, 2),
(3, 3),
(4, 4),
(5, 5);
```

## Walkthrough - Creating Complex Queries
This section of my project was meant to see the capabilities of running advanced queries to obtain diverse and unique response from the database. As per my objective, I had to provide two queries per type of query, and they will all be listed below (Question of what the query wants to perform, and exactly what it does)

### 1. Two different SELECT FROM WHERE ORDER BY statements; each for a single table.
<h4><b> Display all columns in Users in ascending order by Role. </b></h4>
<img src="https://i.imgur.com/w5JmT0o.png"/>

```sql
SELECT *
FROM Users
ORDER BY Role;
```
<h4><b> Display all columns in Devices in ascending order by Location. </b></h4>
<img src="https://i.imgur.com/3MSEzTy.png"/>

```sql
SELECT *
FROM Devices
ORDER BY Location;
```

### 2. Two different SELECT FROM statements that incorporate the use of different aggregate functions (one aggregate function per SELECT statement).
<h4><b> Displays the number of incidents.  </b></h4>
<img src="https://i.imgur.com/TyGOZk9.png"/>

```sql
SELECT COUNT(*) AS IncidentCount
FROM Incidents;
```
<h4><b> Displays the average severity of incidents. </b></h4>
<img src="https://i.imgur.com/k7YurTD.png"/>

```sql
SELECT AVG(Severity) AS AvgSeverity
FROM Incidents;
```

### 3. Two different SELECT statements that incorporate the use of different aggregate functions and GROUP BY.
<h4><b> Displays groups by their incident type and counts the number of incidents in each group. </b></h4>
<img src="https://i.imgur.com/wLiw6vq.png"/>

```sql
SELECT I_Type, COUNT(*) AS TypeCount
FROM Incidents
GROUP BY I_Type;
```
<h4><b> Displays incident groups by their status and calculates the average of each status group. </b></h4>
<img src="https://i.imgur.com/uhPtmxZ.png"/>

```sql
SELECT Status, I_Type, AVG(Severity) AS AvgSeverity
FROM Incidents
GROUP BY Status, I_Type;
```

### 4. Two different SELECT statements that incorporate the use of different aggregate functions and GROUP BY and HAVING.
<h4><b> Displays incident groups in which the average severity is less than 3. </b></h4>
<img src="https://i.imgur.com/Av98ilb.png"/>

```sql
SELECT I_Type, COUNT(*) AS HighSeverityCount
FROM Incidents
GROUP BY I_Type
HAVING AVG(Severity) > 3;
```
<h4><b> Displays the count of incidents where the count is higher than 1. </b></h4>
<img src="https://i.imgur.com/RBm1Qbg.png"/>

```sql
SELECT Inc_ID, COUNT(*) AS ResponseCount
FROM Response
GROUP BY Inc_ID
HAVING COUNT(*) > 1;
```


### 5. Two different SELECT statements that join two tables together.
<h4><b> Joins the Incidents and Response table together and displays all columns with a match between IDs, showing details of incidents along with their corresponding responses. </b></h4>
<img src="https://i.imgur.com/Brzlddk.png"/>

```sql
SELECT *
FROM Incidents i
JOIN Response r ON i.I_ID = r.Inc_ID;
```
<h4><b> Joins the Incidents and Threat Intelligence table and displays all columns with a match between IDs, showing details of incidents along with their associated threat intelligence. </b></h4>
<img src="https://i.imgur.com/A9K0Itc.png"/>

```sql
SELECT *
FROM Incidents i
JOIN Threat_Intelligence t ON i.Int_ID = t.Int_ID;
```


### 6. Two different SELECT statements that join three tables together.
<h4><b> Joins the Incidents, Response, and Users table together based on Incident ID and Responder Personnel. Displays the detais of incidents, their reponses, and the personnel responsible for handling those responses. </b></h4>
<img src="https://i.imgur.com/v7Pbisd.png"/>

```sql
SELECT *
FROM Incidents i
JOIN Response r ON i.I_ID = r.Inc_ID
JOIN Users u ON r.Resp_Personnel = u.Name;
```
<h4><b> Joins the Incidents, Threat Intelligence, Impacts, and Devices tables together based on deviced and intelligence ID. Displays comprehensive information about incidents, associated threat intelligence, impacts on devices, and device details. </b></h4>
<img src="https://i.imgur.com/WcBazFd.png"/>

```sql
SELECT *
FROM Incidents i
JOIN Threat_Intelligence t ON i.Int_ID = t.Int_ID
JOIN Impacts im ON i.I_ID = im.I_ID
JOIN Devices d ON im.D_ID = d.D_ID;
```


### 7. Two different SELECT statements that incorporate nested SELECT statements (aka subqueries).
<h4><b> Displays all incidents where the severity is greater than the average severity of all incidents. </b></h4>
<img src="https://i.imgur.com/QQjOk4x.png"/>

```sql
SELECT *
FROM Incidents
WHERE Severity > (SELECT AVG(Severity) FROM Incidents);
```
<h4><b> Displays all incidents that matches with a threat type of Trojan. </b></h4>
<img src="https://i.imgur.com/SXdwizE.png"/>

```sql
SELECT *
FROM Incidents
WHERE Int_ID IN (
SELECT IntID FROM Threat_Intelligence
WHERE Threat_Type = 'Trojan');
```

## End / Purpose

These are all the queries used for this project and I hope you enjoyed!

This project is to showcase the skills, process, and knowledge used to create, design, and implement a relational database that effectively tracks and manages cybersecurity incidents, associated threats, and response actions within an organization. 

