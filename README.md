# 🏟️ SportNest — Server

> Backend API server for **SportNest**, a modern sports facility booking platform.

---

## 🧰 Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js |
| Framework | Express.js |
| Database | MongoDB |
| ODM | Mongoose |
| Auth | Better Auth |
| Environment | dotenv |

---

## 📁 Project Structure

```
server/
├── src/
│   ├── controllers/       # Route handler logic
│   │   ├── facility.controller.js
│   │   ├── booking.controller.js
│   │   └── user.controller.js
│   ├── models/            # Mongoose schemas
│   │   ├── facility.model.js
│   │   ├── booking.model.js
│   │   └── user.model.js
│   ├── routes/            # Express route definitions
│   │   ├── facility.routes.js
│   │   ├── booking.routes.js
│   │   └── user.routes.js
│   ├── middleware/        # Auth, error, validation middleware
│   ├── lib/               # DB connection, helpers
│   └── app.js             # Express app setup
├── .env                   # Environment variables (never commit)
├── .env.example           # Example env template
├── package.json
└── server.js              # Entry point
```

---

## ⚙️ Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/your-username/sportnest-server.git
cd sportnest-server
```

### 2. Install dependencies

```bash
npm install
```

### 3. Set up environment variables

```bash
cp .env.example .env
```

Fill in your `.env`:

```env
PORT=***
MONGODB_URI=mongodb+***
CLIENT_URL=***
BETTER_AUTH_SECRET=my_secret_key
BETTER_AUTH_URL=***
```

### 4. Run the server

```bash
# Development (with hot reload)
npm run dev

# Production
npm start
```

Server runs at `http://localhost:5000`

---

## 🔌 API Endpoints

### 🏟️ Facilities

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| `GET` | `/facilities` | Get all facilities | ❌ |
| `GET` | `/featured` | Get featured facilities | ❌ |
| `GET` | `/facilities/:id` | Get single facility | ❌ |
| `POST` | `/facilities` | Create a facility | ✅ |
| `PUT` | `/facilities/:id` | Update a facility | ✅ Owner |
| `DELETE` | `/facilities/:id` | Delete a facility | ✅ Owner |

### 📅 Bookings

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| `GET` | `/bookings/my` | Get user's bookings | ✅ |
| `POST` | `/bookings` | Create a booking | ✅ |
| `DELETE` | `/bookings/:id` | Cancel a booking | ✅ Owner |

### 👤 Users

| Method | Endpoint | Description | Auth |
|--------|----------|-------------|------|
| `GET` | `/users/me` | Get current user | ✅ |
| `PUT` | `/users/me` | Update profile | ✅ |

### 🔐 Auth (Better Auth)

| Method | Endpoint | Description |
|--------|----------|-------------|
| `POST` | `/api/auth/sign-up/email` | Register with email |
| `POST` | `/api/auth/sign-in/email` | Login with email |
| `POST` | `/api/auth/sign-in/social` | OAuth (Google etc.) |
| `POST` | `/api/auth/sign-out` | Sign out |
| `GET` | `/api/auth/session` | Get current session |

---

## 🗃️ Data Models

### Facility

```js
{
  name:         String,     // required
  description:  String,
  sportType:    String,     // e.g. "Football", "Cricket"
  imageUrl:     String,
  location:     String,
  pricePerHour: Number,
  capacity:     Number,
  slots:        [String],   // e.g. ["08:00", "10:00"]
  featured:     Boolean,
  owner:        ObjectId,   // ref: User
  createdAt:    Date,
}
```

### Booking

```js
{
  facility:   ObjectId,   // ref: Facility
  user:       ObjectId,   // ref: User
  date:       Date,
  slot:       String,
  totalPrice: Number,
  status:     String,     // "pending" | "confirmed" | "cancelled"
  createdAt:  Date,
}
```

---

## 🌐 Environment Variables Reference

| Variable | Description | Example |
|----------|-------------|---------|
| `PORT` | Server port | `5000` |
| `MONGODB_URI` | MongoDB connection string | `mongodb+srv://...` |
| `CLIENT_URL` | Frontend URL for CORS | `http://localhost:3000` |
| `BETTER_AUTH_SECRET` | Auth secret key | `supersecretkey` |
| `BETTER_AUTH_URL` | Auth base URL | `http://localhost:5000` |

---

## 🚀 Deployment

### Deploy to Render / Railway

1. Push your repo to GitHub
2. Connect repo on [Render](https://render.com) or [Railway](https://railway.app)
3. Set all environment variables in the dashboard
4. Set build command: `npm install`
5. Set start command: `npm start`

> ✅ Make sure `MONGODB_URI` points to your **production** Atlas cluster and `CLIENT_URL` points to your deployed frontend.

---

## 🔒 Security Notes

- Never commit `.env` — it's in `.gitignore`
- All write endpoints require a valid session via Better Auth
- Facility edit/delete is restricted to the owner only
- CORS is configured to allow only `CLIENT_URL`

---

## 🤝 Related Repos

- **Frontend (Next.js):** [sportnest-client](https://github.com/your-username/sportnest-client)

---

## 📄 License

MIT © SportNest
