# Airbnb Clone Backend — Technical & Functional Requirements

## Overview

This document outlines the **technical and functional requirements** for core backend features of the Airbnb Clone project.
The backend follows a **RESTful API architecture**, built using **Node.js with Express** (or Django if preferred), and **PostgreSQL** for persistent data storage.
Authentication and authorization are handled via **JWT (JSON Web Tokens)**, with passwords securely hashed using **bcrypt**.

---

## 1️⃣ User Authentication

### **Objective**

Enable secure registration, login, and user session management.

### **API Endpoints**

| Method | Endpoint        | Description                      |
| ------ | --------------- | -------------------------------- |
| POST   | `/api/register` | Register a new user              |
| POST   | `/api/login`    | Authenticate a user              |
| GET    | `/api/profile`  | Fetch authenticated user details |

### **Input Specifications**

#### `/api/register`

```json
{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "StrongPassword123!"
}
```

### **Output**

* **Success (201):**

```json
{
  "message": "User registered successfully",
  "userId": "a1b2c3d4",
  "token": "<JWT_TOKEN>"
}
```

* **Error (400):**

```json
{
  "error": "Email already exists"
}
```

### **Validation Rules**

* Name: Required, 3–50 characters
* Email: Valid email format, unique
* Password: Minimum 8 characters, at least one uppercase, one lowercase, one number

### **Performance Criteria**

* Registration should complete within 1 second.
* JWT token should expire after 24 hours.

---

## 2️⃣ Property Management

### **Objective**

Allow hosts to create, update, and manage property listings.

### **API Endpoints**

| Method | Endpoint              | Description             |
| ------ | --------------------- | ----------------------- |
| POST   | `/api/properties`     | Add new property        |
| GET    | `/api/properties/:id` | Get property details    |
| PUT    | `/api/properties/:id` | Update property details |
| DELETE | `/api/properties/:id` | Delete property         |

### **Input Specifications**

#### `/api/properties`

```json
{
  "title": "Cozy Apartment in Nairobi",
  "description": "2-bedroom apartment with Wi-Fi and parking.",
  "price_per_night": 50,
  "location": "Nairobi, Kenya",
  "images": ["image1.jpg", "image2.jpg"]
}
```

### **Output**

* **Success (201):**

```json
{
  "message": "Property created successfully",
  "propertyId": "prop_001"
}
```

* **Error (400):**

```json
{
  "error": "Invalid property data"
}
```

### **Validation Rules**

* Title: Required, max 100 chars
* Price per night: Numeric, > 0
* Location: Required
* Images: Optional, must be valid URLs

### **Performance Criteria**

* Property retrieval under 500ms
* File uploads handled via cloud storage (e.g., AWS S3)

---

## 3️⃣ Booking System

### **Objective**

Enable users to book available properties and manage reservations.

### **API Endpoints**

| Method | Endpoint                     | Description                 |
| ------ | ---------------------------- | --------------------------- |
| POST   | `/api/bookings`              | Create a new booking        |
| GET    | `/api/bookings/:id`          | Get booking details         |
| GET    | `/api/bookings/user/:userId` | Get all bookings for a user |
| DELETE | `/api/bookings/:id`          | Cancel booking              |

### **Input Specifications**

#### `/api/bookings`

```json
{
  "userId": "a1b2c3d4",
  "propertyId": "prop_001",
  "check_in": "2025-06-01",
  "check_out": "2025-06-05"
}
```

### **Output**

* **Success (201):**

```json
{
  "message": "Booking confirmed",
  "bookingId": "bkg_2025_001"
}
```

* **Error (400):**

```json
{
  "error": "Property not available for selected dates"
}
```

### **Validation Rules**

* Dates: Check-out must be after check-in
* Property: Must exist and be available
* User: Must be authenticated

### **Performance Criteria**

* Booking confirmation within 1 second
* Prevent overlapping bookings via atomic transaction locks

---

## 4️⃣ Payment Processing

### **Objective**

Handle secure and reliable payments for bookings.

### **API Endpoints**

| Method | Endpoint            | Description             |
| ------ | ------------------- | ----------------------- |
| POST   | `/api/payments`     | Initiate payment        |
| GET    | `/api/payments/:id` | Retrieve payment status |

### **Input Specifications**

#### `/api/payments`

```json
{
  "bookingId": "bkg_2025_001",
  "amount": 200,
  "paymentMethod": "credit_card"
}
```

### **Output**

* **Success (200):**

```json
{
  "message": "Payment processed successfully",
  "paymentId": "pay_001",
  "status": "confirmed"
}
```

* **Error (402):**

```json
{
  "error": "Payment failed, insufficient funds"
}
```

### **Validation Rules**

* Booking must exist and belong to authenticated user
* Amount must match booking total
* Payment method must be supported

### **Performance Criteria**

* Payment gateway response < 2 seconds
* Handle retries on transient failures
