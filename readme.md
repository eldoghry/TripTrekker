# ✈️ Project Name: TripTrekker

_A lightweight, smart flight search and booking system._

### Index

### 📌 Vision

To empower travelers worldwide by providing a fast, reliable, and intelligent platform that finds the best flights based on their preferences, helping them make confident travel decisions.

### 🎯 Mission

Our mission is to simplify flight discovery and booking through an intuitive, data-driven, and user friendly experience — optimizing for cost, convenience, and personalization.

### 🎯 Goals

- Provide real-time, accurate flight search results.

- Suggest personalized or "ideal" flight options based on user preferences.

- Enable secure and seamless flight bookings.

- Integrate with Online Flight Data Integration (via Amedse API).

- Maintain a high-performance, scalable system with global reach.

### ✅ Functional Requirements

1. Flight Search

   - Users can search by airport, destination, dates, passenger count, and cabin class.
   - Supports one-way, round-trip, and multi-city.

2. Ideal Flight Suggestions

   - Show top flights based on cost, duration, number of stops, or preferences (e.g., "best", "cheapest", "fastest").

3. Booking System

   - Users can book flights.

4. User Account Management

   - Sign up & log in.
   - view bookings.
   - save preferences.
   - like flights.

5. Notifications
   - Price alerts, booking confirmations via email or SMS.

### 🚫 Non-Functional Requirements

- **Performance**: Search results should load fast.

- **Scalability**: Support concurrent access.

- **Security**: PCI compliance for payment data; secure APIs (HTTPS, OAuth).

- **Availability**: 99.9% uptime SLA.

- **Usability**: Mobile-first design; responsive UI; accessible.

### 🧑‍🤝‍🧑 Actors

- **Traveler (User)**: Searches, views, and books flights.

- **Admin**: Manages system settings, partners, and logs.

- **Third-Party Providers (Amedse API)**: Provides real-time flight search and booking data.
- **Payment Gateway**: Processes payment.

### 🔍 Assumptions

- Airline APIs are reliable and provide up-to-date availability.

- Users have internet access and mobile or desktop browsers.

- Initial scope targets individual travelers, not corporate booking.

### 📌 Constraints

- System depends on the availability and accuracy of Amedse API.

- Limited to routes and carriers supported by Amedse.

### 📘 Use Cases

#### Use Case 1: Search for Flights

**Actor:** User

**Trigger:** User enters trip details and clicks “Search”

**Flow:**

1. User provides origin, destination, date(s), and passenger info.

2. System calls flight APIs.

3. System returns list of available flights.

#### Use Case 2: View Ideal Flights

**Actor:** User

**Trigger:** After search results load

**Flow:**

1. System analyzes search results.

2. Highlights ideal options (e.g., best price, shortest trip).

3. User clicks on a suggested flight for more details.

#### Use Case 3: Book a Flight

**Actor:** User

**Trigger:** User selects a flight to book

**Flow:**

1. User provides passenger and payment info.

2. System processes booking.

3. Confirmation is displayed and sent via email/SMS.

### 🔌 External Integrations

- amadeus api
- paypal or strip

### Links & Reference

- https://developers.amadeus.com
