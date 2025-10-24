# Company-database-in-MySQL
Users, Education, Institute, Branch, Company, Cab, and Works. It stores user profiles, educational backgrounds, company details, and work records. Various JOIN and subquery operations retrieve linked information like user jobs, institutes, and top passed-out years for analysis.


##  MySQL Project: Company Database Management System

###  Project Overview:
This project simulates a relational database for managing employee profiles, education history, company branches, job roles, and transportation logistics. It demonstrates your ability to design normalized schemas, implement foreign key relationships, and perform complex SQL queries for business insights.

---

###  Database Schema Design

#### Users Table
Stores personal details of employees:
- Fields: `UserId`, `Username`, `Email`, `Address`, `Phone_number`, `UserBio`

#### Education Table
Tracks academic qualifications:
- Fields: `EduId`, `Userdegree`, `Passedout_Year`, `Percentage`, `UserId`, `Institute_Name`
- Foreign Keys: `UserId` → `Users`, `Institute_Name` → `Institute`

#### Institute Table
Stores institute names:
- Fields: `InstituteId`, `Institute_Name`

#### Branch Table
Defines company branch locations:
- Fields: `BranchId`, `Branch_Name`, `Area`

#### Company Table
Links companies to branches:
- Fields: `CompanyId`, `Company_Name`, `BranchId`

#### Cab Table
Stores cab service details:
- Fields: `CabId`, `Cab_Name`

#### Works Table
Tracks employment history:
- Fields: `Work_Id`, `Tittle`, `Salary`, `Start_Date`, `End_Date`, `UserId`, `CompanyId`, `CabId`

---

###  SQL Query Highlights

#### Employee Role & Salary
```sql
SELECT Users.Username, Works.Tittle, Works.Salary
FROM Users
INNER JOIN Works ON Users.UserId = Works.UserId;
```

#### Employee Branch & Company Details
```sql
SELECT Users.Username, Branch.Branch_Name, Branch.Area, Company.Company_Name, Works.Tittle, Works.Salary
FROM Users
INNER JOIN Works ON Users.UserId = Works.UserId
INNER JOIN Company ON Works.CompanyId = Company.CompanyId
INNER JOIN Branch ON Company.BranchId = Branch.BranchId;
```

#### Education Filters
- Degrees from Harvard:
```sql
SELECT Userdegree, Passedout_Year, Institute_Name
FROM Education
WHERE Institute_Name = 'Harvard Univ.';
```

- Degrees not from Harvard:
```sql
SELECT Userdegree, Passedout_Year, Institute_Name
FROM Education
WHERE Institute_Name NOT IN ('Harvard Univ.');
```

#### Graduation Year Analysis
- Latest graduation year:
```sql
SELECT Userdegree, Passedout_Year
FROM Education
WHERE Passedout_Year = (SELECT MAX(Passedout_Year) FROM Education);
```

- Before/After latest year:
```sql
SELECT Userdegree, Passedout_Year
FROM Education
WHERE Passedout_Year < (SELECT MAX(Passedout_Year) FROM Education);
```

---

###  Skills Demonstrated
- Relational schema design with foreign key constraints  
- Data insertion and normalization  
- Join operations across multiple tables  
- Subqueries and filtering logic  
- Business logic modeling (roles, branches, transport, education)

