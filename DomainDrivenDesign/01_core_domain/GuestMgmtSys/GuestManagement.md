## Guest Management (Core Domain)
The Guest Management subdomain is crucial for maintaining guest profiles, preferences, and loyalty programs, providing a personalized experience that enhances guest satisfaction and loyalty.

**Subdomain**: Guest Management
- **Bounded Context**: Manages guest profiles, preferences, and loyalty programs.
- **Ubiquitous Language**:
  - **Guest Profile**: The detailed information about a guest, including personal details and preferences.
  - **Loyalty Points**: Points earned by guests for their stays, which can be redeemed for rewards.
  - **Preferences**: Specific requests or likes of a guest, such as room type, dietary needs, or special services.
  - **Membership**: The status of a guest in the hotel's loyalty program.
  - **Rewards**: Benefits or perks given to guests based on their loyalty points or membership status.



### Context Map for Guest Management

1. **Big Ball of Mud**:
   - **Example**: The legacy guest management system that has evolved over time without a clear structure. This system might handle guest profiles, preferences, and loyalty programs but is difficult to maintain and extend.

2. **Anti-Corruption Layers**:
   - **Example**: When integrating the guest management system with an old billing system, an anti-corruption layer can be used to translate and protect the guest management system from the poorly designed billing system.

3. **Separate Ways**:
   - **Example**: Developing a separate system for managing guest preferences and another for handling loyalty programs if shared models are not beneficial. This allows each system to evolve independently without unnecessary coupling.

4. **Open Host Services**:
   - **Example**: Exposing the functionality of the guest management system through a RESTful API. This allows other systems, such as a mobile app or a third-party booking platform, to interact with the guest profiles, preferences, and loyalty programs in a technology-agnostic manner.

5. **Conformist**:
   - **Example**: If a new microservice is introduced to handle guest rewards, it might adopt the data models of the existing guest management system to ensure consistency and avoid the overhead of maintaining a separate model.

6. **Customer/Supplier Team**:
   - **Example**: The backend team responsible for the guest management system acts as a supplier, providing APIs and services. The frontend team, which develops the user interface for hotel staff and guests, acts as the customer, consuming these APIs.

7. **Shared Kernel**:
   - **Example**: Sharing a common model for guest profiles between the guest management system and the hotel's CRM system. This ensures consistency and reduces duplication of effort in maintaining guest information.



### Tactical Patterns for Guest Management

1. **Entity, Value, Aggregate Object**:
   - **Entity**: 
     - **Guest Profile**: Each guest profile is unique and includes personal details and preferences.
     - **Membership**: Represents the status of a guest in the hotel's loyalty program.
   - **Value**:
     - **Preferences**: Immutable details such as room type, dietary needs, or special services.
     - **Loyalty Points**: Immutable points earned by guests for their stays.
   - **Aggregate**:
     - **Guest Profile Aggregate**: Includes the guest profile entity, preferences value, loyalty points value, and membership entity. This aggregate ensures consistency and encapsulates the guest's overall profile and status.

2. **Repository Pattern**:
   - **GuestProfileRepository**: Manages data operations for guest profiles, including saving, updating, and retrieving guest profiles from the database.
   - **LoyaltyProgramRepository**: Handles data operations related to loyalty points and membership status, ensuring that loyalty points are accurately tracked and updated.

3. **Domain, Application, Infrastructure Services**:
   - **Domain Services**:
     - **LoyaltyPointsService**: Encapsulates business logic for earning and redeeming loyalty points.
     - **GuestPreferencesService**: Manages the logic for handling guest preferences and ensuring they are met during their stay.
   - **Application Services**:
     - **GuestManagementService**: Coordinates tasks such as creating and updating guest profiles, managing loyalty points, and handling guest preferences.
   - **Infrastructure Services**:
     - **NotificationService**: Communicates with external systems to send notifications to guests about their loyalty points, membership status, and special offers.
     - **ExternalSystemIntegrationService**: Manages interactions with external systems, such as third-party booking platforms or old billing systems, ensuring smooth data exchange.


