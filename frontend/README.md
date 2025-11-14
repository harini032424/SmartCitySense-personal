# SmartCitySense Frontend

> Real-time, intelligent city dashboard built with Next.js 14, TypeScript, and Mapbox GL

## 🎨 Features

- **Real-Time Map Visualization** - Interactive Mapbox map with event clustering
- **Live Event Stream** - Auto-refreshing event feed from backend APIs
- **User Report Submission** - Upload media, geo-tag locations, AI-powered summaries
- **Predictive Alerts** - ML-generated warnings and notifications
- **Mood Map** - Sentiment analysis visualization across city zones
- **Analytics Dashboard** - Charts, trends, and city health metrics
- **Dark/Light Mode** - Full theme support
- **Firebase Authentication** - Google OAuth + Email/Password
- **Push Notifications** - Firebase Cloud Messaging integration
- **Responsive Design** - Mobile-first, works on all devices

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| Framework | Next.js 14 (App Router) |
| Language | TypeScript |
| Styling | Tailwind CSS v3, shadcn/ui |
| Map | Mapbox GL JS, Supercluster |
| State | Zustand |
| Data Fetching | React Query (TanStack Query) |
| Auth | Firebase Auth |
| Storage | Firebase Storage |
| Notifications | Firebase Cloud Messaging |
| Charts | Recharts |
| Animations | Framer Motion |
| Icons | Lucide React |

## 📦 Installation

### Prerequisites

- Node.js 18+ and npm
- Mapbox API token
- Firebase project with Auth, Storage, and FCM enabled
- Backend API running (default: http://localhost:8000)

### Step-by-Step Setup

1. **Navigate to frontend directory**
   ```bash
   cd frontend
   ```

2. **Make setup scripts executable**
   ```bash
   chmod +x setup.sh generate-components-part1.sh generate-components-part2.sh generate-components-final.sh
   ```

3. **Run setup script**
   ```bash
   ./setup.sh
   ```

4. **Generate all components**
   ```bash
   ./generate-components-part1.sh
   ./generate-components-part2.sh
   ./generate-components-final.sh
   ```

5. **Configure environment variables**
   ```bash
   cp .env.example .env.local
   ```

   Edit `.env.local` with your values:
   ```env
   # Backend API
   NEXT_PUBLIC_API_URL=http://localhost:8000

   # Mapbox Token
   NEXT_PUBLIC_MAPBOX_TOKEN=YOUR_MAPBOX_PUBLIC_TOKEN

   # Firebase Configuration
   NEXT_PUBLIC_FIREBASE_API_KEY=your_api_key
   NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=your_project.firebaseapp.com
   NEXT_PUBLIC_FIREBASE_PROJECT_ID=your_project_id
   NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=your_project.appspot.com
   NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=your_sender_id
   NEXT_PUBLIC_FIREBASE_APP_ID=your_app_id
   NEXT_PUBLIC_FIREBASE_MEASUREMENT_ID=your_measurement_id
   NEXT_PUBLIC_FIREBASE_VAPID_KEY=your_vapid_key

   # Default Coordinates (Bengaluru)
   NEXT_PUBLIC_DEFAULT_LAT=12.9716
   NEXT_PUBLIC_DEFAULT_LNG=77.5946
   NEXT_PUBLIC_DEFAULT_ZOOM=11
   ```

6. **Install dependencies** (if not done by setup.sh)
   ```bash
   npm install
   ```

7. **Start development server**
   ```bash
   npm run dev
   ```

8. **Open browser**
   ```
   http://localhost:3000
   ```

## 🗂️ Project Structure

```
frontend/
├── src/
│   ├── app/
│   │   ├── (auth)/
│   │   │   └── login/page.tsx
│   │   ├── (dashboard)/
│   │   │   └── dashboard/
│   │   │       ├── layout.tsx
│   │   │       ├── page.tsx (main dashboard)
│   │   │       ├── map/page.tsx
│   │   │       ├── reports/page.tsx
│   │   │       ├── alerts/page.tsx
│   │   │       ├── analytics/page.tsx
│   │   │       ├── mood/page.tsx
│   │   │       └── settings/page.tsx
│   │   ├── layout.tsx (root layout)
│   │   ├── page.tsx (redirect)
│   │   └── globals.css
│   ├── components/
│   │   ├── auth-provider.tsx
│   │   ├── providers.tsx
│   │   ├── dashboard/
│   │   │   ├── header.tsx
│   │   │   └── sidebar.tsx
│   │   ├── map/
│   │   │   ├── map-view.tsx
│   │   │   ├── map-filters.tsx
│   │   │   └── event-detail.tsx
│   │   ├── mood/
│   │   │   └── mood-map-view.tsx
│   │   └── ui/ (shadcn components)
│   │       ├── button.tsx
│   │       ├── card.tsx
│   │       ├── input.tsx
│   │       ├── avatar.tsx
│   │       ├── dropdown-menu.tsx
│   │       └── dialog.tsx
│   ├── hooks/
│   │   └── useApi.ts (React Query hooks)
│   ├── lib/
│   │   ├── api.ts (API client)
│   │   ├── firebase.ts (Firebase config)
│   │   └── utils.ts (helper functions)
│   ├── store/
│   │   ├── auth.ts (auth state)
│   │   ├── map.ts (map state)
│   │   └── ui.ts (UI state)
│   └── types/
│       └── index.ts (TypeScript types)
├── public/
├── package.json
├── next.config.mjs
├── tsconfig.json
├── tailwind.config.js
├── postcss.config.js
└── .env.local
```

## 🚀 Usage Guide

### 1. Authentication

- Navigate to `/login`
- Sign in with Google or Email/Password
- First-time users are automatically redirected to dashboard

### 2. Dashboard Overview

- **Stats Cards**: View total events, active alerts, average sentiment, resolved issues
- **Recent Events**: Latest 5 city events
- **Active Alerts**: Top 3 current alerts

### 3. Map View

- **Navigation**: Pan, zoom, click markers
- **Filters**: Category selection, time range, clustering toggle
- **Event Details**: Click marker to see full event information
- **Auto-refresh**: Toggle live updates every 30 seconds

### 4. Report Submission

- Click "New Report" button in header
- Fill form: title, description, category
- Upload photos/videos
- Auto-geo-tag or manually select location
- AI summarization applied on backend

### 5. Alerts Management

- View all active alerts sorted by severity
- Filter by severity level
- See predictive vs reported alerts

### 6. Analytics

- Event volume trends over time
- Category distribution charts
- City health score indicator
- Top reporting areas

### 7. Mood Map

- Color-coded sentiment zones
- Hover for detailed sentiment data
- View event count per zone

## 🔧 Configuration

### API Integration

The frontend expects the following backend endpoints:

```typescript
GET  /events                  // List all events
GET  /events/:id              // Get single event
POST /reports                 // Create new report
GET  /reports                 // List reports
GET  /alerts                  // List alerts
GET  /sentiments              // Get sentiment data
GET  /stats                   // City statistics
GET  /analytics               // Analytics data
POST /subscriptions           // Create subscription
GET  /subscriptions/:userId   // Get user subscriptions
DELETE /subscriptions/:id     // Delete subscription
```

### Firebase Setup

1. Create Firebase project at https://console.firebase.google.com
2. Enable Authentication (Google, Email/Password)
3. Enable Firestore Database
4. Enable Storage
5. Enable Cloud Messaging
6. Get configuration values from Project Settings
7. Add values to `.env.local`

### Mapbox Setup

1. Create account at https://www.mapbox.com
2. Generate access token
3. Add to `.env.local` as `NEXT_PUBLIC_MAPBOX_TOKEN`

## 🎨 Customization

### Theme Colors

Edit `src/app/globals.css`:

```css
:root {
  --primary: 221.2 83.2% 53.3%;  /* Blue */
  --secondary: 210 40% 96.1%;     /* Light gray */
  /* ... more colors */
}
```

### Default Map Center

Change in `.env.local`:

```env
NEXT_PUBLIC_DEFAULT_LAT=your_latitude
NEXT_PUBLIC_DEFAULT_LNG=your_longitude
NEXT_PUBLIC_DEFAULT_ZOOM=11
```

### Event Categories

Edit `src/components/map/map-filters.tsx`:

```typescript
const categories = ['traffic', 'emergency', 'civic', 'cultural', 'weather', 'your-category'];
```

## 🧪 Testing

```bash
# Run tests
npm test

# Run tests in watch mode
npm run test:watch
```

## 📦 Building for Production

```bash
# Create production build
npm run build

# Start production server
npm start
```

## 🐳 Docker Deployment

```dockerfile
# Dockerfile included in deployment/
docker build -t citypulse-frontend .
docker run -p 3000:3000 citypulse-frontend
```

## 🔍 Troubleshooting

### Map not loading
- Check `NEXT_PUBLIC_MAPBOX_TOKEN` is set correctly
- Verify token has appropriate permissions

### Authentication errors
- Verify Firebase configuration in `.env.local`
- Check Firebase project has Auth enabled
- Ensure authorized domains include localhost

### API connection issues
- Confirm backend is running on `NEXT_PUBLIC_API_URL`
- Check CORS settings on backend
- Verify network connectivity

### Build errors
- Clear `.next` folder: `rm -rf .next`
- Clear node_modules: `rm -rf node_modules && npm install`
- Check Node version: `node --version` (should be 18+)

## 🤝 Integration with Other Services

### Backend (FastAPI)
- Endpoints defined in `/backend/app/routes/`
- Authentication via JWT tokens
- WebSocket support for real-time updates

### AI/ML Service
- Text summarization via `/ai/summarize`
- Image classification for uploaded media
- Sentiment analysis integrated in events

### Data Ingestion
- Events auto-refresh from ingestion pipeline
- Real-time updates via Firebase listeners
- Kafka consumer integration (optional)

## 📱 Mobile Responsiveness

- Fully responsive design
- Touch-optimized map controls
- Mobile-first navigation
- Progressive Web App (PWA) ready

## 🌟 Advanced Features

### Subscriptions & Notifications
- Draw custom areas on map
- Subscribe to specific event types
- Push notifications via FCM
- Email notifications (backend integration)

### Real-Time Updates
- WebSocket connection for live events
- Auto-refresh intervals (configurable)
- Optimistic UI updates

### Accessibility
- ARIA labels on all interactive elements
- Keyboard navigation support
- Screen reader compatible
- High contrast mode support

## 📄 License

MIT License - See LICENSE file for details

## 👥 Contributors

- Member C - Frontend Engineer
- Full-stack integration team

## 🔗 Related Projects

- [Backend API](../backend/README.md)
- [AI/ML Services](../ai-ml/README.md)
- [Data Ingestion](../data-ingestion/README.md)
- [Data Processing](../data-processing/README.md)

---

**Built with ❤️ for SmartCitySense**
