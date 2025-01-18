Sure, let's generate the DDL statements for creating tables in MySQL and the queries to create collections in MongoDB.

### MySQL DDL Statements

#### 1. GuestProfile Table
```sql
CREATE TABLE GuestProfile (
    guestId VARCHAR(36) PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) NOT NULL,
    phone VARCHAR(20),
    preferencesId VARCHAR(36),
    membershipId VARCHAR(36),
    FOREIGN KEY (preferencesId) REFERENCES Preferences(preferencesId),
    FOREIGN KEY (membershipId) REFERENCES Membership(membershipId)
);
```

#### 2. Preferences Table
```sql
CREATE TABLE Preferences (
    preferencesId VARCHAR(36) PRIMARY KEY,
    guestId VARCHAR(36) UNIQUE,
    roomType VARCHAR(50),
    dietaryNeeds VARCHAR(255),
    specialServices VARCHAR(255),
    FOREIGN KEY (guestId) REFERENCES GuestProfile(guestId)
);
```

#### 3. LoyaltyPoints Table
```sql
CREATE TABLE LoyaltyPoints (
    pointsId VARCHAR(36) PRIMARY KEY,
    guestId VARCHAR(36) UNIQUE,
    points INT NOT NULL,
    FOREIGN KEY (guestId) REFERENCES GuestProfile(guestId)
);
```

#### 4. Membership Table
```sql
CREATE TABLE Membership (
    membershipId VARCHAR(36) PRIMARY KEY,
    guestId VARCHAR(36) UNIQUE,
    status VARCHAR(50),
    FOREIGN KEY (guestId) REFERENCES GuestProfile(guestId)
);
```

#### 5. Notification Table
```sql
CREATE TABLE Notification (
    notificationId VARCHAR(36) PRIMARY KEY,
    guestId VARCHAR(36),
    message TEXT,
    type VARCHAR(50),
    timestamp TIMESTAMP,
    FOREIGN KEY (guestId) REFERENCES GuestProfile(guestId)
);
```

#### 6. ExternalSystemRequest Table
```sql
CREATE TABLE ExternalSystemRequest (
    requestId VARCHAR(36) PRIMARY KEY,
    systemName VARCHAR(255),
    payload TEXT,
    timestamp TIMESTAMP
);
```

#### 7. ExternalSystemResponse Table
```sql
CREATE TABLE ExternalSystemResponse (
    responseId VARCHAR(36) PRIMARY KEY,
    requestId VARCHAR(36) UNIQUE,
    response TEXT,
    timestamp TIMESTAMP,
    FOREIGN KEY (requestId) REFERENCES ExternalSystemRequest(requestId)
);
```

### MongoDB Collection Creation Queries

#### 1. GuestProfile Collection
```javascript
db.createCollection("GuestProfile");
db.GuestProfile.createIndex({ guestId: 1 }, { unique: true });
```

#### 2. Preferences Collection
```javascript
db.createCollection("Preferences");
db.Preferences.createIndex({ preferencesId: 1 }, { unique: true });
db.Preferences.createIndex({ guestId: 1 }, { unique: true });
```

#### 3. LoyaltyPoints Collection
```javascript
db.createCollection("LoyaltyPoints");
db.LoyaltyPoints.createIndex({ pointsId: 1 }, { unique: true });
db.LoyaltyPoints.createIndex({ guestId: 1 }, { unique: true });
```

#### 4. Membership Collection
```javascript
db.createCollection("Membership");
db.Membership.createIndex({ membershipId: 1 }, { unique: true });
db.Membership.createIndex({ guestId: 1 }, { unique: true });
```

#### 5. Notification Collection
```javascript
db.createCollection("Notification");
db.Notification.createIndex({ notificationId: 1 }, { unique: true });
```

#### 6. ExternalSystemRequest Collection
```javascript
db.createCollection("ExternalSystemRequest");
db.ExternalSystemRequest.createIndex({ requestId: 1 }, { unique: true });
```

#### 7. ExternalSystemResponse Collection
```javascript
db.createCollection("ExternalSystemResponse");
db.ExternalSystemResponse.createIndex({ responseId: 1 }, { unique: true });
db.ExternalSystemResponse.createIndex({ requestId: 1 }, { unique: true });
```
