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
### A user can:
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
### A property:
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
### A booking:
- Belongs to one user (guest).
- Belongs to one property.
## Reviews
Feedback left by guests after a stay.
- id (UUID): Primary key.
- user_id (UUID): Reviewer (guest).
- property_id (UUID): Property being reviewed.
- rating (integer): Star rating (e.g., 1–5).
- comment (text): Review content.
### A review:
- Belongs to one user.
- Belongs to one property.
## Payments
Tracks financial transactions related to bookings.
- id (UUID): Primary key.
- booking_id (UUID): Associated booking.
- amount (decimal): Total amount paid.
- status (enum): Payment status (e.g., "pending", "completed").
- paid_at (timestamp): Time of payment.
### A payment:
- Belongs to one booking.
- 
# Feature Breakdown
This project is built with modular, scalable components to support a smooth and secure property rental experience. Below are the core features and their functions:
## User Management
Handles user registration, authentication, and role-based access (host or guest). Ensures data privacy and tailored access to different parts of the system based on user type.
## Property Management
Allows hosts to create, update, and delete listings. Includes property details such as title, location, pricing, and availability to attract guests and enable easy discovery.
## Booking System
Enables guests to reserve properties by selecting available dates. Prevents overlapping bookings and ensures accurate availability tracking across the platform.
## Payment Processing
Securely handles transactions between guests and hosts. Tracks payment status and ensures all bookings are paid for before confirmation.
## Review & Rating System
Allows guests to leave reviews and star ratings after their stay. Helps build trust in listings and hosts, and enables a feedback loop for service improvement.

# API Security
Security is a critical aspect of this platform, especially when dealing with sensitive user data and financial transactions. The following measures will be implemented to ensure robust API protection and secure interactions.

## Authentication
All users must authenticate using secure methods (e.g., JWT or OAuth). This ensures that only verified users can access protected resources, reducing the risk of unauthorized access and identity spoofing.
## Authorization
Role-based access control (RBAC) ensures users can only perform actions permitted by their role (e.g., hosts can manage properties, but guests cannot). This helps maintain system integrity and prevents privilege escalation.
## Rate Limiting
Rate limiting is enforced to prevent abuse of the API through brute-force attacks or excessive requests. It protects server resources and ensures fair use among all users.
## Data Encryption
Sensitive data (like passwords and payment details) is encrypted both in transit (via HTTPS) and at rest. This protects against data breaches and man-in-the-middle attacks.
## Input Validation & Sanitization
All incoming data is validated and sanitized to prevent injection attacks (e.g., SQL injection, XSS). This is crucial to ensure the integrity and security of the application.
