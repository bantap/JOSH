Josh Database Script (T-SQL)
---

```sql

-- ALTER DATABASE JoshDb SET SINGLE_USER WITH ROLLBACK IMMEDIATE;
-- ALTER DATABASE JoshDb SET MULTI_USER;

USE master;

DROP DATABASE IF EXISTS JoshDb;
CREATE DATABASE JoshDb;
GO

USE JoshDb;
GO



--   U s e r s   T a b l e

CREATE TABLE Users
(
   id         INT            NOT NULL IDENTITY PRIMARY KEY,
   username   NVARCHAR(80)   NOT NULL, -- EMail
   password   NVARCHAR(80)   NOT NULL  -- Wombat1
);

CREATE UNIQUE NONCLUSTERED INDEX UqIdx_Username ON Users(username);

SET IDENTITY_INSERT Users ON;
INSERT INTO Users(id, username, password)
   VALUES (1, N'Bantap@ERAU.Edu',     N'Wombat1'),
          (2, N'PBanta101@GMail.Com', N'Wombat1'),
          (3, N'PBanta@Example.Com',  N'Wombat1');
SET IDENTITY_INSERT Users OFF;

SELECT *
   FROM Users;



--   C o m p a n y

CREATE TABLE Company
(
   id                  INT             NOT NULL IDENTITY PRIMARY KEY,
   name                NVARCHAR(80)    NOT NULL,
   location            NVARCHAR(40)    NULL,
   address1            NVARCHAR(40)    NULL,
   address2            NVARCHAR(40)    NULL,
   city                NVARCHAR(40)    NULL,
   state               NVARCHAR(10)    NULL,
   zip                 NVARCHAR(10)    NULL,
   phone               NVARCHAR(20)    NULL,
   email               NVARCHAR(80)    NULL,
   mainWebSite         NVARCHAR(200)   NULL,
   jobOpeningsPage     NVARCHAR(200)   NULL,
   numberOfEmployees   INT             NULL,
   userId              INT             NOT NULL FOREIGN KEY REFERENCES Users(id)
);

SET IDENTITY_INSERT Company ON;
INSERT INTO Company(id, name, location, mainWebSite, jobOpeningsPage, userId)
   VALUES (1, N'Lockheet Martin',          NULL,                  NULL,                   NULL,                                    1),
          (2, N'Northrop Grumman',         NULL,                  NULL,                   NULL,                                    1),
          (3, N'Raytheon',                 N'Colorado Springs',   N'https://www.rtx.com', N'https://www.rtx.com/careers/overview', 1),
          (4, N'Raytheon',                 N'Denver',             N'https://www.rtx.com', NULL,                                    1),
          (5, N'Embry Riddle',             N'Colorado Springs',   NULL,                   NULL,                                    1),
          (6, N'Skill Distillery',         N'Denver Tech Center', NULL,                   NULL,                                    1),
          (7, N'Compassion International', N'Colorado Springs',   NULL,                   NULL,                                    1);
          
SET IDENTITY_INSERT Company OFF;

SELECT *
   FROM Company;



--   E d u c a t i o n

CREATE TABLE Education
(
   id               INT             NOT NULL IDENTITY PRIMARY KEY,
   institution      NVARCHAR(80)    NOT NULL,
   description      NVARCHAR(200)   NULL,
   startDate        DATE            NOT NULL,
   endDate          DATE            NULL,
   stillAttending   BIT             NULL DEFAULT 0,
   major            NVARCHAR(40)    NULL,
   degree           NVARCHAR(20)    NULL,
   completed        BIT             NULL,
   userId           INT             NOT NULL FOREIGN KEY REFERENCES Users(id)
);

SET IDENTITY_INSERT Education ON;
INSERT INTO Education(id, institution, startDate, endDate, major, degree, completed, userid)
   VALUES (1, 'Eagle Rock High School',           '1977-09-15', '1981-06-15', NULL,                               'High School Diploma', 1, 1),
          (2, 'University of California, Irvine', '1981-09-15', '1986-06-15', 'Information and Computer Science', 'Bachelor of Science', 1, 1),
          (3, 'University of Nevada, Las Vegas',  '1991-09-01', '1993-12-15', 'Computer Science',                 'Master of Science',   1, 1);
SET IDENTITY_INSERT Education OFF;

SELECT *
   FROM Education
   ORDER BY endDate;



--   P r e v i o u s   J o b

CREATE TABLE PreviousJob
(
   id            INT              NOT NULL IDENTITY PRIMARY KEY,
   position      NVARCHAR(40)     NULL,
   jobTitle      NVARCHAR(40)     NULL,
   description   NVARCHAR(1000)   NULL,
   startDate     DATE             NULL,
   endDate       DATE             NULL,
   companyId     INT              NOT NULL FOREIGN KEY REFERENCES Company(id),
   userId        INT              NOT NULL FOREIGN KEY REFERENCES Users(id)
);

INSERT INTO PreviousJob(position, description, startDate, endDate, companyId, userid)
   VALUES ('Software Engineer', 'Salesforce software development', '2016-09-15', '2018-06-30', 7, 1),
          ('Instructor',        NULL,                              '2018-07-09', '2020-03-15', 6, 1),
          ('Instructor',        NULL,                              '2020-03-15', '2021-06-30', 5, 1);

SELECT PJ.startDate, PJ.endDate, PJ.position, C.name, C.location
   FROM PreviousJob AS PJ
      INNER JOIN Company AS C
         ON PJ.companyId = C.id;



--   R e f e r e n c e   T a b l e

CREATE TABLE Reference
(
   id              INT            NOT NULL IDENTITY PRIMARY KEY,
   name            NVARCHAR(40)   NOT NULL,
   company         NVARCHAR(60)   NULL,
   relationship    NVARCHAR(20)   NULL,
   phone           NVARCHAR(20)   NULL,
   email           NVARCHAR(80)   NULL,
   dateConfirmed   DATE           NULL,
   userId          INT            NOT NULL FOREIGN KEY REFERENCES Users(id)
);

INSERT INTO Reference(name, company, relationship, dateconfirmed, userid)
   VALUES ('Amy Y.',  'Compassion International', 'Hiring Supervisor', '2020-12-15', 1),
          ('Greg F.', 'Booz Allen Hamilton',      'Team Lead',         '2020-12-15', 1);

SELECT *
   FROM Reference
      INNER JOIN Users
         ON Reference.userid = Users.id;



--   J o b   A p p l i c a t i o n

CREATE TABLE JobApplication
(
   id            INT              NOT NULL IDENTITY PRIMARY KEY,
   url           NVARCHAR(200)    NULL,
   jobNumber     NVARCHAR(40)     NULL,
   jobTitle      NVARCHAR(80)     NULL,
   position      NVARCHAR(80)     NULL,
   description   NVARCHAR(1000)   NULL,
   dateposted    DATE             NULL,
   dateapplied   DATE             NOT NULL,
   companyid     INT              NOT NULL FOREIGN KEY REFERENCES Company(id),
   userid        INT              NOT NULL FOREIGN KEY REFERENCES Users(id)
);

INSERT INTO JobApplication(jobNumber, jobTitle, dateApplied, companyId, userId)
   VALUES ('ABC123',  'Software Engineer 3', '2021-02-15', 3, 1),
          ('123-ABC', 'Software Engineer 4', '2021-02-16', 2, 1);

SELECT *
   FROM JobApplication AS JA
      INNER JOIN Company AS C
         ON JA.companyid = C.id;



--   C o r r e s p o n d e n c e

CREATE TABLE Correspondence
(
   id                 INT              NOT NULL IDENTITY PRIMARY KEY,
   date               DATE             NOT NULL,
   type               NVARCHAR(10)     NOT NULL,
   names              NVARCHAR(40)     NOT NULL,
   description        NVARCHAR(1000)   NOT NULL,
   jobApplicationId   INT              NOT NULL FOREIGN KEY REFERENCES Company(id)
);

INSERT INTO Correspondence(date, type, names, description, jobApplicationId)
   VALUES ('2021-02-22', 'EMail', 'Bob Smith (HR)', 'Schedule Interview', 1),
          ('2021-02-28', 'Zoom',  'John Brown & Susan Jones', 'Technical Interview', 1);

SELECT *
   FROM Correspondence AS C
      INNER JOIN JobApplication AS JA
         ON C.jobApplicationId = JA.id
      INNER JOIN Company AS Cpy
         ON JA.companyid = Cpy.id;



--   C o n t a c t

CREATE TABLE Contact
(
   id                 INT            NOT NULL IDENTITY PRIMARY KEY,
   name               NVARCHAR(40)   NOT NULL,
   phone              NVARCHAR(20)   NOT NULL,
   email              NVARCHAR(80)   NOT NULL,
   companyId          INT            NULL FOREIGN KEY REFERENCES Company(id),         -- NULL Allowed
   jobApplicationId   INT            NULL FOREIGN KEY REFERENCES JobApplication(id)   -- NULL Allowed
);

-- ToDo: Add some INSERT(s) & SELECT(s)



--   R a t i n g

CREATE TABLE Rating
(
   id           INT             NOT NULL IDENTITY PRIMARY KEY,
   source       NVARCHAR(80)    NOT NULL,
   rating       DECIMAL(4, 1)   NOT NULL,   -- 999.9
   outOf        DECIMAL(4, 1)   NOT NULL,   -- 999.9
   percentage                   AS 100.0 * rating / outOf,   -- A computed field
   url          NVARCHAR(200)   NULL,
   companyId    INT             NULL FOREIGN KEY REFERENCES Company(id),
);

INSERT INTO Rating(source, rating, outOf, companyId)
   VALUES ('Glass Door', 3.9,  5.0, 1),
          ('Indeed',     9.2, 10.0, 1);

SELECT *
   FROM Rating AS R
      INNER JOIN Company AS C
         ON R.companyid = C.id;



--   S a l a r y

CREATE TABLE Salary
(
   id           INT             NOT NULL IDENTITY PRIMARY KEY,
   source       NVARCHAR(80)    NOT NULL,
   position     NVARCHAR(80)    NULL,
   salary       BIT             NULL DEFAULT 1,
   salaryFrom   DECIMAL(9, 2)   NOT NULL,   -- 9,999,999.99
   salaryTo     DECIMAL(9, 2)   NULL,       -- 9,999,999.99
   url          NVARCHAR(200)   NULL,
   companyId    INT             NULL FOREIGN KEY REFERENCES Company(id),
);

-- ToDo: Add some INSERT(s) & SELECT(s)
```

[Back](ReadMe.md)
