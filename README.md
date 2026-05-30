# Aeronest 360 PG Finder

A full-stack web application to discover, list, and book Paying Guest (PG) accommodations. Users can browse properties by category, search by location or type, create their own listings, manage bookings, and maintain a wishlist.

---

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Frontend | React 18, Vite, Redux Toolkit, React Router v6, SCSS |
| Backend | Node.js, Express.js |
| Database | MongoDB + Mongoose |
| Auth | JWT + bcryptjs |
| File Upload | Multer (disk storage) |
| State Management | Redux Persist |

---

## Features

- **Auth** Register with profile photo, login with JWT
- **Browse Listings** View all PG properties, filter by category
- **Search** Search properties by title or category
- **Create Listing** Multi-photo upload, full property details (address, amenities, pricing)
- **Booking** Book properties with date range and total price calculation
- **Wishlist** Save/unsave favourite properties
- **Trip List** View all bookings made as a customer
- **Property List** Manage your own listings as a host
- **Reservation List** View bookings received as a host
- **Static Pages** About Us, Terms & Conditions, Payment Info, Refund Policy

---

## Project Structure

```
PG-Finder/
 frontend/
 pg-frontend/
 src/
 Components/ # Navbar, Footer, Listing cards, Slider
 Pages/
 Auth/ # Login, Register
 Home/ # HomePage, ListingDetails, CreateListing,
 # TripList, WishList, PropertyList,
 # ReservationList, Search, Category,
 # Payment, RefundPolicy, T&C, AboutUs
 redux/ # Redux store + state slice
 Styles/ # SCSS modules
 App.jsx
 package.json
 server/
 Controllers/
 AuthController.js # register, login
 PageListingController.js # CRUD + search listings
 BookingController.js # create booking
 UserController.js # trips, wishlist, properties, reservations
 Routes/
 authRoutes.js
 PageListingRoute.js
 BookingRoute.js
 UserRoute.js
 modals/
 UserSchema.js
 PageListingSchema.js
 BookingSchema.js
 connectDB/connect.js
 index.js
```

---

## API Endpoints

### Auth `/api/v1/auth`
| Method | Route | Description |
|--------|-------|-------------|
| POST | `/register` | Register user (with profile image) |
| POST | `/login` | Login, returns JWT |

### Properties `/api/v1/properties`
| Method | Route | Description |
|--------|-------|-------------|
| POST | `/create` | Create listing (multi-image upload) |
| GET | `/` | Get all listings (optional `?category=`) |
| GET | `/:listingId` | Get single listing |
| GET | `/search/:search` | Search by title or category |

### Bookings `/api/v1/bookings`
| Method | Route | Description |
|--------|-------|-------------|
| POST | `/create` | Create booking |

### Users `/api/v1/users`
| Method | Route | Description |
|--------|-------|-------------|
| GET | `/:userId/trips` | Get user's booked trips |
| PATCH | `/:userId/:listingId` | Toggle wishlist item |
| GET | `/:userId/properties` | Get user's own listings |
| GET | `/:userId/reservations` | Get bookings received as host |

---

## Setup & Installation

### Prerequisites
- Node.js v18+
- MongoDB (local or Atlas)

### 1. Clone the repository
```bash
git clone https://github.com/your-username/pg-finder.git
cd pg-finder
```

### 2. Backend Setup
```bash
cd server
npm install
```

Create a `.env` file in `/server`:
```env
MONGO_URI=your_mongodb_connection_string
JWT_SECERET=your_jwt_secret
```

Start the server:
```bash
npm start
# Runs on http://localhost:3000
```

### 3. Frontend Setup
```bash
cd frontend/pg-frontend
npm install
npm run dev
# Runs on http://localhost:5173
```

---

## Key Dependencies

### Backend
- `express` HTTP server
- `mongoose` MongoDB ODM
- `bcryptjs` Password hashing
- `jsonwebtoken` JWT auth
- `multer` File/image uploads
- `dotenv` Environment config
- `cors` Cross-origin requests

### Frontend
- `react-router-dom` Client-side routing
- `@reduxjs/toolkit` + `redux-persist` Global state with persistence
- `react-date-range` Date picker for bookings
- `react-icons` Icon library
- `react-hot-toast` Toast notifications
- `sass` SCSS styling

---

## Data Models

### User
`firstName`, `lastName`, `email`, `password` (hashed), `profileImagePath`, `tripList`, `whishList`, `propertyList`, `reservationList`

### Listing
`creator` (ref User), `category`, `type`, `address fields`, `guestCount`, `bedroomCount`, `bedCount`, `bathroomCount`, `amenities`, `listingPhotoPaths[]`, `title`, `description`, `highlight`, `highlightDesc`, `price`

### Booking
`customerId` (ref User), `hostId` (ref User), `listingId` (ref Listing), `startDate`, `endDate`, `totalPrice`

---


