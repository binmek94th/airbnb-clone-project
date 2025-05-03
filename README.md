# airbnb-clone-project
# Team Roles
- Project manager (PM): Makes sure a product or its part is delivered on time and within budget.
- UI/UX designer: Transforms a product vision into user-friendly designs.
- Software developer: Engineers and stabilizes the product, solves any technical problems emerging during the development lifecycle
- Database Administrator: Manages database design, indexing, and optimizations.
- DevOps Engineer: Handles deployment, monitoring, and scaling of the backend services.
- QA Engineer: Ensures the backend functionalities are thoroughly tested and meet quality standards.
# Technology Stack
- Django: A high-level Python web framework used for building the RESTful API.
- Django REST Framework: Provides tools for creating and managing RESTful APIs.
- PostgreSQL: A powerful relational database used for data storage.
- GraphQL: Allows for flexible and efficient querying of data.
- Celery: For handling asynchronous tasks such as sending notifications or processing payments.
- Redis: Used for caching and session management.
- Docker: Containerization tool for consistent development and deployment environments.
- CI/CD Pipelines: Automated pipelines for testing and deploying code changes.
# Database Design
## Users
Represents the people using the platform.
- id (UUID): Primary key.
- name (string): Full name of the user.
- email (string): Unique email address.
- role (enum): Can be "host" or "guest".
- created_at (timestamp): Account creation time.
A user can:
- Host multiple properties.
- Make multiple bookings.
- Leave reviews on properties they’ve stayed in.
## Properties
- Represents listings available for booking.
- id (UUID): Primary key.
- user_id (UUID): References the host (User).
- title (string): Name of the property.
- location (string): Geographic location.
- price_per_night (decimal): Cost to stay per night.
A property:
- Belongs to a user (host).
- Can have many bookings.
- Can have multiple reviews.
## Bookings
Represents reservations made by guests.
- id (UUID): Primary key.
- user_id (UUID): References the guest.
- property_id (UUID): References the booked property.
- start_date (date): Check-in date.
- end_date (date): Check-out date.
A booking:
- Belongs to one user (guest).
- Belongs to one property.
## Reviews
Feedback left by guests after a stay.
- id (UUID): Primary key.
- user_id (UUID): Reviewer (guest).
- property_id (UUID): Property being reviewed.
- rating (integer): Star rating (e.g., 1–5).
- comment (text): Review content.
A review:
- Belongs to one user.
- Belongs to one property.
## Payments
Tracks financial transactions related to bookings.
- id (UUID): Primary key.
- booking_id (UUID): Associated booking.
- amount (decimal): Total amount paid.
- status (enum): Payment status (e.g., "pending", "completed").
- paid_at (timestamp): Time of payment.
A payment:
- Belongs to one booking.
