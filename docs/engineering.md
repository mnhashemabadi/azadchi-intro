# Engineering note

## Overview

Azadchi is a classifieds marketplace for Iran's free zones and special economic zones. A visitor posts a listing, searches in that area, and talks directly with the other party.

## Stack

Web client:

- React ^18.3.1
- Vite ^6.0.7
- Tailwind CSS ^3.4.17
- React Router ^7.1.1
- Leaflet ^1.9.4
- Socket.IO client ^4.8.1

API, Node.js 20 or later:

- Express ^4.21.2
- PostgreSQL client `pg` ^8.13.1
- Redis client `ioredis` ^5.4.2
- Bull ^4.16.5
- Socket.IO ^4.8.1
- sharp ^0.34.5
- multer ^1.4.5-lts.1
- web-push ^3.6.7
- Helmet ^8.0.0
- express-rate-limit ^8.5.2

Mobile app:

- Flutter
- Dart SDK >=3.5.0 <4.0.0
- webview_flutter ^4.10.0
- speech_to_text ^7.0.0

End-to-end tests: Playwright (`@playwright/test` ^1.61.1).

## Specialties

- Listing search for free zones and special economic zones, served by the Express API and the React client
- Direct conversation: Socket.IO on the server and the web client
- Maps: Leaflet on the web client and in the app
- Background jobs: Bull on Redis
- Image upload and processing: multer and sharp
- Web push: web-push
- On-device speech input: `speech_to_text`
