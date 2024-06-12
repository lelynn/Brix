# Database Model
The database model for Brix, including the textual descriptions of each entity and their attributes, along with SQL code blocks to create the necessary tables.

# Urban Bouldering App Database Model

## Entities and Attributes

### `Person`
Represents users of the app.
- **ID**: A unique identifier for each person.
- **Username**: User's chosen name.
- **Email**: Email address of the user.
- **Password**: Stored password for account security.

### `Location`
Describes specific urban locations where bouldering occurs.
- **ID**: Unique identifier for each location.
- **Street**: Street address of the bouldering location.
- **City**: City where the location is found.

### `Structure`
Specific structures within a location where bouldering can be done.
- **ID**: Unique identifier for each structure.
- **LocationID**: Link to the location where the structure is found.
- **WallName**: Name of the specific wall or structure.

### `Boulder`
Details about individual bouldering problems on a structure.
- **ID**: Unique identifier for each boulder problem.
- **StructureID**: Reference to the structure where the boulder is.
- **Name**: Name of the boulder problem.
- **Grade**: Difficulty grade of the boulder.

## Relationships
- Each `Person` can log multiple `Boulder` instances (many-to-many).
- Each `Location` can have multiple `Structures` (one-to-many).
- Each `Structure` can contain multiple `Boulders` (one-to-many).

## SQL Schema

### Create `Person` Table
```sql
CREATE TABLE Person (
    ID INT PRIMARY KEY AUTO_INCREMENT,
    Username VARCHAR(255) NOT NULL UNIQUE,
    Email VARCHAR(255) NOT NULL UNIQUE,
    Password VARCHAR(255) NOT NULL
);
```

### Create `Location` Table
```sql
CREATE TABLE Location (
    ID INT PRIMARY KEY AUTO_INCREMENT,
    Street VARCHAR(255) NOT NULL,
    City VARCHAR(255) NOT NULL
);
```

### Create `Structure` Table
```sql
CREATE TABLE Structure (
    ID INT PRIMARY KEY AUTO_INCREMENT,
    LocationID INT NOT NULL,
    WallName VARCHAR(255) NOT NULL,
    FOREIGN KEY (LocationID) REFERENCES Location(ID)
);
```

### Create `Boulder` Table
```sql
CREATE TABLE Boulder (
    ID INT PRIMARY KEY AUTO_INCREMENT,
    StructureID INT NOT NULL,
    Name VARCHAR(255) NOT NULL,
    Grade VARCHAR(10) NOT NULL,
    FOREIGN KEY (StructureID) REFERENCES Structure(ID)
);
```

### Create `Climbs` Join Table for Person and Boulder
```sql
CREATE TABLE Climbs (
    PersonID INT,
    BoulderID INT,
    ClimbDate DATE,
    Notes TEXT,
    PRIMARY KEY (PersonID, BoulderID),
    FOREIGN KEY (PersonID) REFERENCES Person(ID),
    FOREIGN KEY (BoulderID) REFERENCES Boulder(ID)
);
```
