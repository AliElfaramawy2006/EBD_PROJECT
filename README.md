# CampusMarket


**Course:** Electronic Business Development (BINF 503) · Winter 2026
**Instructor:** Dr. Nourhan Hamdi
**Teaching Assistants:** Mr. Nour Gaser, Mr. Omar Alaa, Ms. Mariam Khalid, Mr. Younes Zied, Mr. Mahmoud Hani

## 1. Team
| Name | Student ID | Tutorial group | GitHub username |
|---|---|---|---|
| Ali Elfaramawy | 16002753 | T6 | AliElFaramawy2006 |
| Omar Ahmed Saleh | 16001575 | T2 | omarsaleh24680-cyber |
| Youssef Abdelbaset | 16001329 | T7 | youssef414 |
| Omar Elsayed | 16002170 | T2 | omaraelsayed2006-creator |
| Mennatallah Mohamed | 16008687 | T2 | nanomoha2006-coder |


## 2. The idea
CampusMarket is a web application designed for university students to buy and sell second-hand products within their university community. Students can create accounts, publish products they want to sell, browse available listings, send purchase requests, manage incoming requests, and update their personal profiles. The platform aims to provide students with an easy, affordable, and convenient way to exchange products such as textbooks, calculators, laptops, and other university essentials.



## 3. Features

### 3.1 The full product
- **User Registration and Login:** Students can create accounts, log in securely, and manage their personal profiles.

- **Product Listings:** Students can publish products for sale, including titles, descriptions, prices, categories, and images.

- **Product Browsing and Search:** Users can browse available products and search or filter them by name and category.

- **Purchase Requests:** Students can send requests to purchase products listed by other students.

- **Request Management:** Sellers can view incoming purchase requests and accept or reject them.

- **User Profiles:** Students can update their personal information and view their own published listings.

- **Product Availability Management:** Sellers can update product availability when an item is sold or no longer available.

- **Future Features:** The platform could eventually include in-app messaging, notifications, online payments, and delivery tracking.
 



### 3.2 The use cases we will build


| # | Use case | What the user does | What they see | What is stored |
|---|---|---|---|---|
| 1 | Registration and login | Registers with name, email and password; logs in with email and password | Their home page, with their name in the header | A User, with the password hashed |
| 2 | Manage Product Listings | Creates, edits, and deletes product listings with a title, description, price, and category | A list of their published products and confirmation of changes | Listing documents containing product details and seller ID |
| 3 | Browse Products and Send Purchase Requests | Browses available products, views product details, and sends a request to buy a product | Available products, product details, and confirmation that the request was submitted | PurchaseRequest document containing buyer ID, seller ID, listing ID, and request status |
| 4 | Manage Purchase Requests | Views incoming requests and accepts or rejects purchase requests | A list of incoming requests with their updated statuses | Updated PurchaseRequest documents with accepted or rejected status |
| 5 | Manage User Profile | Views and updates personal information and can delete their account | Their profile information and confirmation of successful updates or account deletion | Updated or deleted User document containing name, email, and password hash |

## 4. Who owns what

| Member | Use case |
|---|---|
| Omar Elsayed | 1. Registration and login |
| Ali Elfaramawy | 2. Manage Product Listings |
| Mennatallah Mohamed | 3. Browse Products and Send Purchase Requests |
| Youssef Abdelbaset | 4. Manage Purchase Requests |
| Omar Ahmed Saleh | 5. Manage User Profile |

## 5. Data model

### User


```js
const userSchema = new mongoose.Schema({
  name: { type: String, required: true },
  email: { type: String, required: true, unique: true },
  password: { type: String, required: true }, // stored hashed, never as plain text
});
```
### Listing

```js
const listingSchema = new mongoose.Schema({
  title: { type: String, required: true },
  description: { type: String, required: true },
  price: { type: Number, required: true, min: 0 },
  category: { type: String, required: true },
  image: { type: String },
  seller: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  status: {
    type: String,
    enum: ['AVAILABLE', 'SOLD'],
    default: 'AVAILABLE'
  }
}, { timestamps: true });
```
### PurchaseRequest

```js
const purchaseRequestSchema = new mongoose.Schema({
  buyer: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  seller: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'User',
    required: true
  },
  listing: {
    type: mongoose.Schema.Types.ObjectId,
    ref: 'Listing',
    required: true
  },
  status: {
    type: String,
    enum: ['PENDING', 'ACCEPTED', 'REJECTED'],
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
