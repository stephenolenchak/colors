# Colors LAMP

An web application that users can add colors to and search for them.

# Technologies used
Linux, Apache, Mysql, PHP (LAMP stack)

# How to deploy Colors LAMP

## Step 1: Database
### Prerequisites
- A digital ocean droplet with LAMP stack image installed

1. Login to MySQL
```bash
mysql -u root -p
```

2. Run the following commands
```bash
CREATE DATABASE IF NOT EXISTS COP4331;
USE COP4331;

DROP TABLE IF EXISTS Users;
DROP TABLE IF EXISTS Colors;
DROP TABLE IF EXISTS Contacts;

CREATE TABLE Users (
  ID INT NOT NULL AUTO_INCREMENT,
  FirstName VARCHAR(50) NOT NULL DEFAULT '',
  LastName VARCHAR(50) NOT NULL DEFAULT '',
  Login VARCHAR(50) NOT NULL DEFAULT '',
  Password VARCHAR(50) NOT NULL DEFAULT '',
  PRIMARY KEY (ID)
) ENGINE=InnoDB;

CREATE TABLE Colors (
  ID INT NOT NULL AUTO_INCREMENT,
  Name VARCHAR(50) NOT NULL DEFAULT '',
  UserID INT NOT NULL DEFAULT 0,
  PRIMARY KEY (ID)
) ENGINE=InnoDB;

CREATE TABLE Contacts (
  ID INT NOT NULL AUTO_INCREMENT,
  FirstName VARCHAR(50) NOT NULL DEFAULT '',
  LastName VARCHAR(50) NOT NULL DEFAULT '',
  Phone VARCHAR(50) NOT NULL DEFAULT '',
  Email VARCHAR(50) NOT NULL DEFAULT '',
  UserID INT NOT NULL DEFAULT 0,
  PRIMARY KEY (ID)
) ENGINE=InnoDB;

CREATE USER IF NOT EXISTS 'TheBeast' IDENTIFIED BY 'WeLoveCOP4331';
GRANT ALL PRIVILEGES ON COP4331.* TO 'TheBeast'@'%';
FLUSH PRIVILEGES;

INSERT INTO Users (FirstName, LastName, Login, Password)
VALUES ('Rick', 'Leinecker', 'RickL', '5832a71366768098cceb7095efb774f2');

INSERT INTO Colors (Name, UserID) VALUES
('Blue', 1),
('White', 1),
('Black', 1),
('Gray', 1),
('Magenta', 1),
('Yellow', 1),
('Cyan', 1);

```

## Step 2: Frontend + API
1. Clone the github repo
```bash
git clone git@github.com:stephenolenchak/colors.git
```
2. Copy the files to /var/www/html/
```bash cp colors/* /var/www/html/
```
3. Edit the base in code.js 
```bash
const urlBase = 'http://{PUT YOUR URL HERE}.com/LAMPAPI';
```