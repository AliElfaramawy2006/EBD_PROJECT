# Nema


**Course:** Electronic Business Development (BINF 503) · Winter 2026
**Instructor:** Dr. Nourhan Hamdi
**Teaching Assistants:** Mr. Nour Gaser, Mr. Omar Alaa, Ms. Mariam Khalid, Mr. Younes Zied, Mr. Mahmoud Hani

## 1. Team
| Name | Student ID | Tutorial group | GitHub username |
|---|---|---|---|
| Ali Elfaramawy | 16002753 | T6 | AliElFaramawy2006 |
| Omar Ahmed Saleh | 16001575 | T2 | omarsaleh24680-cyber |
| Youssef Abdelbaset | 16001329 | T7 | youssef414 |
| Omar Elsayed | 16002710 | T2 | omaraelsayed2006-creator |
| Mennatallah Mohamed | 16008687 | T2 | nanomoha2006-coder |


## 2. The idea
Nema is a hyperlocal surplus food rescue marketplace designed for Egyptian university students, budget-conscious households, and local food businesses (bakeries, cafes, and supermarkets). It solves the dual real-world problems of daily commercial food waste and rising meal costs by allowing partner shops to list unsold end-of-day food bundles at 50–70% off, enabling nearby users to reserve and pick them up before closing time.



## 3. Features

### 3.1 The full product
- **User Registration and Login:** Users and partner food businesses can create accounts and log in securely.

- **Business Registration and Management:** Bakeries, cafes, and supermarkets can register their businesses and manage their profiles.

- **Surplus Food Listings:** Partner businesses can publish food bundles with descriptions, discounted prices, quantities, pickup locations, and collection deadlines.

- **Browse and Search Food Bundles:** Users can browse available food bundles and filter them by category, price, and nearby location.

- **Food Bundle Reservations:** Users can reserve available food bundles and receive reservation confirmation.

- **Reservation Management:** Businesses can view incoming reservations and confirm or cancel them.

- **Pickup and Order Status:** Users and businesses can track reservation status, including reserved, ready for pickup, and collected.

- **Future Features:** The platform could eventually include online payments, push notifications, ratings and reviews, and personalized food recommendations.





### 3.2 The use cases we will build


| # | Use case | What the user does | What they see | What is stored |
|---|---|---|---|---|
| 1 | Registration and Login | Creates an account using name, email, and password, or logs in using existing credentials | Their personalized home page with their name and account information | A User document containing name, email, and securely hashed password |
| 2 | Manage Food Listings | A registered business creates, edits, or deletes surplus food bundles with descriptions, prices, quantities, and pickup deadlines | A list of published food bundles and confirmation of successful changes | FoodListing documents containing bundle details, business ID, and availability status |
| 3 | Browse Food Bundles and Make Reservations | Browses nearby available food bundles, views details, and reserves a bundle | Available bundles, discounted prices, pickup locations, and reservation confirmation | A Reservation document containing user ID, listing ID, quantity, and reservation status |
| 4 | Manage Reservations and Pickup Status | A business views incoming reservations, confirms or cancels them, and updates orders as ready for pickup or collected | A list of reservations with their current statuses | Updated Reservation documents containing confirmation and pickup status |
| 5 | Manage User and Business Profiles | Users and businesses view and update their profile information and can delete their accounts | Their updated profile information and confirmation of successful changes | Updated or deleted User and Business documents |


## 4. Who owns what

| Member | Use case |
|---|---|
| Omar Elsayed | 1. Registration and Login |
| Ali Elfaramawy | 2. Manage Food Listings |
| Mennatallah Mohamed | 3. Browse Food Bundles and Make Reservations |
| Youssef Abdelbaset | 4. Manage Reservations and Pickup Status |
| Omar Ahmed Saleh | 5. Manage User and Business Profiles |

## 5. Data model

```js
const mongoose = require('mongoose');
```

### User
```js
const userSchema = new mongoose.Schema({
  name: {
    type: String,
    required: true
  },
  email: {
    type: String,
    required: true,
    unique: true
  },
  password: {
    type: String,
    required: true
  },
  role: {
    type: String,
    enum: ['CUSTOMER', 'BUSINESS'],
    default: 'CUSTOMER'
  }
}, { timestamps: true });
```

### Business

```js
const businessSchema = new mongoose.Schema({
  owner: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  businessName: {
    type: String,
    required: true
  },
  category: {
    type: String,
    enum: ['BAKERY', 'CAFE', 'SUPERMARKET', 'OTHER'],
    required: true
  },
  address: {
    type: String,
    required: true
  },
  phone: {
    type: String,
    required: true
  }
}, { timestamps: true });
```

### FoodListing

```js
const foodListingSchema = new mongoose.Schema({
  business: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Business',
    required: true
  },
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  },
  category: {
    type: String,
    required: true
  },
  originalPrice: {
    type: Number,
    required: true,
    min: 0
  },
  discountedPrice: {
    type: Number,
    required: true,
    min: 0
  },
  quantityAvailable: {
    type: Number,
    required: true,
    min: 0
  },
  pickupAddress: {
    type: String,
    required: true
  },
  pickupDeadline: {
    type: Date,
    required: true
  },
  status: {
    type: String,
    enum: ['AVAILABLE', 'SOLD_OUT', 'EXPIRED'],
    default: 'AVAILABLE'
  }
}, { timestamps: true });
```

### Reservation

```js
const reservationSchema = new mongoose.Schema({
  user: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  business: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Business',
    required: true
  },
  foodListing: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'FoodListing',
    required: true
  },
  quantity: {
    type: Number,
    required: true,
    min: 1
  },
  totalPrice: {
    type: Number,
    required: true,
    min: 0
  },
  status: {
    type: String,
    enum: [
      'PENDING',
      'CONFIRMED',
      'CANCELLED',
      'READY_FOR_PICKUP',
      'COLLECTED'
    ],
    default: 'PENDING'
  }
}, { timestamps: true });
```




## 6. Run it locally

> Leave this section as it is until Submission 2 (Thursday 10 December 2026,
> 23:59). Then fill it in: we follow these steps to run your project.

### Back end

```bash
cd backend
npm install
# create backend/.env from backend/.env.example (see the table below)
npm start
```

The API runs on http://localhost:3000.

| Variable in `.env` | What it is |
|---|---|
| `MONGODB_URI` | The connection string of your MongoDB Atlas database |
| `JWT_SECRET` | Any long random text, used to sign login tokens |
| [Any other variable] | [What it is] |

### Front end

```bash
cd frontend
npm install
npm run dev
```

The app runs on [the address `npm run dev` prints, e.g. http://localhost:5173].
