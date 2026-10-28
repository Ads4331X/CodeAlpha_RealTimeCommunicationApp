# SwiftChat - Real-Time Communication App

A full-stack real-time chat application with voice/video calling, built for the CodeAlpha internship. Supports instant messaging, media sharing, user authentication, and WebRTC-based calls across mobile (React Native/Expo) and web platforms.

## Features

- **Real-time Messaging** - Instant one-to-one and group chat powered by Socket.IO
- **Voice & Video Calls** - WebRTC peer-to-peer calling with STUN/TURN support
- **User Authentication** - JWT-based auth with email verification via Nodemailer
- **Media Sharing** - Send images, videos, and files via Cloudinary
- **Profile Management** - Update profile, avatar, and user settings
- **Online Status** - Real-time presence tracking
- **Secure** - Password encryption with bcrypt, rate limiting, and secure token handling
- **Cross-platform** - React Native frontend for iOS/Android, Express backend API

## Tech Stack

### Backend
- **Runtime**: Node.js with TypeScript
- **Framework**: Express.js
- **Real-time**: Socket.IO
- **Database**: PostgreSQL with Prisma ORM
- **Auth**: JWT (jsonwebtoken) + bcryptjs
- **File Storage**: Cloudinary
- **Email**: Nodemailer (Gmail)
- **Validation**: Validator.js

### Frontend
- **Framework**: React Native with Expo Router
- **Real-time**: Socket.IO Client
- **WebRTC**: react-native-webrtc
- **State/UI**: NativeWind (TailwindCSS), React Hook Form
- **Media**: Expo Image Picker, Vision Camera, FFmpeg
- **Storage**: Expo Secure Store, SQLite

## Project Structure

```
.
├── backend/          # Express API server with Socket.IO
│   ├── src/
│   │   ├── controllers/  # Route handlers
│   │   ├── routes/       # API routes
│   │   ├── socket.ts     # Socket.IO logic
│   │   ├── server.ts     # Entry point
│   │   └── prisma/       # Database schema & migrations
│   └── .env.example
└── frontend/         # React Native Expo app
    ├── app/             # Expo Router pages
    ├── components/      # Reusable components
    ├── context/         # React Context providers
    └── .env.example
```

## Getting Started

### Prerequisites
- Node.js (v18+)
- PostgreSQL
- Cloudinary account (for media uploads)
- Gmail account with app password (for email verification)

### Backend Setup

1. Navigate to backend directory:
```bash
cd backend
```

2. Install dependencies:
```bash
npm install
```

3. Copy environment variables:
```bash
cp .env.example .env
```

4. Update `.env` with your credentials (DATABASE_URL, JWT_SECRET, Cloudinary keys, etc.)

5. Run Prisma migrations:
```bash
npx prisma migrate dev
```

6. Start the server:
```bash
npm start
```

Server runs on `http://localhost:3000` by default.

### Frontend Setup

1. Navigate to frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Copy environment variables:
```bash
cp .env.example .env
```

4. Update `.env`:
- `EXPO_PUBLIC_API_URL` - Your backend URL (use LAN IP for physical devices)
- WebRTC STUN/TURN server configs (optional for local development)

5. Start the app:
```bash
npm start
```

For LAN testing on physical devices:
```bash
npm run start:lan
```

## Testing

Backend tests:
```bash
cd backend
npm test
```

Frontend tests:
```bash
cd frontend
npm test
```

## Environment Variables

See `.env.example` files in both `backend/` and `frontend/` directories for required configuration.

## License

This project was created as part of CodeAlpha internship program.
