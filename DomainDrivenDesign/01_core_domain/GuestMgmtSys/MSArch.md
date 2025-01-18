### Microservice Architecture

#### Secure Services
1. **GuestProfileService**
   - **Domain Object**: GuestProfile
     - **Attributes**:
       - `guestId`: Unique identifier for the guest
       - `name`: Full name of the guest
       - `email`: Email address of the guest
       - `phone`: Phone number of the guest
       - `preferences`: Guest preferences (room type, dietary needs, special services)
       - `membershipStatus`: Status of the guest in the hotel's loyalty program
   - **Service**: GuestProfileService
     - **Methods**:
       - `createGuestProfile(GuestProfile guestProfile)` - **Roles**: Admin, Manager
       - `updateGuestProfile(String guestId, GuestProfile guestProfile)` - **Roles**: Admin, Manager
       - `getGuestProfile(String guestId)` - **Roles**: Admin, Manager, Guest - **Cached**
       - `deleteGuestProfile(String guestId)` - **Roles**: Admin
   - **Controller**: GuestProfileController
     - **API Endpoints**:
       - `POST /api/guest-profiles` - **Roles**: Admin, Manager
       - `PUT /api/guest-profiles/{guestId}` - **Roles**: Admin, Manager
       - `GET /api/guest-profiles/{guestId}` - **Roles**: Admin, Manager, Guest - **Cached**
       - `DELETE /api/guest-profiles/{guestId}` - **Roles**: Admin
   - **Database**: RDBMS (MySQL)

2. **LoyaltyProgramService**
   - **Domain Object**: LoyaltyPoints, Membership
     - **Attributes**:
       - `guestId`: Unique identifier for the guest
       - `points`: Number of loyalty points earned by the guest
       - `membershipStatus`: Status of the guest in the loyalty program (e.g., Silver, Gold, Platinum)
   - **Service**: LoyaltyProgramService
     - **Methods**:
       - `earnPoints(String guestId, int points)` - **Roles**: Admin, Manager
       - `redeemPoints(String guestId, int points)` - **Roles**: Admin, Manager, Guest
       - `getLoyaltyPoints(String guestId)` - **Roles**: Admin, Manager, Guest - **Cached**
       - `updateMembershipStatus(String guestId, Membership membership)` - **Roles**: Admin, Manager
   - **Controller**: LoyaltyProgramController
     - **API Endpoints**:
       - `POST /api/loyalty-program/earn` - **Roles**: Admin, Manager
       - `POST /api/loyalty-program/redeem` - **Roles**: Admin, Manager, Guest
       - `GET /api/loyalty-program/{guestId}/points` - **Roles**: Admin, Manager, Guest - **Cached**
       - `PUT /api/loyalty-program/{guestId}/membership` - **Roles**: Admin, Manager
   - **Database**: RDBMS (MySQL)

#### Asynchronous Services (Using Kafka)
1. **NotificationService**
   - **Domain Object**: Notification
     - **Attributes**:
       - `notificationId`: Unique identifier for the notification
       - `guestId`: Unique identifier for the guest
       - `message`: Content of the notification
       - `type`: Type of notification (e.g., email, SMS)
       - `timestamp`: Time when the notification was sent
   - **Service**: NotificationService
     - **Methods**:
       - `sendNotification(Notification notification)` - **Roles**: Admin, Manager
   - **Controller**: NotificationController
     - **API Endpoints**:
       - `POST /api/notifications` - **Roles**: Admin, Manager
   - **Database**: NoSQL (MongoDB)
   - **Communication**: Asynchronous communication using Kafka

2. **ExternalSystemIntegrationService**
   - **Domain Object**: ExternalSystemRequest, ExternalSystemResponse
     - **Attributes**:
       - `requestId`: Unique identifier for the request
       - `systemName`: Name of the external system
       - `payload`: Data to be sent to the external system
       - `response`: Response received from the external system
       - `timestamp`: Time when the request was made
   - **Service**: ExternalSystemIntegrationService
     - **Methods**:
       - `integrateWithSystem(ExternalSystemRequest request)` - **Roles**: Admin, Manager
   - **Controller**: ExternalSystemIntegrationController
     - **API Endpoints**:
       - `POST /api/external-systems/integrate` - **Roles**: Admin, Manager
   - **Database**: NoSQL (MongoDB)
   - **Communication**: Asynchronous communication using Kafka

#### Mixed Communication Services
1. **GuestPreferencesService**
   - **Domain Object**: Preferences
     - **Attributes**:
       - `guestId`: Unique identifier for the guest
       - `roomType`: Preferred room type of the guest
       - `dietaryNeeds`: Dietary requirements of the guest
       - `specialServices`: Any special services requested by the guest
   - **Service**: GuestPreferencesService
     - **Methods**:
       - `setPreferences(String guestId, Preferences preferences)` - **Roles**: Admin, Manager, Guest
       - `getPreferences(String guestId)` - **Roles**: Admin, Manager, Guest - **Cached**
   - **Controller**: GuestPreferencesController
     - **API Endpoints**:
       - `POST /api/guest-preferences` - **Roles**: Admin, Manager, Guest
       - `GET /api/guest-preferences/{guestId}` - **Roles**: Admin, Manager, Guest - **Cached**
   - **Database**: NoSQL (MongoDB)
   - **Communication**: Can use both synchronous and asynchronous communication

