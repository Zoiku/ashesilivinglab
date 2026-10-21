# Ashesi Living Lab Dashboard

A React dashboard for room sensor readings, charts, and suggested energy-saving actions.

Read the [repository README](../README.md) for Firebase Realtime Database configuration, API startup, and the current sensor-field mismatch.

## Develop

From this directory, run `npm install` and `npm start`. The default development address is `http://localhost:3000`.

Update the historical Heroku URL in `src/Pages/Dashboard.jsx` to the intended API. A local API should use a different port from the website.

## Commands

- `npm run build`: production output in `build/`.
- `npm test`: Create React App test runner.

The dashboard expects capitalized sensor fields, while the bundled API writes lowercase fields and does not write temperature. Align those data shapes before checking charts. Also review the fetch effect's state dependency to avoid repeated requests.

Routes and page components are in `src/App.js` and `src/Pages/`; chart presentation is in `src/Components/`.
