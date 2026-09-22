# Techflix dsu

A Smart Mobility Intelligence System built with Next.js, featuring real-time route analysis, interactive maps, and premium animations.

## Features

- 🗺️ Interactive Google Maps integration
- 🚗 Real-time route analysis with traffic insights
- 🎨 45+ premium CSS animations
- 📍 Location search with 20+ Bengaluru landmarks
- 📊 Analytics dashboard with environmental impact
- 🎯 Nearby transport vehicle visualization
- 📱 Fully responsive design

## Getting Started

### Local Development

1. Clone the repository
2. Install dependencies:
```bash
npm install
```

3. Create environment file:
```bash
cp .env.local.example .env.local
```

4. Add your Google Maps API key to `.env.local`:
```
NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=your_api_key_here
```

5. Run the development server:
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Deployment

#### Netlify Deployment

1. **Connect Repository**: Link your GitHub repository to Netlify
2. **Build Settings**:
   - Build command: `npm run build`
   - Publish directory: `.next`
   - Node version: 18

3. **Environment Variables**: Add in Netlify dashboard:
   - `NEXT_PUBLIC_GOOGLE_MAPS_API_KEY`: Your Google Maps API key

4. **Deploy**: Netlify will automatically build and deploy on git push

#### Manual Deployment

```bash
npm run build
npm run start
```

## Tech Stack

- **Framework**: Next.js 16
- **Styling**: Tailwind CSS
- **Maps**: Google Maps API
- **Animations**: CSS3 Keyframes
- **Deployment**: Netlify-ready

## Project Structure

```
routeiq/
├── src/
│   ├── app/
│   │   ├── api/
│   │   ├── globals.css
│   │   ├── layout.js
│   │   └── page.js
│   └── components/
│       ├── EnhancedMapView.jsx
│       ├── EnhancedRouteForm.jsx
│       └── EnhancedDashboard.jsx
├── public/
├── netlify.toml
└── package.json
```

## Environment Variables

Create a `.env.local` file with:

```
NEXT_PUBLIC_GOOGLE_MAPS_API_KEY=your_google_maps_api_key
```

Get your API key from [Google Cloud Console](https://console.cloud.google.com/).

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## License

This project is open source and available under the [MIT License](LICENSE).
