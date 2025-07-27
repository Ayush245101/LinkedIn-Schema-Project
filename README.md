# LinkedIn Schema Project

## Overview

This project provides a comprehensive schema design for a LinkedIn-like professional networking platform. The schema is designed to support features such as user profiles, connections, job postings, endorsements, courses, and messaging, closely modeling the core structure of LinkedIn.

## Company Overview

**LinkedIn** is the world's leading professional networking platform, launched in 2003. It connects professionals, empowers job searching, fosters skill development, and enables personal branding. Now part of Microsoft, LinkedIn continues to innovate and provide tools for professional growth.

## Real-World Problems Solved by LinkedIn

LinkedIn addresses several challenges:
- **Professional Networking:** Enables global connection and collaboration.
- **Job Searching:** Streamlines job discovery and applications.
- **Skill Development:** Offers courses and training to help users stay competitive.
- **Personal Branding:** Allows users to showcase their expertise and achievements.

### Case Study: LinkedIn's Solutions to Real-World Problems

1. **Limited Networking Opportunities**
   - *Solution*: Facilitates global, easy networking through intuitive connections and messaging.
2. **Inefficient Job Searching**
   - *Solution*: Provides personalized job recommendations, filters, and application tracking.
3. **Difficulty Showcasing Expertise**
   - *Solution*: Dynamic user profiles to highlight skills, endorsements, and achievements.

## Key Features

- **User Profiles:** Detailed profiles with skills, experience, and endorsements.
- **Connections:** Network building through requests.
- **Job Postings:** Employers and candidates interact via a robust job board.
- **LinkedIn Learning:** Courses for skill development.
- **Messaging:** Direct communication between professionals.
- **Content Sharing:** Posts, articles, and multimedia sharing.

## Schema Description

The schema includes the following main entities:

### User Entity

| Field            | Type           | Description                        |
|------------------|----------------|------------------------------------|
| UserID           | SERIAL (PK)    | Unique user identifier             |
| Name             | VARCHAR(255)   | Full name                          |
| Email            | VARCHAR(255)   | Unique email address               |
| Headline         | VARCHAR(255)   | Professional headline              |
| Summary          | TEXT           | Profile summary                    |
| ProfilePicture   | VARCHAR(255)   | URL to profile picture             |
| RegistrationDate | DATE           | Date of registration               |

### Connections Entity

| Field            | Type           | Description                        |
|------------------|----------------|------------------------------------|
| ConnectionID     | SERIAL (PK)    | Unique connection identifier       |
| UserID           | INT (FK)       | User initiating connection         |
| ConnectedUserID  | INT (FK)       | Connected user                     |
| ConnectionDate   | DATE           | Date of connection                 |

### Jobs Entity

| Field            | Type           | Description                        |
|------------------|----------------|------------------------------------|
| JobID            | SERIAL (PK)    | Unique job post identifier         |
| EmployerID       | INT (FK)       | User posting the job               |
| Title            | VARCHAR(255)   | Job title                          |
| Description      | TEXT           | Job description                    |
| Location         | VARCHAR(255)   | Job location                       |
| PostDate         | DATE           | Date posted                        |

### Relationships

- Users connect with other Users.
- Users apply to Jobs.
- Users endorse Skills of other Users.
- Users enroll in Courses.
- Employers post Jobs.

## ER Diagram

> **Note:** The ER diagram visually represents the entities (`Users`, `Connections`, `Jobs`, `Skills`, and `Courses`) and their relationships. For details, see the [schema project link](https://drive.google.com/file/d/14LiGjCmfawyLWcA8KqAsHbHGg3jP41XQ/view).

## Example SQL Schema

```sql
-- Users table
CREATE TABLE Users (
    UserID SERIAL PRIMARY KEY,
    Name VARCHAR(255) NOT NULL,
    Email VARCHAR(255) UNIQUE NOT NULL,
    Headline VARCHAR(255),
    Summary TEXT,
    ProfilePicture VARCHAR(255),
    RegistrationDate DATE NOT NULL
);

-- Connections table
CREATE TABLE Connections (
    ConnectionID SERIAL PRIMARY KEY,
    UserID INT NOT NULL,
    ConnectedUserID INT NOT NULL,
    ConnectionDate DATE NOT NULL,
    CONSTRAINT FK_User FOREIGN KEY (UserID) REFERENCES Users(UserID),
    CONSTRAINT FK_ConnectedUser FOREIGN KEY (ConnectedUserID) REFERENCES Users(UserID)
);

-- Jobs table
CREATE TABLE Jobs (
    JobID SERIAL PRIMARY KEY,
    EmployerID INT NOT NULL,
    Title VARCHAR(255) NOT NULL,
    Description TEXT,
    Location VARCHAR(255),
    PostDate DATE NOT NULL,
    CONSTRAINT FK_Employer FOREIGN KEY (EmployerID) REFERENCES Users(UserID)
);
```

## Conclusion

LinkedIn's schema design supports robust professional networking, job searching, and skill-building. By analyzing and implementing this schema, we gain insights into how data structures enable the core functionalities and objectives of a leading professional networking platform.

---

**For a detailed ER diagram and further schema details, refer to the project file:**  
[LinkedIn Schema Project](https://drive.google.com/file/d/14LiGjCmfawyLWcA8KqAsHbHGg3jP41XQ/view)
