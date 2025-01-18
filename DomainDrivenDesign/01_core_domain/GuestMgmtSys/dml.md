Sure, let's generate sample data for each table and collection. Here are the insert statements for MySQL and MongoDB:

### MySQL Insert Statements

#### 1. GuestProfile Table
```sql
INSERT INTO GuestProfile (guestId, name, email, phone, preferencesId, membershipId) VALUES
('1', 'John Doe', 'john.doe@example.com', '1234567890', '1', '1'),
('2', 'Jane Smith', 'jane.smith@example.com', '0987654321', '2', '2'),
('3', 'Alice Johnson', 'alice.johnson@example.com', '1112223333', '3', '3'),
('4', 'Bob Brown', 'bob.brown@example.com', '4445556666', '4', '4'),
('5', 'Charlie Davis', 'charlie.davis@example.com', '7778889999', '5', '5'),
('6', 'Diana Evans', 'diana.evans@example.com', '1231231234', '6', '6'),
('7', 'Ethan Foster', 'ethan.foster@example.com', '3213214321', '7', '7'),
('8', 'Fiona Green', 'fiona.green@example.com', '4564564567', '8', '8'),
('9', 'George Harris', 'george.harris@example.com', '6546546543', '9', '9'),
('10', 'Hannah White', 'hannah.white@example.com', '7897897890', '10', '10');
```

#### 2. Preferences Table
```sql
INSERT INTO Preferences (preferencesId, guestId, roomType, dietaryNeeds, specialServices) VALUES
('1', '1', 'Deluxe', 'Vegetarian', 'Extra pillows'),
('2', '2', 'Suite', 'Vegan', 'Late check-out'),
('3', '3', 'Standard', 'Gluten-free', 'Early check-in'),
('4', '4', 'Deluxe', 'None', 'Airport pickup'),
('5', '5', 'Suite', 'Halal', 'Spa access'),
('6', '6', 'Standard', 'Kosher', 'Gym access'),
('7', '7', 'Deluxe', 'None', 'Sea view'),
('8', '8', 'Suite', 'Vegetarian', 'Balcony'),
('9', '9', 'Standard', 'Vegan', 'High floor'),
('10', '10', 'Deluxe', 'None', 'Quiet room');
```

#### 3. LoyaltyPoints Table
```sql
INSERT INTO LoyaltyPoints (pointsId, guestId, points) VALUES
('1', '1', 1000),
('2', '2', 1500),
('3', '3', 2000),
('4', '4', 2500),
('5', '5', 3000),
('6', '6', 3500),
('7', '7', 4000),
('8', '8', 4500),
('9', '9', 5000),
('10', '10', 5500);
```

#### 4. Membership Table
```sql
INSERT INTO Membership (membershipId, guestId, status) VALUES
('1', '1', 'Gold'),
('2', '2', 'Platinum'),
('3', '3', 'Silver'),
('4', '4', 'Gold'),
('5', '5', 'Platinum'),
('6', '6', 'Silver'),
('7', '7', 'Gold'),
('8', '8', 'Platinum'),
('9', '9', 'Silver'),
('10', '10', 'Gold');
```

#### 5. Notification Table
```sql
INSERT INTO Notification (notificationId, guestId, message, type, timestamp) VALUES
('1', '1', 'Welcome to our hotel!', 'email', '2025-01-12 10:00:00'),
('2', '2', 'Your room is ready.', 'sms', '2025-01-12 11:00:00'),
('3', '3', 'Enjoy your stay!', 'email', '2025-01-12 12:00:00'),
('4', '4', 'Special offer for you.', 'sms', '2025-01-12 13:00:00'),
('5', '5', 'Thank you for staying with us.', 'email', '2025-01-12 14:00:00'),
('6', '6', 'Your feedback is valuable.', 'sms', '2025-01-12 15:00:00'),
('7', '7', 'Exclusive discount available.', 'email', '2025-01-12 16:00:00'),
('8', '8', 'Join our loyalty program.', 'sms', '2025-01-12 17:00:00'),
('9', '9', 'Room upgrade available.', 'email', '2025-01-12 18:00:00'),
('10', '10', 'Late check-out confirmed.', 'sms', '2025-01-12 19:00:00');
```

#### 6. ExternalSystemRequest Table
```sql
INSERT INTO ExternalSystemRequest (requestId, systemName, payload, timestamp) VALUES
('1', 'BillingSystem', '{"amount": 100}', '2025-01-12 10:00:00'),
('2', 'BookingSystem', '{"roomType": "Deluxe"}', '2025-01-12 11:00:00'),
('3', 'PaymentGateway', '{"transactionId": "12345"}', '2025-01-12 12:00:00'),
('4', 'CRMSystem', '{"customerId": "67890"}', '2025-01-12 13:00:00'),
('5', 'InventorySystem', '{"itemId": "111"}', '2025-01-12 14:00:00'),
('6', 'HRSystem', '{"employeeId": "222"}', '2025-01-12 15:00:00'),
('7', 'MarketingSystem', '{"campaignId": "333"}', '2025-01-12 16:00:00'),
('8', 'AnalyticsSystem', '{"reportId": "444"}', '2025-01-12 17:00:00'),
('9', 'SupportSystem', '{"ticketId": "555"}', '2025-01-12 18:00:00'),
('10', 'FeedbackSystem', '{"feedbackId": "666"}', '2025-01-12 19:00:00');
```

#### 7. ExternalSystemResponse Table
```sql
INSERT INTO ExternalSystemResponse (responseId, requestId, response, timestamp) VALUES
('1', '1', '{"status": "success"}', '2025-01-12 10:05:00'),
('2', '2', '{"status": "success"}', '2025-01-12 11:05:00'),
('3', '3', '{"status": "success"}', '2025-01-12 12:05:00'),
('4', '4', '{"status": "success"}', '2025-01-12 13:05:00'),
('5', '5', '{"status": "success"}', '2025-01-12 14:05:00'),
('6', '6', '{"status": "success"}', '2025-01-12 15:05:00'),
('7', '7', '{"status": "success"}', '2025-01-12 16:05:00'),
('8', '8', '{"status": "success"}', '2025-01-12 17:05:00'),
('9', '9', '{"status": "success"}', '2025-01-12 18:05:00'),
('10', '10', '{"status": "success"}', '2025-01-12 19:05:00');
```

### MongoDB Insert Statements

#### 1. GuestProfile Collection
```javascript
db.GuestProfile.insertMany([
    { guestId: '1', name: 'John Doe', email: 'john.doe@example.com', phone: '1234567890', preferencesId: '1', membershipId: '1' },
    { guestId: '2', name: 'Jane Smith', email: 'jane.smith@example.com', phone: '0987654321', preferencesId: '2', membershipId: '2' },
    { guestId: '3', name: 'Alice Johnson', email: 'alice.johnson@example.com', phone: '1112223333', preferencesId: '3', membershipId: '3' },
    { guestId: '4', name: 'Bob Brown', email: 'bob.brown@example.com', phone: '4445556666', preferencesId: '4', membershipId: '4' },
    { guestId: '5', name: 'Charlie Davis', email: 'charlie.davis@example.com', phone: '7778889999', preferencesId: '5', membershipId: '5' },
    { guestId: '6', name: 'Diana Evans', email: 'diana.evans@example.com', phone: '1231231234', preferencesId: '6', membershipId: '6' },
    { guestId: '7', name: 'Ethan Foster', email: 'ethan.foster