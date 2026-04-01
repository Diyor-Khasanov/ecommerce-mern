# 🛒 E-Commerce Store with Admin Dashboard

A full-stack **MERN** e-commerce application featuring a complete shopping experience for customers and a powerful admin dashboard for store management. Built with **MongoDB**, **Express.js**, **React** (Vite), and **Node.js** — with Stripe payments, Redis caching, Cloudinary image hosting, and JWT-based authentication.

🔗 **Live Demo:** [ecommerce-mern-gamma-cyan.vercel.app](https://ecommerce-mern-gamma-cyan.vercel.app)

---

## ✨ Features

### 🛍️ Customer-Facing
- Browse and search products by category
- Product detail pages with images
- Shopping cart — add, update, and remove items
- Secure checkout powered by **Stripe**
- User registration and login with JWT authentication
- Protected routes for authenticated users

### 🔐 Authentication & Security
- JWT-based auth with **HTTP-only cookies**
- Password hashing with **bcryptjs**
- Role-based access control (customer vs. admin)
- Access token refresh via **Redis** (ioredis)

### 🛠️ Admin Dashboard
- Manage products — create, update, delete
- Upload and manage product images via **Cloudinary**
- View and manage all customer orders
- Sales analytics and revenue overview

### ⚙️ Backend & Infrastructure
- RESTful API built with **Express.js**
- **MongoDB** database via Mongoose ODM
- **Redis** (ioredis) for session/token caching and performance
- **Cloudinary** for cloud image storage
- Environment-based configuration via **dotenv**

---

## 🛠️ Tech Stack

### Backend
| Technology | Purpose |
|---|---|
| Node.js + Express.js | REST API server |
| MongoDB + Mongoose | Database & ODM |
| Redis (ioredis) | Caching & token store |
| Stripe | Payment processing |
| Cloudinary | Image upload & storage |
| jsonwebtoken | Authentication |
| bcryptjs | Password hashing |
| cookie-parser | Cookie management |
| dotenv | Environment config |
| nodemon | Dev auto-reload |

### Frontend
| Technology | Purpose |
|---|---|
| React + Vite | UI framework & build tool |
| React Router | Client-side routing |
| Zustand / Context | State management |
| Tailwind CSS | Styling |
| Axios | API communication |

---

## 📁 Project Structure

```
ecommerce-mern/
├── backend/
│   ├── controllers/        # Route handler logic
│   │   ├── auth.controller.js
│   │   ├── product.controller.js
│   │   ├── cart.controller.js
│   │   ├── order.controller.js
│   │   ├── payment.controller.js
│   │   └── analytics.controller.js
│   ├── models/             # Mongoose schemas
│   │   ├── user.model.js
│   │   ├── product.model.js
│   │   └── order.model.js
│   ├── routes/             # API route definitions
│   │   ├── auth.route.js
│   │   ├── product.route.js
│   │   ├── cart.route.js
│   │   ├── order.route.js
│   │   ├── payment.route.js
│   │   └── analytics.route.js
│   ├── middleware/         # Auth & error middleware
│   ├── lib/                # DB, Redis, Cloudinary, Stripe setup
│   └── server.js           # App entry point
├── frontend/
│   ├── src/
│   │   ├── components/     # Reusable UI components
│   │   ├── pages/          # Route-level pages
│   │   ├── stores/         # State management
│   │   └── main.jsx        # React entry point
│   └── package.json        # Frontend dependencies
├── package.json            # Root (backend) package
└── .gitignore
```

---

## 🚀 Getting Started

### Prerequisites

- **Node.js** v18+
- **npm** v9+
- **MongoDB** (local or [MongoDB Atlas](https://www.mongodb.com/atlas))
- **Redis** (local or [Upstash](https://upstash.com))
- **Stripe** account — [stripe.com](https://stripe.com)
- **Cloudinary** account — [cloudinary.com](https://cloudinary.com)

### 1. Clone the repository

```bash
git clone https://github.com/Diyor-Khasanov/ecommerce-mern.git
cd ecommerce-mern
```

### 2. Configure environment variables

Create a `.env` file in the **project root**:

```env
# Server
PORT=5000
NODE_ENV=development

# MongoDB
MONGO_URI=your_mongodb_connection_string

# Redis
UPSTASH_REDIS_URL=your_redis_url

# JWT
ACCESS_TOKEN_SECRET=your_access_token_secret
REFRESH_TOKEN_SECRET=your_refresh_token_secret
ACCESS_TOKEN_EXPIRY=15m
REFRESH_TOKEN_EXPIRY=7d

# Cloudinary
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret

# Stripe
STRIPE_SECRET_KEY=your_stripe_secret_key
STRIPE_WEBHOOK_SECRET=your_stripe_webhook_secret

# Frontend URL (for CORS)
CLIENT_URL=http://localhost:5173
```

### 3. Install dependencies & build

```bash
# Installs root + frontend deps and builds the React app
npm run build
```

### 4. Run in development

```bash
# Backend with hot-reload (nodemon)
npm run dev
```

The backend will be available at `http://localhost:5000`.  
The frontend dev server (Vite) runs at `http://localhost:5173`.

---

## 📜 Available Scripts

| Command | Description |
|---|---|
| `npm run dev` | Start backend with nodemon (development) |
| `npm start` | Start backend with node (production) |
| `npm run build` | Install all deps & build frontend for production |

---

## 🔌 API Endpoints

| Method | Endpoint | Description | Auth Required |
|---|---|---|---|
| POST | `/api/auth/signup` | Register new user | Public |
| POST | `/api/auth/login` | Login & receive tokens | Public |
| POST | `/api/auth/logout` | Logout user | User |
| POST | `/api/auth/refresh-token` | Refresh access token | Public |
| GET | `/api/products` | Get all products | Public |
| GET | `/api/products/:id` | Get single product | Public |
| POST | `/api/products` | Create product | Admin |
| PUT | `/api/products/:id` | Update product | Admin |
| DELETE | `/api/products/:id` | Delete product | Admin |
| GET | `/api/cart` | Get user's cart | User |
| POST | `/api/cart` | Add item to cart | User |
| DELETE | `/api/cart` | Remove cart item | User |
| POST | `/api/payment/create-checkout-session` | Create Stripe session | User |
| POST | `/api/payment/checkout-success` | Handle payment success | User |
| GET | `/api/orders` | Get user orders | User |
| GET | `/api/analytics` | Get store analytics | Admin |

---

## 💳 Stripe Test Cards

Use these card numbers to test payments in development:

| Scenario | Card Number |
|---|---|
| Success | `4242 4242 4242 4242` |
| Declined | `4000 0000 0000 0002` |
| Requires auth | `4000 0025 0000 3155` |

Use any future expiry date, any 3-digit CVC, and any ZIP code.

---

## 🌐 Deployment

This project is deployed as a **monorepo on Vercel**. The build command installs all dependencies and builds the React frontend, which the Express server then serves as static files in production.

To deploy your own instance:

1. Fork this repository
2. Import the repo into [Vercel](https://vercel.com)
3. Add all environment variables in Vercel project settings
4. Set the **build command** to: `npm run build`
5. Set the **output directory** to: `frontend/dist`
6. Click **Deploy**

---

## 🤝 Contributing

Contributions are welcome!

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add your feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](./LICENSE) file for details.

---

## 👤 Author

**Diyor Khasanov**
- GitHub: [@Diyor-Khasanov](https://github.com/Diyor-Khasanov)
