# Data Normalization and Entity-Relationship Diagramming

# University Courses Database 4NF Normalization Report

## Original Data Set

The original dataset was structured as follows, which led to multiple anomalies and redundancies:

| assignment_id | student_id | due_date  | professor | assignment_topic       | classroom | grade | relevant_reading   | professor_email    |
|---------------|------------|-----------|-----------|------------------------|-----------|-------|--------------------|--------------------|
| 1             | 1          | 23.02.21  | Melvin    | Data normalization     | WWH 101   | 80    | Deumlich Chapter 3 | l.melvin@foo.edu   |
| 2             | 7          | 18.11.21  | Logston   | Single table queries   | 60FA 314  | 25    | Dümmlers Chapter 11| e.logston@foo.edu  |
| ...           | ...        | ...       | ...       | ...                    | ...       | ...   | ...                | ...                |

### Issues with the Original Data Set

This structure isn't compliant with 4NF for several reasons:

1. **Multi-Valued Dependencies**: A single record could contain multiple types of information (assignments, professors, classrooms) that are not strictly related to each other but to the course.
2. **Redundancy**: Information such as `professor_email` and `relevant_reading` was repeated across multiple records for the same course offering, leading to update anomalies.
3. **Update Anomalies**: Changing a professor's email would require multiple updates if they were teaching more than one section.

## 4NF Compliant Data Set

To address these issues, the dataset was restructured into the following tables:

### Courses

| CourseID | CourseName          | CourseTopic          |
|----------|---------------------|----------------------|
| 101      | Database Systems    | Data normalization   |
| 102      | Introduction to SQL | Single table queries |
| ...      | ...                 | ...                  |

### Professors

| ProfessorID | ProfessorName | ProfessorEmail       |
|-------------|---------------|----------------------|
| 1           | Melvin        | l.melvin@foo.edu     |
| 2           | Logston       | e.logston@foo.edu    |
| ...         | ...           | ...                  |

### Classrooms

| ClassroomID | Location  |
|-------------|-----------|
| 1           | WWH 101   |
| 2           | 60FA 314  |
| ...         | ...       |

### Assignments

| AssignmentID | AssignmentTopic       | RelevantReading       |
|--------------|-----------------------|-----------------------|
| 1            | Data normalization    | Deumlich Chapter 3    |
| 2            | Single table queries  | Dümmlers Chapter 11   |
| ...          | ...                   | ...                   |

### CourseOfferings

| OfferingID | CourseID | ProfessorID | ClassroomID |
|------------|----------|-------------|-------------|
| 1          | 101      | 1           | 1           |
| 2          | 102      | 2           | 2           |
| ...        | ...      | ...         | ...         |

### StudentEnrollments

| EnrollmentID | StudentID | OfferingID | Grade |
|--------------|-----------|------------|-------|
| 1            | 1         | 1          | 80    |
| 2            | 7         | 2          | 25    |
| ...          | ...       | ...        | ...   |

### AssignmentAllocations

| AllocationID | AssignmentID | OfferingID |
|--------------|--------------|------------|
| 1            | 1            | 1          |
| 2            | 2            | 2          |
| ...          | ...          | ...        |

## ER Diagram

![ER Diagram for University Courses Database](/Users/taranagarwal/Desktop/database & design/5-database-design-taranagarwal18/images/HW 5 Diagram.drawio.svg)

## Changes Made and 4NF Compliance

By restructuring the dataset into separate tables based on entity and relationship types, the following was achieved:

- **Elimination of Multi-Valued Dependencies**: Each table now represents a distinct entity or relationship, ensuring no table contains more than one multi-valued fact about an entity, which complies with 4NF.
- **Reduction in Redundancy**: Professor emails, course topics, and other previously redundant information are now stored in their own tables, significantly reducing redundancy and eliminating update anomalies.
- **Simplified Updates**: Updating information like a professor's email now requires changing only one record in the `Professors` table.

This new structure adheres to the 4NF by ensuring that each record type has no multi-valued dependencies, thereby avoiding redundancy and update anomalies.

