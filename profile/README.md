# RoomFit - No-Equipment Home Workout Program

A full-stack web application for tracking no-equipment home workouts with a React frontend and Node.js/Express backend.

## Project Structure

```
Roomfit/
├── frontend/                 # React + Tailwind CSS application
│   ├── public/
│   │   └── index.html       # HTML entry point
│   ├── src/
│   │   ├── components/      # Reusable React components
│   │   │   ├── Navigation.jsx
│   │   │   └── ExerciseCard.jsx
│   │   ├── pages/          # Page components
│   │   │   ├── Landing.jsx
│   │   │   ├── Program.jsx
│   │   │   └── Community.jsx
│   │   ├── App.jsx         # Main app component
│   │   ├── index.css       # Tailwind + global styles
│   │   └── main.jsx        # React entry point
│   ├── package.json
│   ├── tailwind.config.js
│   └── postcss.config.js
│
└── backend/                 # Express.js API server
    ├── models/             # Mongoose schemas
    │   ├── User.js
    │   ├── Workout.js
    │   └── Exercise.js
    ├── routes/             # API endpoints
    │   ├── users.js
    │   └── workouts.js
    ├── server.js          # Main server file
    ├── .env               # Environment variables
    └── package.json
```

## Features

### Frontend (React + Tailwind CSS)

- **Landing Page**: Join the program with your name
- **Program Page**: 7-day workout plan with detailed exercises
- **Community Page**: Leaderboard showing member streaks
- **Navigation**: Fixed navbar with user info and logout
- **Exercise Cards**: Display exercise details with type badges and video links
- **Check-in System**: Mark workouts as complete

### Backend (Express + MongoDB)

- **User Management**: Create users, track stats (streak, total workouts)
- **Workout Tracking**: Check-in for daily workouts
- **Progress Tracking**: Get weekly progress and statistics
- **Leaderboard**: Rank users by streak and total workouts
- **Exercise Management**: Store and retrieve workout exercises

## Setup Instructions

### Prerequisites

- Node.js 16+ and npm
- MongoDB (local or cloud)
- Git

### Backend Setup

1. **Navigate to backend folder**

   ```bash
   cd backend
   npm install
   ```

2. **Configure environment variables**
   Edit `.env`:

   ```
   PORT=5000
   NODE_ENV=development
   MONGODB_URI=mongodb://localhost:27017/roomfit
   CORS_ORIGIN=http://localhost:3000
   ```

3. **Start MongoDB**

   ```bash
   # If using local MongoDB
   mongod
   ```

4. **Run the backend**
   ```bash
   npm start          # Production
   npm run dev        # Development with nodemon
   ```
   Server runs on `http://localhost:5000`

### Frontend Setup

1. **Navigate to frontend folder**

   ```bash
   cd frontend
   npm install
   ```

2. **Create `.env` file** (optional, defaults to localhost:5000)

   ```
   REACT_APP_API_URL=http://localhost:5000/api
   ```

3. **Start the development server**
   ```bash
   npm start
   ```
   App runs on `http://localhost:3000`

## API Endpoints

### Users

- `POST /api/users` - Create new user (join program)
- `GET /api/users/leaderboard` - Get top users sorted by streak
- `GET /api/users/:userId` - Get user details
- `PUT /api/users/:userId` - Update user info

### Workouts

- `POST /api/workouts/:userId/checkin` - Check in for a workout
- `GET /api/workouts/:userId/progress` - Get weekly progress
- `GET /api/workouts/:userId` - Get user's workouts (with optional date range)
- `GET /api/workouts/:userId/stats` - Get workout statistics

## Database Models

### User

```javascript
{
  id: String (UUID),
  name: String,
  streak: Number,
  totalWorkouts: Number,
  workoutsThisWeek: [String],
  createdAt: Date,
  updatedAt: Date
}
```

### Workout

```javascript
{
  userId: String,
  day: String (mon-sun),
  date: Date,
  completed: Boolean,
  duration: Number,
  notes: String,
  createdAt: Date,
  updatedAt: Date
}
```

### Exercise

```javascript
{
  name: String,
  description: String,
  reps: String,
  sets: Number,
  duration: String,
  type: String (strength|cardio|core|fat|stretch),
  videoUrl: String,
  day: String (mon-sun),
  section: String (warmup|main|cooldown),
  order: Number,
  createdAt: Date,
  updatedAt: Date
}
```

## Styling

The project uses **Tailwind CSS** with custom color configuration:

- **Dark Theme**: `#0d0d0d` background
- **Accent Color**: `#e8ff00` (neon yellow)
- **Secondary Accent**: `#ff6b35` (orange)
- **Custom Fonts**: Bebas Neue (display), DM Sans (body), DM Mono (code)

All styles are configured in `frontend/tailwind.config.js` and global styles in `frontend/src/index.css`.

## Running Both Services

### Development Mode (Two Terminals)

**Terminal 1 - Backend:**

```bash
cd backend
npm run dev
```

**Terminal 2 - Frontend:**

```bash
cd frontend
npm start
```

## Building for Production

### Frontend

```bash
cd frontend
npm run build
```

Creates optimized build in `frontend/build/`

### Backend

No build step needed - just ensure Node.js 16+ is installed on production server.

## Next Steps / Enhancements

- [ ] User authentication (JWT/OAuth)
- [ ] Exercise customization and notes
- [ ] Weekly statistics and charts
- [ ] Social features (friend requests, challenges)
- [ ] Mobile app (React Native)
- [ ] Push notifications for daily workouts
- [ ] Workout history and analytics
- [ ] Custom workout plans

## License

ISC
