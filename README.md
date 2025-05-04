# airbnb-clone-project
ALX ProDev Course Project

## Brief overview of the project
This airbnb clone project is a full-stack web application that allows users to list, search, and book short-term rentals. The application supports detailed property listings with images and descriptions, booking management, user reviews, and search/filter functionalities.

## Project Goals
1. User authentication - Enable user sign-up, login, logout, profile management
2. Property listing - allow admin users create, edit, and delete property listings with title, description, price, location, and images.
3. Search and filtering - implement search functionality with filters (e.g. location, price range, number of guests)
4. Booking system - allow users view abailability and make bookings for specific dates
5. Booking management - Enable users to manage their reservations and allow host users to manage incoming booking.
6. Support secure image upload for property listings.
7. Enable users to make reviews and ratings of their experience on the properties they have interacted with.
8. Responsive design.

## Tech Stack
1. Frontend - HTML5, CSS3, JS, React.Js, Tailwind CSS/Bootstrap
2. Backend - Django, Django REST Framework. GraphQL
3. Database - PostgreSQL, Redis, Cassandra, ElasticSearch
4. Authentication - Django built-in auth system, JWT
5. Message Broker & Real-time processing - Kafka, Kafka consumers
6. Big Data and Analytics - Apache Spark Streaming, Hadoop
7. Load Balancing - Load Balancers (LB)
8. Content Delivery - Content Delivery Network (CDN)

## Team Roles
1.Business Analyst - Understands the business landscape where the application is to be used and translates the customer processes and needs into requirements.
2. Project Manager - Oversees the planning, execution, and delivery of the project. Coordinates between team members, manages timelines, and ensures the project stays aligned with goals and budget.
3. UI/UX Designer - Serves to transform the product vision into user friendly designs for a good user experince. Responsibilities include creating wireframes, and final visual designs for the application focusing on the usability, accessibility, and aesthetic appeal to ensure the platform is engaging and user friendly. 
4. Software Architect - Designs a high level software architecture. Responsibilities include selecting appropriate tools and platforms for the project and set up code quality standards and perform code reviews.
5. Software Developer - 
  Frontend Developer - Builds the user interface and client-side functionality using HTML, CSS (Bootstrap), and JavaScript. They ensure a responsive and intuitive user experience for all user roles (students, teachers, admin).
  Backend Developer - Develops the server-side logic, APIs, and database integration. In this project, they work primarily with Python and Django to implement core business logic and RESTful services.
6. Database Administrator -  Designs, implements, and maintains the database structure. Ensures data integrity, performance optimization, and security. Works closely with the backend team to support data models and migrations.
Quality Assurance Engineer - Tests the application to identify bugs and ensure functionality meets the requirements. Develops automated and manual test plans, and ensures continuous integration practices are followed.
7. DevOps Engineer - Manages deployment, CI/CD pipelines, and cloud infrastructure. Ensures the system runs reliably, scales effectively, and is securely deployed to production environments.
Security Specialist -  Ensures the system is secure from vulnerabilities, sets up authentication and authorization protocols, and conducts penetration testing where necessary.
8. Content Developer -  Creates and manages platform content including rentals titles, description, and images.

## Technology Stack
1. Frontend
  HTML5: The standard markup language used for creating the structure of web pages.
  CSS3: for styling the web application to ensure a visually appealing and responsive layout.
  JavaScript (JS): to provide interactivity and dynamic content rendering on the client side.
  React.js: for building fast and scalable user interfaces.
  Tailwind CSS / Bootstrap: CSS frameworks to streamline responsive UI design and improve the overall user experience with pre-built utility classes and components.

2. Backend
  Django: A high-level Python web framework used for building the core application logic, handling user authentication, managing models, and integrating with the database.
  Also, for integration with external services (e.g., Kafka producers).
  Django REST Framework (DRF): An extension of Django that simplifies the creation of RESTful APIs used by the frontend to interact with the backend.
  GraphQL: An alternative API layer to REST, providing a flexible and efficient way for clients to query only the data they need. Useful for complex data interactions and      reducing over-fetching in mobile or SPA frontends.

4. Database
  PostgreSQL: A powerful, open-source relational database system used for securely storing and querying user data, property listings, booking records, and reviews.
  Redis: In-memory data store for caching frequently accessed data and managing sessions.
  Cassandra: A distributed NoSQL database optimized for handling large volumes of time-series or archival booking data across multiple nodes.
  ElasticSearch: Powers the search service for hotels/listings with fast and flexible querying.

5. Authentication and Authorization
   Django Built-in Auth System: Handles user registration, login, logout, and permission management with secure password hashing.
   JWT (JSON Web Tokens): Provides stateless, token-based authentication for securely identifying users in API requests.

6. Message Broker & Real-Time processing
   Kafka: A distributed streaming platform used for handling real-time data pipelines and message brokering between microservices.
   Kafka Consumers: Services that consume and process data from Kafka topics, such as for activity tracking or logging user actions in real time. Handles notifications       
   (emails, app alerts), search updates (via ElasticSearch), and Data Archival (Cassandra).
7. Big Data and Analytics
   Apache Spark Streaming: Enables real-time data processing and analytics, allowing the platform to analyze user behavior, trends, and metrics on the fly.
   Hadoop: Used for batch processing and storage of large datasets, especially useful for long-term analytics, reporting, and machine learning workloads.
   
9. Load Balancing
    LB: Distributes incoming traffic across multiple backend servers to ensure high availability, fault tolerance, and optimal resource utilization.
   
11. Content Delivery
   CDN: Delivers static assets like images, videos, and stylesheets from edge locations closest to users, reducing latency and improving load times.

## Database Design
1. User
Represents customers and hosts using the platform.

    id: Primary key   
    username: Unique identifier
    email: Unique email address
    password: Hashed password
    is_host: Boolean flag to distinguish hosts from customers

    Relationship - A user can list multiple properties (if host) and make multiple bookings (if customer).

2. Property
Represents listings available for booking.

    id: Primary key
    owner: ForeignKey → User (host)
    title: Property title
    description: Text description of the listing
    location: City/region/address
    image: Images of the property

   Relationship - A property is owned by one user (host) and can have many bookings and reviews.

3. Booking
Represents a reservation made by a user.

    id: Primary key
    user: ForeignKey → User (customer)
    property: ForeignKey → Property
    check_in: Date
    check_out: Date
    status: (e.g., pending, confirmed, cancelled)

    Relationship - Each booking links a user and a property. A user can have many bookings.

4. Review
User-generated feedback for a property.

    id: Primary key
    user: ForeignKey → User (reviewer)
    property: ForeignKey → Property
    rating: Integer (e.g., 1–5 stars)
    comment: Text

    Relationship - A user can review a property once per booking. A property can have many reviews.

5. Payment
Tracks financial transactions for bookings.
    
    id: Primary key
    booking: OneToOneField → Booking
    amount: Decimal
    payment_date: DateTime
    payment_status: (e.g., completed, pending, failed)

    Relationship - Each booking has one corresponding payment.

Entity Relationships Summary
User ↔ Property: One-to-many (host can list multiple properties)

User ↔ Booking: One-to-many (user can book multiple properties)

Property ↔ Booking: One-to-many (each property can be booked multiple times)

Property ↔ Review: One-to-many (property can receive many reviews)

Booking ↔ Payment: One-to-one (each booking has one payment)


## Feature Breakdown
1. User Management
Allows users to register, log in, log out, and manage their profiles securely. Hosts and guests are distinguished using role flags, enabling proper access control and interaction within the platform.

2. Property Management
Enables hosts to create, update, and manage property listings. Each listing includes descriptions, images, location, and pricing details to ensure that guests have all necessary information to make informed booking decisions.

3. Booking System
Facilitates the reservation process where guests can select properties, view availability, and confirm bookings. The system manages check-in/check-out dates and booking statuses, ensuring smooth and conflict-free operations.

4. Search and Filtering
Users can search for properties based on location, availability, and price range. The search functionality is optimized to provide relevant results quickly, enhancing the user experience.

5. Payment Integration
Implements secure payment processing for completed bookings. It handles the transaction lifecycle, from pending to completed status, ensuring reliable financial tracking.

6. Review and Rating System
Allows guests to leave reviews and rate properties after their stay. This feature builds trust and transparency in the platform by helping future users assess the quality of listings.

7. Responsive UI and Frontend
The platform is built with React.js and styled using Tailwind CSS or Bootstrap to ensure a seamless user experience across devices. Dynamic interfaces and component reusability improve overall usability and maintainability.

8. API Layer (Django REST Framework)
All frontend-backend interactions are handled through secure RESTful APIs. These APIs ensure clean separation of concerns and facilitate scalability and mobile compatibility.

9. Role-Based Access Control
Different permissions and access levels are implemented for hosts and guests. This ensures that only authorized users can perform specific actions like adding properties or confirming bookings.

## API Security
Securing the backend APIs is essential to protect sensitive user data, prevent unauthorized access, and ensure the integrity of financial transactions. Below are the key API security measures implemented in this project:

1. Authentication (JWT)
We use JSON Web Tokens (JWT) for stateless authentication across the API. This ensures that only verified users can access protected endpoints after login. JWT tokens are signed and tamper-proof, providing a secure way to maintain sessions.

Why it's important: Prevents unauthorized users from accessing user accounts or sensitive actions like bookings and payments.

2. Authorization
Role-based access control is implemented to differentiate between users (guests and hosts). Certain actions—like listing properties or viewing bookings—are only accessible based on the user’s role.

Why it's important: Ensures that users only access features and data appropriate to their role, protecting business logic and user privacy.

3. Rate Limiting
We will implement rate limiting using tools such as Django Ratelimit or middleware to prevent abuse of the API through brute-force attacks or denial-of-service attempts.

Why it's important: Protects the application from spam, abuse, and performance degradation due to high traffic or malicious activity.

4. Data Validation & Sanitization
All inputs from users are validated and sanitized at both frontend and backend levels to prevent injection attacks such as SQL Injection and Cross-Site Scripting (XSS).

Why it's important: Maintains data integrity and protects against attacks that exploit user input to compromise the system.

5. HTTPS Enforcement
All data communication between the client and server will be secured using HTTPS to encrypt sensitive information such as login credentials and payment data.

Why it's important: Prevents man-in-the-middle attacks and ensures that private information is not exposed during transmission.

6. CSRF Protection
Cross-Site Request Forgery (CSRF) protection mechanisms are applied to ensure that API requests originate from legitimate users and not malicious third-party sites.

Why it's important: Prevents attackers from performing unwanted actions on behalf of authenticated users.

## CI/CD Pipeline
A CI/CD (Continuous Integration/Continuous Deployment) pipeline is an automated workflow that allows developers to integrate code changes, test them, and deploy them to production more efficiently and reliably. In this project, the CI/CD pipeline ensures that every code commit is automatically tested, built, and deployed, reducing manual errors and maintaining code quality throughout the development lifecycle.

Tools and technologies include:
  GitHub Actions: Automates workflows for testing and deployment on every push or pull request.
  Docker: Containers ensure consistency between development, testing, and production environments.
  Docker Compose: Manages multi-container setups (e.g., app + database).
  Heroku / Render / AWS (Optional): Could be used for automatic deployment and hosting.
  
Their benefits include: 
  Improved Code Quality: Automated tests run on each push, catching bugs early.
  Faster Delivery: Code changes are deployed more frequently and reliably.
  Team Collaboration: Helps teams coordinate development efforts by detecting integration issues early.
