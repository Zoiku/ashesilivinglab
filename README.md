# Ashesi Living Lab

A room-monitoring prototype with an Express API and React dashboard for laboratory sensor readings. The dashboard visualizes humidity, light, motion, and temperature-related readings and displays suggested actions for conserving energy.

## Components

- `ashesi-living-lab-api/`: Express service backed by Firebase Realtime Database.
- `ashesi-living-lab-website/`: React 18 / Create React App dashboard with Material UI and Chart.js.

Despite the name `Firestore.js`, the API uses Firebase Realtime Database, not Cloud Firestore.

## Local setup

Node.js/npm and a configured Firebase Realtime Database are required.

1. In `ashesi-living-lab-api/Firestore.js`, replace the unquoted `XXX` configuration placeholders with your Firebase project's actual configuration.
2. Install dependencies in `ashesi-living-lab-api/`.
3. Set `PORT=3001` in your shell and run `node index.js` from that directory. The package's current start script is `npm index.js`, so use the direct Node command.
4. Update the hardcoded API address in `ashesi-living-lab-website/src/Pages/Dashboard.jsx` from the historical Heroku service to your local API, for example `http://localhost:3001/api/get/`.
5. In a second terminal, install dependencies in `ashesi-living-lab-website/` and run `npm start`. The website normally uses `http://localhost:3000`.

## API and data shape

- `GET /api/get/`: reads `Lecture-Hall/Lab222` from Realtime Database.
- `POST /api/post/`: writes an entry using `id`, `humidity`, `motion`, and `light`.

The current write path uses lowercase property names, while the dashboard reads capitalized `Humidity`, `Light`, `Motion`, and `Temperature`. Align the producer/database data shape and dashboard before expecting complete charts. Temperature is not written by the current POST handler.

The dashboard fetch effect also depends on the state it updates; review its refresh behavior before running against a shared service.

## Build and checks

From the website directory:

- `npm run build`: creates production assets in `build/`.
- `npm test`: invokes the Create React App test runner.

The API test command is a placeholder. Verify sensor writes, stored field names, chart rendering, and empty-data behavior with a development database.

## Code guide

`src/App.js` in the website defines Home, Dashboard, API Endpoints, and Settings routes. API behavior is in `index.js`; database access is in `Firestore.js`.
