# Airbnb Clone ‚Äì Backend Requirement Specifications

This document outlines technical and functional requirements for 3 selected core backend features.

---

## Ì¥ê Feature 1: User Authentication

### Ì≥Ñ Description
Allow users (guests and hosts) to securely register and log in using email and password with JWT-based session management.

### Ì¥ó API Endpoints
- `POST /api/register` ‚Äì Register a new user
- `POST /api/login` ‚Äì Authenticate user and return JWT
- `GET /api/profile` ‚Äì Get current user info (protected)
- `PUT /api/profile` ‚Äì Update profile details (protected)

### Ì¥∏ Request Examples

#### Registration:
```json
{
  "email": "user@example.com",
  "password": "securepass123",
  "role": "guest",
  "first_name": "John",
  "last_name": "Doe"
}


#### Login:

{
  "email": "user@example.com",
  "password": "securepass123"
}

‚úÖ Validation Rules
Email must be unique and properly formatted.

Password must be at least 6 characters.

Role must be either "guest" or "host".

Ì¥í Security
Passwords must be hashed using bcrypt.

JWT tokens should expire in 24 hours.

Rate limiting on login to prevent brute-force attacks.

ÔøΩÔøΩ Feature 2: Property Management
Ì≥Ñ Description
Hosts can add, edit, delete, and view property listings including descriptions, images, and pricing.

Ì¥ó API Endpoints
POST /api/properties ‚Äì Add property (host only)

GET /api/properties ‚Äì List all properties (searchable)

GET /api/properties/{id} ‚Äì View property details

PUT /api/properties/{id} ‚Äì Update property (host only)

DELETE /api/properties/{id} ‚Äì Delete property (host only)

Ì¥∏ Request Example
Add Property: 
{
  "title": "Cozy Apartment",
  "description": "2-bedroom apartment in downtown",
  "location": "New York, NY",
  "price_per_night": 120,
  "amenities": ["WiFi", "AC", "Kitchen"],
  "images": ["img1.jpg", "img2.jpg"]
}

‚úÖ Validation Rules
Title and location are required.

Price must be a positive number.

Max 10 images per property.

Ì¥ß Performance
Use pagination for listing retrieval.

Use filters for location, price range, and amenities.

Ì≥Ö Feature 3: Booking System
Ì≥Ñ Description
Allow guests to book available listings for specific dates and prevent double-booking.

Ì¥ó API Endpoints
POST /api/bookings ‚Äì Create a booking

GET /api/bookings/my ‚Äì View my bookings (guest)

DELETE /api/bookings/{id} ‚Äì Cancel booking (guest)

Ì¥∏ Request Example
Book Listing:

```json
{
  "property_id": "123456",
  "check_in": "2025-07-10",
  "check_out": "2025-07-15"
}
```


‚úÖ Validation Rules
Check-in must be before check-out.

Property must be available for selected dates.

Cannot book your own property.

Ì≤æ Persistence
Booking is only confirmed after payment is successful.

Booking status: pending ‚Üí confirmed ‚Üí canceled ‚Üí completed

Ì¥ß Optimization
Cache property availability lookups.

Prevent race conditions using database locks or transactions.

‚úÖ Summary
These requirements help guide implementation, ensure API consistency, and enforce rules that protect user data, maintain business logic, and support scalability.
