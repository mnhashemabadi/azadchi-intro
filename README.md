# آزادچی

آزادچی بازار نیازمندی مناطق آزاد و ویژهٔ اقتصادی است. آگهی در همان محدوده ثبت و جستجو می‌شود و گفتگو با طرف دیگر داخل خود آزادچی انجام می‌شود.

سایت: [azadchi.ir](https://azadchi.ir)

## رفتار عمومی

صفحهٔ [azadchi.ir](https://azadchi.ir) ثبت آگهی را این‌طور می‌نویسد: انتخاب منطقهٔ آزاد و دسته، افزودن عکس و جزئیات، پیش‌نمایش، انتشار تا آگهی در جستجوی همان منطقه دیده شود، و پاسخ به پیام خریدار در چت. جستجو منطقه (یا «همه مناطق آزاد»)، دسته، و کلمات را می‌گیرد و از روی آگهی به چت با فروشنده می‌رود. همان صفحه می‌گوید پوشش، کل کشور نیست و انتخاب محدوده «همه مناطق آزاد» است نه کل ایران، و نمونه‌هایی مثل کیش، قشم، ارس، انزلی، اروند و چابهار را نام می‌برد. ده ثبت اول هر ماه (آگهی فروش) رایگان است؛ بعد از آن هر ثبت ۱۰۰٬۰۰۰ تومان از کیف پول کم می‌شود و روی خود معامله کارمزد گرفته نمی‌شود. صفحه به ثبت آگهی، جستجو، مناطق آزاد، راهنما، دریافت برنامه، وبلاگ، درباره، و مجوزها پیوند می‌دهد.

## English

Azadchi is a classifieds marketplace for Iran's free zones and special economic zones. A visitor posts a listing, searches inside that area, and talks with the other party in Azadchi chat.

Site: [azadchi.ir](https://azadchi.ir)

The public homepage describes posting as choosing a free zone and a category, adding photos and details, previewing, and publishing so the listing shows in search for that zone, then answering buyers in chat. Search takes a zone (or all free zones), a category, and keywords, then opens chat with the seller. The page says the scope is not the whole country: the range choice is all free zones, not all of Iran, and it names examples such as Kish, Qeshm, Aras, Anzali, Arvand, and Chabahar. The first ten sale posts of each month are free. After that, each post is 100,000 tomans from the wallet. The deal itself has no commission. The page links new-request, search, zones, help, download, blog, about, and licenses.

## Parts

The web client is `azadchi-client` (Vite, React, React Router). The API is `azadchi-server` (Express, Node.js engines `>=20`). The mobile shell is `azadchi_app` (Flutter).

`azadchi-server/src/server.js` checks PostgreSQL, connects Redis, attaches Socket.IO, starts Bull workers, and listens. PostgreSQL is a `pg.Pool` in `azadchi-server/src/infrastructure/database/postgresql.js`. Redis is `ioredis` in `azadchi-server/src/infrastructure/database/redis.js`.

`azadchi-server/src/app.js` mounts Helmet, CORS, a JSON body limit of 1mb, and these routers:

- `/api/auth`
- `/api/requests`
- `/api/search` and `/api/search/external`, both behind the search rate limit
- `/api/alerts`, `/api/notifications`, `/api/chat`, `/api/wallet`, `/api/affiliate`, `/api/identity`, `/api/pricing`
- `/api/reports`, `/api/ratings`, `/api/blog`, `/api/pages`, `/api/seo`, `/api/meta`
- `/api/vehicles`, `/api/electronics`, `/api/uploads`, `/api/users`, `/api/ai`, `/api/map`, `/api/bookmarks`, `/api/ads`, `/api/support`
- `/api/content-review`, and only when `requireContentReviewEnabled` allows it
- quote routes at `/api` (`/quotes` and `/requests/:id/quotes`)

## Zone list in the app

`azadchi_app/assets/geo/free-zones.json` is a Flutter asset (also referenced from `azadchi_app/pubspec.yaml` together with `assets/brand/free-zones/`). The file's `allScopeLabel` is `همه مناطق آزاد`. The `zones` array names:

- چابهار (`chabahar`)
- کیش (`kish`)
- قشم (`qeshm`)
- ارس (`aras`)
- انزلی (`anzali`)
- اروند (`arvand`)
- ماکو (`maku`)
- فرودگاه امام (`ika`)
- اینچه‌برون (`inchehborun`)
- بوشهر (`bushehr`)
- اردبیل (`ardabil`)
- سیستان (`sistan`)
- مهران (`mehran`)
- قصرشیرین (`qasre-shirin`)
- بانه و مریوان (`baneh-marivan`)
- مازندران (`mazandaran`)
- سرخس (`sarakhs`)
- دوغارون (`dogharun`)
- سرو (`sero`)
- بازارچه مرزی پیرانشهر (`piranshahr-bazaar`)
- بازارچه ساحلی آستارا (`astara-bazaar`)

City coordinates and the Iran city list are separate assets: `assets/geo/iran-cities.json` and `assets/geo/iran-city-coordinates.json`. Category art and `assets/azadchi-categories.json` ship with the same app. Leaflet files `assets/map/leaflet.css` and `assets/map/leaflet.js` are packaged for the in-app map. The web client depends on Leaflet `^1.9.4`.

## Listing, search, and chat

A listing is a request row. `azadchi-server/src/modules/request/request.routes.js` exposes:

- `GET /api/requests` and `GET /api/requests/:id` (optional auth on the single row)
- `POST /api/requests` with `authMiddleware` and `checkRequestQuota`
- `PUT /api/requests/:id` and `DELETE /api/requests/:id` for the owner
- `GET /api/requests/mine`
- `GET /api/requests/:id/matches`, `GET /api/requests/:id/related`, `GET /api/requests/:id/market-estimate`
- `POST /api/requests/:id/contact`, renew routes, and review routes on the same id

Search of the market is `GET /api/search` behind `searchRateLimit`.

Chat is the public conversation path. HTTP routes in the chat router all use `authMiddleware`: list conversations, `POST /requests/:requestId/conversation`, get and send messages, edit and delete a message, hide and unhide. Socket.IO is initialized in `server.js`. The socket module handles `connection`, `chat:join`, `chat:leave`, `chat:typing`, `chat:typing_stop`, and `disconnect`. The web client depends on `socket.io-client` `^4.8.1`.

Quotes are also mounted: `POST /api/requests/:id/quotes` with `checkQuoteQuota`, list quotes for a request, list the caller's quotes, seller dashboard, patch, accept, and withdraw. The public homepage describes chat on a listing rather than a quote comparison table. Both route groups exist on the server.

Auth routes: `POST /api/auth/register`, `POST /api/auth/verify`, TOTP verify and recover, `POST /api/auth/logout`, `GET /api/auth/me`. Register and verify use the auth rate limit. Session routes use `authMiddleware`, which reads the bearer token. Declared libraries: `jsonwebtoken`, `bcryptjs`, `otplib`.

Uploads: `POST /api/uploads` with `upload.single('image')` (`multer`), and `sharp` on the server for images. Web push is the `web-push` dependency.

## Jobs and matching

`server.js` starts Bull workers for match alerts, match opposite, and pilot liquidity. The AI extraction worker starts when `aiConfig.queueEnabled` is on. The request-embedding worker starts when `aiConfig.embedPersistEnabled` is on, with concurrency 2.

`azadchi-server/database/migrations/020_pgvector_request_embeddings.sql` creates the `vector` extension, adds `requests.embedding vector(768)`, `embedding_model`, and `embedding_updated_at`, and adds HNSW index `idx_requests_embedding_hnsw` using `vector_cosine_ops` for rows with an embedding, category `vehicles` or `real-estate`, and status `active`. Matching code is `azadchi-server/src/modules/matching/matchEmbedding.js`.

On-device speech input is `speech_to_text` in `azadchi_app/lib/core/native_stt/device_speech.dart`. The shell also uses `webview_flutter` so the packaged app can open the web UI. Firebase messaging dependencies in that pubspec are comments, not active dependencies.

## Libraries

Web client, `azadchi-client/package.json`:

- react ^18.3.1, react-dom ^18.3.1
- react-router-dom ^7.1.1
- vite ^6.0.7, @vitejs/plugin-react ^4.3.4
- tailwindcss ^3.4.17, postcss ^8.4.49, autoprefixer ^10.4.20
- leaflet ^1.9.4
- socket.io-client ^4.8.1
- lucide-react ^1.21.0
- @fontsource/vazirmatn ^5.2.6
- @uiw/react-md-editor ^4.1.1

API, `azadchi-server/package.json`, Node.js >= 20:

- express ^4.21.2, pg ^8.13.1, ioredis ^5.4.2, bull ^4.16.5, socket.io ^4.8.1
- jsonwebtoken ^9.0.2, bcryptjs ^2.4.3, otplib ^13.4.1
- sharp ^0.34.5, multer ^1.4.5-lts.1, web-push ^3.6.7
- helmet ^8.0.0, express-rate-limit ^8.5.2, rate-limit-redis ^5.0.0, cors ^2.8.5
- axios ^1.18.1, cheerio ^1.2.0, gray-matter ^4.0.3, marked ^18.0.5, uuid ^11.0.5
- firebase-admin ^13.10.0, dotenv ^16.4.7
- dev: @playwright/test ^1.61.1, simple-icons ^16.27.0

`firebase-admin` is a server dependency. The Flutter app does not depend on it.

Mobile, `azadchi_app/pubspec.yaml` version 1.0.14+83:

- Flutter, flutter_localizations, Dart SDK >=3.5.0 <4.0.0
- webview_flutter ^4.10.0 and the Android, web, and platform-interface packages listed beside it
- speech_to_text ^7.0.0
- url_launcher ^6.3.2
- flutter_screenutil ^5.9.3
- web ^1.1.1
- flutter_lints ^5.0.0 in dev_dependencies

## Boundaries

Hosting and credentials are omitted. The zone names above are the `zones` entries in `free-zones.json`, not a claim about which of those zones currently have listings.

## پروژه‌های مرتبط

- [hamejoo-intro](https://github.com/mnhashemabadi/hamejoo-intro): همه‌جو نتیجهٔ جستجوی آگهی را یک‌جا نشان می‌دهد و جزئیات آگهی روی منبع اصلی می‌ماند.
- [alwer-intro](https://github.com/mnhashemabadi/alwer-intro): آلور بازار نیازمندی است؛ درخواست خرید ثبت می‌شود، فروشنده پیشنهاد قیمت می‌فرستد، و آگهی فروش هم در همان بازار است.
- [kasbafzar-intro](https://github.com/mnhashemabadi/kasbafzar-intro): کسب‌افزار پیشخوان فروش و گزارش مالی است؛ فروش، مشتری و هزینه ثبت می‌شود و فاکتور می‌تواند لینک پرداخت داشته باشد.
- [afzi-intro](https://github.com/mnhashemabadi/afzi-intro): افزی یک نشانی http یا https را به لینک کوتاه تبدیل می‌کند و باز کردن آن لینک به همان صفحه می‌رود.
- [alweryar-intro](https://github.com/mnhashemabadi/alweryar-intro): آلوریار شبکهٔ همکاران آلور برای بررسی آگهی و همکاری در فروش است.
- [alwerchi-intro](https://github.com/mnhashemabadi/alwerchi-intro): آلورچی خانهٔ فروشگاه‌هایی است که کالا و موجودی‌شان در بازار آلور دیده می‌شود و خریدار در آلور می‌ماند.

## Related

- [hamejoo-intro](https://github.com/mnhashemabadi/hamejoo-intro): Hamejoo shows listing search results in one place, and the listing detail stays on the original source.
- [alwer-intro](https://github.com/mnhashemabadi/alwer-intro): Alwer is a classifieds marketplace: a buyer posts a request, sellers send price offers, and a sale listing can be posted on the same market.
- [kasbafzar-intro](https://github.com/mnhashemabadi/kasbafzar-intro): Kasbafzar is a sales desk and a financial report: sales, customers, and expenses are recorded, and an invoice can carry a payment link.
- [afzi-intro](https://github.com/mnhashemabadi/afzi-intro): Afzi turns an http or https address into a short link, and opening that link goes to the same page.
- [alweryar-intro](https://github.com/mnhashemabadi/alweryar-intro): Alweryar is Alwer's collaborator network for listing review and for sales collaboration.
- [alwerchi-intro](https://github.com/mnhashemabadi/alwerchi-intro): Alwerchi is the home of shops whose goods and stock appear on the Alwer marketplace while the buyer stays on Alwer.

یادداشت مهندسی کوتاه‌تر: [docs/engineering.md](docs/engineering.md)

Shorter engineering note: [docs/engineering.md](docs/engineering.md)

