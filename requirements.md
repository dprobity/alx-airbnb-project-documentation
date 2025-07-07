# Airbnb Clone – Backend Requirement Specifications

This document outlines technical and functional requirements for 3 selected core backend features.

---

## � Feature 1: User Authentication

### � Description
Allow users (guests and hosts) to securely register and log in using email and password with JWT-based session management.

### � API Endpoints
- `POST /api/register` – Register a new user
- `POST /api/login` – Authenticate user and return JWT
- `GET /api/profile` – Get current user info (protected)
- `PUT /api/profile` – Update profile details (protected)

### � Request Examples

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

✅ Validation Rules
Email must be unique and properly formatted.

Password must be at least 6 characters.

Role must be either "guest" or "host".

� Security
Passwords must be hashed using bcrypt.

JWT tokens should expire in 24 hours.

Rate limiting on login to prevent brute-force attacks.

�� Feature 2: Property Management
� Description
Hosts can add, edit, delete, and view property listings including descriptions, images, and pricing.

� API Endpoints
POST /api/properties – Add property (host only)

GET /api/properties – List all properties (searchable)

GET /api/properties/{id} – View property details

PUT /api/properties/{id} – Update property (host only)

DELETE /api/properties/{id} – Delete property (host only)

� Request Example
Add Property: 
{
  "title": "Cozy Apartment",
  "description": "2-bedroom apartment in downtown",
  "location": "New York, NY",
  "price_per_night": 120,
  "amenities": ["WiFi", "AC", "Kitchen"],
  "images": ["img1.jpg", "img2.jpg"]
}

✅ Validation Rules
Title and location are required.

Price must be a positive number.

Max 10 images per property.

� Performance
Use pagination for listing retrieval.

Use filters for location, price range, and amenities.

� Feature 3: Booking System
� Description
Allow guests to book available listings for specific dates and prevent double-booking.

� API Endpoints
POST /api/bookings – Create a booking

GET /api/bookings/my – View my bookings (guest)

DELETE /api/bookings/{id} – Cancel booking (guest)

� Request Example
Book Listing:

```json
{
  "property_id": "123456",
  "check_in": "2025-07-10",
  "check_out": "2025-07-15"
}
```


✅ Validation Rules
Check-in must be before check-out.

Property must be available for selected dates.

Cannot book your own property.

� Persistence
Booking is only confirmed after payment is successful.

Booking status: pending → confirmed → canceled → completed

� Optimization
Cache property availability lookups.

Prevent race conditions using database locks or transactions.

✅ Summary
These requirements help guide implementation, ensure API consistency, and enforce rules that protect user data, maintain business logic, and support scalability.
