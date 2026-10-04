# Engineering note

## Overview

Azadchi is a classifieds marketplace for Iran's free zones and special economic zones. A visitor posts a listing, searches in that area, and talks directly with the other party.

## Stack

Web client, declared in `azadchi-client/package.json`:

- React ^18.3.1
- Vite ^6.0.7
- Tailwind CSS ^3.4.17
- React Router ^7.1.1
- Leaflet ^1.9.4
- Socket.IO client ^4.8.1

API, declared in `azadchi-server/package.json`. Engines field: Node.js >= 20.

- Express ^4.21.2
- PostgreSQL client `pg` ^8.13.1
- Redis client `ioredis` ^5.4.2
- Bull ^4.16.5
- Socket.IO ^4.8.1
- jsonwebtoken ^9.0.2
- bcryptjs ^2.4.3
- otplib ^13.4.1
- sharp ^0.34.5
- multer ^1.4.5-lts.1
- web-push ^3.6.7
- Helmet ^8.0.0
- express-rate-limit ^8.5.2

PostgreSQL is opened with `pg.Pool` in `azadchi-server/src/infrastructure/database/postgresql.js`. Redis is opened with `ioredis` in `azadchi-server/src/infrastructure/database/redis.js`.

Mobile app, declared in `azadchi_app/pubspec.yaml`:

- Flutter
- Dart SDK >=3.5.0 <4.0.0
- webview_flutter ^4.10.0
- speech_to_text ^7.0.0

End-to-end tests: Playwright, devDependency `@playwright/test` ^1.61.1 in `azadchi-server/package.json`.

## Specialties

- Listing search for free zones and special economic zones, served by the Express API and the React client above
- Direct conversation: Socket.IO (`socket.io` on the server, `socket.io-client` on the web client)
- Maps: Leaflet on the web client
- Authentication: jsonwebtoken, bcryptjs, and otplib
- Background jobs: Bull on Redis
- Image upload: multer and sharp
- Web push: web-push
- On-device speech input: `speech_to_text` in `azadchi_app/lib/core/native_stt/device_speech.dart`
- Request matching: lexical match is the default path. PostgreSQL pgvector embeddings exist for an optional shortlist and the flag defaults off (`ALWER_MATCH_PGVECTOR`). The extension migration is `azadchi-server/database/migrations/020_pgvector_request_embeddings.sql`. Matching code is in `azadchi-server/src/modules/matching/matchEmbedding.js`.

## Boundaries

This note covers the Azadchi marketplace applications named above. It does not describe hosting or credentials.
