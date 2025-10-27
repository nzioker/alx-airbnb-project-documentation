# User Stories - Airbnb Clone

This document contains user stories derived from the use case diagram interactions for the Airbnb Clone backend system.

## Core User Stories

### Story 1: User Registration
**As a** new user  
**I want to** register for an account with my email and password  
**So that** I can access the platform as either a guest or host

**Acceptance Criteria:**
- User can select role (Guest/Host) during registration
- Email verification is required before account activation
- Password must meet security requirements
- Duplicate email addresses are prevented

### Story 2: Property Listing Creation
**As a** host  
**I want to** create and publish property listings  
**So that** I can attract guests and generate rental income

**Acceptance Criteria:**
- Host can add property details (title, description, type)
- Multiple photos can be uploaded for each property
- Amenities and house rules can be specified
- Pricing and availability calendar can be set

### Story 3: Property Search and Discovery
**As a** guest  
**I want to** search and filter available properties  
**So that** I can find accommodations that match my needs and preferences

**Acceptance Criteria:**
- Search by location with map integration
- Filter by price range, dates, and number of guests
- Filter by amenities (WiFi, kitchen, parking, etc.)
- View detailed property pages with photos and reviews

### Story 4: Booking Creation
**As a** guest  
**I want to** book a property for specific dates  
**So that** I can secure my accommodation for my trip

**Acceptance Criteria:**
- Guest can select check-in/check-out dates
- Total cost is calculated automatically (including fees)
- Real-time availability is checked
- Payment is processed securely upon booking

### Story 5: Payment Processing
**As a** guest  
**I want to** make secure payments for my bookings  
**So that** I can complete my reservation with confidence

**Acceptance Criteria:**
- Multiple payment methods are supported (credit card, PayPal)
- Payment information is encrypted and secure
- Receipt is generated and emailed after payment
- Multi-currency support for international users

### Story 6: Review Submission
**As a** guest  
**I want to** submit reviews and ratings for properties I've stayed at  
**So that** I can share my experience with other users

**Acceptance Criteria:**
- Review can be submitted only after stay completion
- Rating system includes multiple criteria (cleanliness, location, etc.)
- Hosts can respond to reviews
- Reviews are moderated for inappropriate content
