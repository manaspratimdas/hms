### Updated Swagger (OpenAPI) Specification with Security

```yaml
openapi: 3.0.0
info:
  title: Guest Management API
  version: 1.0.0
  description: API for managing guest profiles, preferences, and loyalty programs.

servers:
  - url: http://localhost:8080

components:
  securitySchemes:
    BearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT

  schemas:
    GuestProfile:
      type: object
      properties:
        guestId:
          type: string
        name:
          type: string
        email:
          type: string
        phone:
          type: string
        preferences:
          type: string
        membershipStatus:
          type: string

    Preferences:
      type: object
      properties:
        preferencesId:
          type: string
        guestId:
          type: string
        roomType:
          type: string
        dietaryNeeds:
          type: string
        specialServices:
          type: string

    LoyaltyPoints:
      type: object
      properties:
        pointsId:
          type: string
        guestId:
          type: string
        points:
          type: integer

    Membership:
      type: object
      properties:
        membershipId:
          type: string
        guestId:
          type: string
        status:
          type: string

    Notification:
      type: object
      properties:
        notificationId:
          type: string
        guestId:
          type: string
        message:
          type: string
        type:
          type: string
        timestamp:
          type: string
          format: date-time

    ExternalSystemRequest:
      type: object
      properties:
        requestId:
          type: string
        systemName:
          type: string
        payload:
          type: string
        timestamp:
          type: string
          format: date-time

    ExternalSystemResponse:
      type: object
      properties:
        responseId:
          type: string
        requestId:
          type: string
        response:
          type: string
        timestamp:
          type: string
          format: date-time

    EarnPointsRequest:
      type: object
      properties:
        guestId:
          type: string
        points:
          type: integer

    RedeemPointsRequest:
      type: object
      properties:
        guestId:
          type: string
        points:
          type: integer

security:
  - BearerAuth: []

paths:
  /api/guest-profiles:
    post:
      summary: Create a new guest profile
      tags:
        - GuestProfile
      security:
        - BearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/GuestProfile'
      responses:
        '201':
          description: Guest profile created
    get:
      summary: Get all guest profiles
      tags:
        - GuestProfile
      security:
        - BearerAuth: []
      responses:
        '200':
          description: List of guest profiles
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/GuestProfile'

  /api/guest-profiles/{guestId}:
    get:
      summary: Retrieve a guest profile
      tags:
        - GuestProfile
      security:
        - BearerAuth: []
      parameters:
        - name: guestId
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Guest profile retrieved
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/GuestProfile'
    put:
      summary: Update an existing guest profile
      tags:
        - GuestProfile
      security:
        - BearerAuth: []
      parameters:
        - name: guestId
          in: path
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/GuestProfile'
      responses:
        '200':
          description: Guest profile updated
    delete:
      summary: Delete a guest profile
      tags:
        - GuestProfile
      security:
        - BearerAuth: []
      parameters:
        - name: guestId
          in: path
          required: true
          schema:
            type: string
      responses:
        '204':
          description: Guest profile deleted

  /api/loyalty-program/earn:
    post:
      summary: Earn loyalty points
      tags:
        - LoyaltyProgram
      security:
        - BearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/EarnPointsRequest'
      responses:
        '200':
          description: Points earned

  /api/loyalty-program/redeem:
    post:
      summary: Redeem loyalty points
      tags:
        - LoyaltyProgram
      security:
        - BearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/RedeemPointsRequest'
      responses:
        '200':
          description: Points redeemed

  /api/loyalty-program/{guestId}/points:
    get:
      summary: Get loyalty points
      tags:
        - LoyaltyProgram
      security:
        - BearerAuth: []
      parameters:
        - name: guestId
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Loyalty points retrieved
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/LoyaltyPoints'

  /api/loyalty-program/{guestId}/membership:
    put:
      summary: Update membership status
      tags:
        - LoyaltyProgram
      security:
        - BearerAuth: []
      parameters:
        - name: guestId
          in: path
          required: true
          schema:
            type: string
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Membership'
      responses:
        '200':
          description: Membership status updated

  /api/guest-preferences:
    post:
      summary: Set guest preferences
      tags:
        - GuestPreferences
      security:
        - BearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Preferences'
      responses:
        '200':
          description: Preferences set

  /api/guest-preferences/{guestId}:
    get:
      summary: Get guest preferences
      tags:
        - GuestPreferences
      security:
        - BearerAuth: []
      parameters:
        - name: guestId
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Preferences retrieved
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Preferences'

  /api/notifications:
    post:
      summary: Send a notification
      tags:
        - Notification
      security:
        - BearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Notification'
      responses:
        '200':
          description: Notification sent

  /api/external-systems/integrate:
    post:
      summary: Integrate with an external system
      tags:
        - ExternalSystemIntegration
      security:
        - BearerAuth: []
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ExternalSystemRequest'
      responses:
        '200':
          description: Integration request sent
```

This updated Swagger file includes the security components, defining a Bearer authentication scheme and applying it to the relevant endpoints. 