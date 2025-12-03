# Tal3a (طلعه) - Friend Location Tracking App

<div align="center">

**A fun, friendly group location tracking application for small groups**

Arabic: طلعه means "a group outing / hangout trip"

[Features](#features) • [Setup](#setup) • [Usage](#usage) • [Development](#development)

</div>

---

## 📖 Overview

Tal3a is a **free MVP** for tracking friends in real-time on a map. Perfect for:
- Weekend trips with friends
- Festival meetups
- Family outings
- Group adventures

**Free for up to 10 people per room** with no paid services required!

## ✨ Features

### 🔐 Authentication
- Email/password signup and login via Supabase Auth
- Profile creation with customizable display names
- Avatar selection (10+ default options + custom upload)

### 👥 Groups / Rooms
- Create unlimited groups with unique invite codes
- Join groups via 8-character invite codes
- Max 10 members per group (configurable)
- View all your groups in one place

### 📍 Real-time Location Sharing
- Live location updates every 3 seconds (configurable)
- Smart delta threshold (only sends when you move >5 meters)
- Automatic reconnection with exponential backoff
- No historical location storage (privacy-first)

### 🗺️ Interactive Map
- Leaflet + OpenStreetMap integration
- Custom avatar markers with names
- Auto-fit zoom to include all active members
- Popup with member info and last update time

### 🔒 Privacy Controls
- Toggle location sharing on/off instantly
- Temporary sharing (15, 30, or 60 minutes)
- Indefinite sharing option
- Clear consent modal explaining data collection
- Only group members can see your location

### 🎨 Modern UI
- Mobile-first responsive design
- Tailwind CSS with custom primary/accent colors
- Smooth animations and transitions
- Arabic RTL support for branding

## 🚀 Quick Start

### Prerequisites

- Node.js 18+ and npm/yarn
- A Supabase account (free tier works!)
- Modern web browser with geolocation support

### Installation

1. **Clone or download this project:**

```bash
cd Tal3a
```

2. **Install dependencies:**

```bash
npm install
```

3. **Set up Supabase:**

   a. Create a new project at [supabase.com](https://supabase.com)
   
   b. Get your project URL and anon key from Settings > API
   
   c. Create `.env` file (copy from `.env.example`):
   
   ```bash
   VITE_SUPABASE_URL=https://your-project.supabase.co
   VITE_SUPABASE_ANON_KEY=your-anon-key-here
   VITE_MAP_TILES_URL=https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png
   VITE_APP_NAME=Tal3a
   VITE_MAX_ROOM_MEMBERS=10
   VITE_LOCATION_UPDATE_INTERVAL=3000
   ```

4. **Run the database migrations:**

   a. Open Supabase SQL Editor
   
   b. Copy the entire contents of `migrations.sql`
   
   c. Execute the SQL
   
   d. This creates all tables, RLS policies, and triggers

5. **Create the avatars storage bucket:**

   a. Go to Supabase Storage
   
   b. Create a new public bucket named `avatars`
   
   c. The SQL migrations already set up the policies

6. **Enable Realtime:**

   a. Go to Database > Replication
   
   b. Enable realtime for `group_members` table (optional, for member updates)

7. **Start the development server:**

```bash
npm run dev
```

8. **Open http://localhost:3000** in your browser

## 📱 Usage

### Creating Your First Group

1. **Sign up** with email and password
2. **Choose an avatar** (or skip for now)
3. **Create a group** with a name
4. **Share the invite code** with friends
5. **Enable location sharing** in the group
6. **See everyone on the map** in real-time!

### Joining a Group

1. **Get the invite code** from a friend
2. Click **"Join Group"**
3. Enter the **8-character code**
4. You're in! Start sharing your location

### Privacy Best Practices

- Only share location when actively meeting up
- Use temporary sharing (15-60 min) for events
- Stop sharing when you're done
- Review group members regularly

## 🛠️ Development

### Project Structure

```
Tal3a/
├── src/
│   ├── components/
│   │   ├── ui/              # Reusable UI components
│   │   ├── map/             # Map-related components
│   │   └── location/        # Location tracking logic
│   ├── hooks/               # Custom React hooks
│   ├── lib/                 # Supabase client and utilities
│   ├── pages/               # Page components (routes)
│   ├── types/               # TypeScript type definitions
│   ├── App.tsx              # Main app with routing
│   ├── main.tsx             # Entry point
│   └── index.css            # Global styles (Tailwind)
├── public/
│   └── avatars/             # Default avatar images
├── migrations.sql           # Database schema
├── package.json
├── tailwind.config.js
├── tsconfig.json
└── vite.config.ts
```

### Key Technologies

- **Frontend:** React 18 + TypeScript + Vite
- **Styling:** Tailwind CSS
- **Backend:** Supabase (Auth, Database, Realtime, Storage)
- **Maps:** Leaflet + React-Leaflet + OpenStreetMap
- **Routing:** React Router v6
- **State:** React Hooks (no external state management)
- **Testing:** Vitest + React Testing Library

### Available Scripts

```bash
npm run dev        # Start dev server (port 3000)
npm run build      # Build for production
npm run preview    # Preview production build
npm run lint       # Lint code with ESLint
npm run format     # Format code with Prettier
npm test           # Run tests with Vitest
```

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `VITE_SUPABASE_URL` | Supabase project URL | (required) |
| `VITE_SUPABASE_ANON_KEY` | Supabase anonymous key | (required) |
| `VITE_MAP_TILES_URL` | Map tile server URL | OpenStreetMap |
| `VITE_MAX_ROOM_MEMBERS` | Max members per group | 10 |
| `VITE_LOCATION_UPDATE_INTERVAL` | Location update frequency (ms) | 3000 |

## 🧪 Testing

Run unit tests:

```bash
npm test
```

Run tests in watch mode:

```bash
npm test -- --watch
```

## 📦 Building for Production

1. **Build the app:**

```bash
npm run build
```

2. **Test the production build:**

```bash
npm run preview
```

3. **Deploy** the `dist` folder to your hosting service:
   - Vercel
   - Netlify
   - GitHub Pages
   - Any static hosting

## 🔐 Security & Privacy

### Data We Collect
- Email and password (hashed by Supabase)
- Display name and avatar
- Real-time location (only when sharing is enabled)
- Last known location (optional, for offline fallback)

### What We Don't Collect
- Location history
- Location when sharing is disabled
- Any data after you leave a group

### Row Level Security (RLS)
All database tables have RLS enabled:
- Users can only see their own profile
- Users can only see members of groups they're in
- Location data only visible to group members
- Only group owners can delete groups

## ⚠️ Important Notices

### OpenStreetMap Tiles

This app uses **free OpenStreetMap tiles** by default. Please note:

- **Fair use policy applies** - heavy usage may be rate-limited
- **Not for production at scale** - consider paid alternatives:
  - Mapbox (generous free tier)
  - Maptiler
  - Stadia Maps
  - Self-hosted tile server

Change tile provider in `.env`:
```bash
VITE_MAP_TILES_URL=https://your-tile-server/{z}/{x}/{y}.png
```

### Geolocation Accuracy

- Accuracy varies by device and environment
- Indoor accuracy is typically lower
- GPS may drain battery faster
- Some browsers require HTTPS for geolocation

## 🤝 Contributing

This is an MVP project. Feel free to:
- Report bugs
- Suggest features
- Submit pull requests
- Share feedback

## 📄 License

MIT License - feel free to use this project for personal or commercial purposes.

## 🙏 Acknowledgments

- **Supabase** for amazing BaaS
- **OpenStreetMap** contributors
- **Leaflet** for the map library
- **Tailwind CSS** for beautiful styling

---

<div align="center">

**Built with ❤️ for fun group adventures**

طلعه - Let's go on an adventure!

</div>
# Tal3a-app
