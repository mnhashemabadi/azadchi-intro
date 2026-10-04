# آزادچی

من آزادچی را از همان شکل آلور ساختم و محدوده را عوض کردم. بازار نیازمندی معمولی کل کشور است. آزادچی فقط مناطق آزاد و ویژهٔ اقتصادی است. روی [azadchi.ir](https://azadchi.ir) نوشتم «آزاد» یعنی آزادی تجارت در مناطق آزاد و «چی» یعنی پهنهٔ کسب‌وکار در همان مناطق. آگهی و جستجو حول همان منطقه است. گفتگو با طرف دیگر داخل آزادچی می‌ماند، نه تماس پراکنده بیرون محصول.

سایت: [azadchi.ir](https://azadchi.ir)

## آنچه بازدیدکننده می‌بیند

ثبت آگهی روی صفحهٔ اصلی: انتخاب منطقهٔ آزاد و دسته، عکس و جزئیات، پیش‌نمایش، انتشار تا آگهی در جستجوی همان منطقه بیاید، بعد جواب پیام خریدار در چت. جستجو منطقه (یا «همه مناطق آزاد»)، دسته و کلمات را می‌گیرد و از روی آگهی به چت با فروشنده می‌رود. پوشش کل ایران نیست. انتخاب محدوده «همه مناطق آزاد» است، نه کل کشور. صفحه نمونه‌هایی مثل کیش، قشم، ارس، انزلی، اروند و چابهار را نام می‌برد و بقیه را به صفحهٔ مناطق آزاد حواله می‌دهد.

ده ثبت اول هر ماه رایگان است. بعد از آن هر ثبت از کیف پول کم می‌شود و روی خود معامله کارمزد گرفته نمی‌شود. این را صفحهٔ اصلی می‌گوید و مبلغ تومان را روی همان متن ننوشته است. در سرور، `FREE_REQUEST_LIMIT` برابر ۱۰ و `REQUEST_FEE_AMOUNT` برابر ۱۰۰۰۰ است. پیشنهاد قیمت جدا است: `FREE_QUOTE_LIMIT` برابر ۱۰ و `QUOTE_FEE_AMOUNT` برابر ۵۰۰۰. سهمیه را مثل آلور با `jalaliPeriod.js` روی ماه جلالی حساب می‌کنم. مسیر اصلی صفحه، چت روی آگهی است نه جدول مقایسهٔ پیشنهاد. هر دو گروه مسیر روی سرور هستند؛ پیشنهاد را برداشتم چون خانوادهٔ کد همان است، ولی صفحه را روی آگهی منطقه و چت بستم.

## همان خانواده، تأییدشده از مانیفست

کلاینت `azadchi-client` است. `package.json` همان وابستگی‌های وب آلور را اعلام می‌کند: React ^18.3.1، Vite ^6.0.7، Tailwind ^3.4.17، React Router ^7.1.1، Leaflet ^1.9.4، `socket.io-client` ^4.8.1، و فونت Vazirmatn. نقشه را با Leaflet گذاشتم چون منطقه باید روی نقشه دیده شود، نه فقط در یک فهرست متنی.

API `azadchi-server` است. Express ^4.21.2، Node.js `>=20`، `pg` ^8.13.1، `ioredis` ^5.4.2، Bull ^4.16.5، Socket.IO ^4.8.1، `jsonwebtoken`، `bcryptjs`، `otplib`، `sharp`، `multer`، `web-push`، Helmet، `express-rate-limit`. Postgres را با `pg.Pool` در `src/infrastructure/database/postgresql.js` باز می‌کنم و Redis را با `ioredis` در `src/infrastructure/database/redis.js`. `src/server.js` مثل آلور اول پایگاه را چک می‌کند، Redis را وصل می‌کند، Socket.IO را می‌چسباند، ورکرهای Bull را شروع می‌کند و بعد گوش می‌دهد.

اپ `azadchi_app` پوستهٔ Flutter است، نسخهٔ `1.0.14+83`، Dart `>=3.5.0 <4.0.0`، `webview_flutter` ^4.10.0 و `speech_to_text` ^7.0.0. pubspec می‌گوید بازار و مسیرهای اصلی نیتیو‌اند و WebView fallback است.

## فهرست منطقه داخل خود برنامه

محدوده را به یک رشتهٔ آزاد نسپردم. `azadchi_app/assets/geo/free-zones.json` دارایی Flutter است و در `pubspec.yaml` کنار `assets/brand/` می‌آید. `allScopeLabel` برابر `همه مناطق آزاد` است. آرایهٔ `zones` این ۲۱ مورد است:

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

مختصات شهر و فهرست شهرهای ایران دارایی جدا هستند: `assets/geo/iran-cities.json` و `assets/geo/iran-city-coordinates.json`. دسته‌ها در `assets/azadchi-categories.json` هستند. فایل‌های Leaflet `assets/map/leaflet.css` و `assets/map/leaflet.js` را برای نقشهٔ داخل برنامه بسته‌بندی کردم. اگر منطقه فقط برچسب متنی بود، «همه مناطق آزاد» با کل ایران قاطی می‌شد.

## آگهی، جستجو، چت

آگهی یک ردیف درخواست است. `request.routes.js` این‌ها را دارد: `GET /api/requests` و `GET /api/requests/:id` (احراز اختیاری روی تک‌ردیف)، `POST /api/requests` با `authMiddleware` و `checkRequestQuota`، `PUT` و `DELETE` برای مالک، `GET /api/requests/mine`، `GET /api/requests/:id/matches` و `related` و `market-estimate`، و `POST /api/requests/:id/contact` به‌همراه تمدید. جستجوی بازار `GET /api/search` پشت `searchRateLimit` است.

چت مسیر گفتگوی عمومی است. مسیرهای HTTP چت همه `authMiddleware` دارند: فهرست گفتگو، `POST` گفتگو روی شناسهٔ درخواست، خواندن و فرستادن پیام، ویرایش و حذف، پنهان و آشکار. Socket.IO در `server.js` راه می‌افتد و ماژول سوکت `connection`، `chat:join`، `chat:leave`، `chat:typing`، `chat:typing_stop` و `disconnect` را می‌گیرد.

پیشنهاد هم سوار است: `POST /api/requests/:id/quotes` با `checkQuoteQuota`، فهرست پیشنهاد درخواست، فهرست پیشنهادهای خود کاربر، داشبورد فروشنده، ویرایش، قبول، پس گرفتن.

`app.js` Helmet و CORS و بدنهٔ JSON با سقف ۱ مگابایت را دارد و همان خانوادۀ مسیر را سوار می‌کند: auth، alerts، notifications، wallet، affiliate، pricing، reports، ratings، blog، pages، seo، meta، vehicles، electronics، uploads، users، ai، map، bookmarks، ads، support. تفاوتی که عمداً گذاشتم: `/api/content-review` فقط وقتی `requireContentReviewEnabled` اجازه بدهد سوار می‌شود. در آلور این مسیر بدون آن قفل سوار است. روی آزادچی بررسی همکار را پیش‌فرض بازار منطقه نکردم.

ورود همان شکل است: ثبت، تأیید، TOTP، خروج، `me`. `OTP_TTL_SECONDS` برابر ۱۲۰ است. توکن با `jsonwebtoken`، رمز با `bcryptjs`، TOTP با `otplib`. آپلود تصویر `multer` و `sharp` است.

## pgvector

مهاجرت `azadchi-server/database/migrations/020_pgvector_request_embeddings.sql` ستون embedding درخواست را برای کوتاه‌فهرست معنایی اضافه می‌کند. در `src/config/intelligence.js` پرچم `matchPgvectorEnabled` از متغیر `ALWER_MATCH_PGVECTOR` خوانده می‌شود و پیش‌فرضش خاموش است. همان توضیح می‌گوید تا وقتی بردارها باشند روشن نشود و مسیر واژگانی شبکهٔ ایمنی بماند. نام مدل را نمی‌نویسم.

میزبانی و رمزها را اینجا نیاوردم.

## English

I built Azadchi from the same shape as Alwer and changed the range. A normal classifieds market is the whole country. Azadchi is only free zones and special economic zones. On [azadchi.ir](https://azadchi.ir) I wrote that "Azad" means trade freedom in the free zones and "chi" means the business field inside those zones. A listing and a search stay around that zone. The conversation with the other party stays inside Azadchi, not as a scattered contact outside the product.

Site: [azadchi.ir](https://azadchi.ir)

### What a visitor sees

Posting on the homepage: choose a free zone and a category, add photos and details, preview, publish so the listing shows in search for that zone, then answer the buyer in chat. Search takes a zone (or all free zones), a category, and keywords, and opens chat with the seller from the listing. The coverage is not all of Iran. The range choice is all free zones, not the whole country. The page names examples such as Kish, Qeshm, Aras, Anzali, Arvand, and Chabahar, and points the rest at the zones page.

The first ten posts of each month are free. After that, each post comes out of the wallet, and the deal itself has no commission. The homepage says that and does not print a toman amount in that text. On the server, `FREE_REQUEST_LIMIT` is 10 and `REQUEST_FEE_AMOUNT` is 10000. A price offer is separate: `FREE_QUOTE_LIMIT` is 10 and `QUOTE_FEE_AMOUNT` is 5000. I count the quota on the Jalali month with `jalaliPeriod.js`, the same way as Alwer. The page's main path is chat on a listing, not an offer-comparison table. Both route groups exist on the server. I kept quotes because the code family is the same, and I closed the page on the zone listing and the chat.

### Same family, confirmed from the manifests

The client is `azadchi-client`. Its `package.json` declares the same web dependencies I use on Alwer: React ^18.3.1, Vite ^6.0.7, Tailwind ^3.4.17, React Router ^7.1.1, Leaflet ^1.9.4, `socket.io-client` ^4.8.1, and the Vazirmatn font. I used Leaflet because a zone has to be visible on a map, not only in a text list.

The API is `azadchi-server`. Express ^4.21.2, Node.js `>=20`, `pg` ^8.13.1, `ioredis` ^5.4.2, Bull ^4.16.5, Socket.IO ^4.8.1, `jsonwebtoken`, `bcryptjs`, `otplib`, `sharp`, `multer`, `web-push`, Helmet, `express-rate-limit`. I open Postgres with `pg.Pool` in `src/infrastructure/database/postgresql.js` and Redis with `ioredis` in `src/infrastructure/database/redis.js`. `src/server.js`, like Alwer, checks the database, connects Redis, attaches Socket.IO, starts the Bull workers, then listens.

The app `azadchi_app` is a Flutter shell, version `1.0.14+83`, Dart `>=3.5.0 <4.0.0`, `webview_flutter` ^4.10.0 and `speech_to_text` ^7.0.0. The pubspec says the market and the main paths are native and WebView is the fallback.

### The zone list lives in the app

I did not leave the range as a free-typed string. `azadchi_app/assets/geo/free-zones.json` is a Flutter asset, referenced from `pubspec.yaml` next to `assets/brand/`. `allScopeLabel` is `همه مناطق آزاد`. The `zones` array is these 21 entries:

- Chabahar (`chabahar`)
- Kish (`kish`)
- Qeshm (`qeshm`)
- Aras (`aras`)
- Anzali (`anzali`)
- Arvand (`arvand`)
- Maku (`maku`)
- Imam Khomeini Airport (`ika`)
- Incheh Borun (`inchehborun`)
- Bushehr (`bushehr`)
- Ardabil (`ardabil`)
- Sistan (`sistan`)
- Mehran (`mehran`)
- Qasr-e Shirin (`qasre-shirin`)
- Baneh and Marivan (`baneh-marivan`)
- Mazandaran (`mazandaran`)
- Sarakhs (`sarakhs`)
- Dogharun (`dogharun`)
- Sero (`sero`)
- Piranshahr border market (`piranshahr-bazaar`)
- Astara coastal market (`astara-bazaar`)

City coordinates and the Iran city list are separate assets: `assets/geo/iran-cities.json` and `assets/geo/iran-city-coordinates.json`. Categories are in `assets/azadchi-categories.json`. I packaged Leaflet files `assets/map/leaflet.css` and `assets/map/leaflet.js` for the in-app map. If a zone were only a text label, "all free zones" would blur into all of Iran.

### Listing, search, chat

A listing is a request row. `request.routes.js` exposes `GET /api/requests` and `GET /api/requests/:id` (optional auth on the single row), `POST /api/requests` with `authMiddleware` and `checkRequestQuota`, `PUT` and `DELETE` for the owner, `GET /api/requests/mine`, `GET /api/requests/:id/matches`, `related`, and `market-estimate`, and `POST /api/requests/:id/contact` plus renew. Market search is `GET /api/search` behind `searchRateLimit`.

Chat is the public conversation path. Chat HTTP routes all use `authMiddleware`: list conversations, `POST` a conversation on a request id, read and send messages, edit and delete, hide and unhide. Socket.IO starts in `server.js`, and the socket module handles `connection`, `chat:join`, `chat:leave`, `chat:typing`, `chat:typing_stop`, and `disconnect`.

Quotes are mounted too: `POST /api/requests/:id/quotes` with `checkQuoteQuota`, quotes for a request, the caller's quotes, the seller dashboard, patch, accept, and withdraw.

`app.js` mounts Helmet, CORS, and a JSON body limit of 1mb, and the same route family: auth, alerts, notifications, wallet, affiliate, pricing, reports, ratings, blog, pages, seo, meta, vehicles, electronics, uploads, users, ai, map, bookmarks, ads, support. The difference I put in on purpose: `/api/content-review` mounts only when `requireContentReviewEnabled` allows it. On Alwer that route mounts without that gate. I did not make collaborator review the default of the zone market.

Sign-in is the same shape: register, verify, TOTP, logout, `me`. `OTP_TTL_SECONDS` is 120. Tokens use `jsonwebtoken`, passwords `bcryptjs`, TOTP `otplib`. Image upload is `multer` and `sharp`.

### pgvector

The migration `azadchi-server/database/migrations/020_pgvector_request_embeddings.sql` adds the request embedding column for a semantic shortlist. In `src/config/intelligence.js`, `matchPgvectorEnabled` reads `ALWER_MATCH_PGVECTOR` and defaults to off. The comment there says to keep it off until vectors exist, and to leave the lexical path as the safety net. I am not writing a model name.

I am not putting hosting or credentials here.

## پروژه‌های مرتبط

- [hamejoo-intro](https://github.com/mnhashemabadi/hamejoo-intro): همه‌جو را برای بازدیدکننده‌ای گذاشتم که با یک عبارت آگهی را یک‌جا ببیند و برای جزئیات به سایت منبع برود.
- [alwer-intro](https://github.com/mnhashemabadi/alwer-intro): آلور را برای خریداری گذاشتم که درخواست بنویسد و پیشنهاد قیمت‌ها را کنار هم ببیند؛ آگهی فروش هم روی همان بازار است.
- [kasbafzar-intro](https://github.com/mnhashemabadi/kasbafzar-intro): کسب‌افزار را برای کسی گذاشتم که فروش و مشتری و هزینه را ثبت کند و فاکتور را با لینک پرداخت برای مشتری بفرستد.
- [afzi-intro](https://github.com/mnhashemabadi/afzi-intro): افزی را برای کوتاه کردن یک نشانی http یا https گذاشتم؛ باز کردن لینک همان صفحه را باز می‌کند.
- [alweryar-intro](https://github.com/mnhashemabadi/alweryar-intro): آلوریار را برای همکاری در بررسی آگهی و همکاری در فروش آلور گذاشتم.
- [alwerchi-intro](https://github.com/mnhashemabadi/alwerchi-intro): آلورچی را برای فروشگاهی گذاشتم که کالا و موجودی‌اش در بازار آلور دیده شود و خریدار در آلور بماند.

## Related

- [hamejoo-intro](https://github.com/mnhashemabadi/hamejoo-intro): I built Hamejoo for a visitor who types one phrase, sees listings in one place, and opens the original site for the listing itself.
- [alwer-intro](https://github.com/mnhashemabadi/alwer-intro): I built Alwer for a buyer who posts a request and compares price offers side by side; a sale listing sits on the same market.
- [kasbafzar-intro](https://github.com/mnhashemabadi/kasbafzar-intro): I built Kasbafzar for someone who records sales, customers, and expenses, and sends the customer an invoice with a payment link.
- [afzi-intro](https://github.com/mnhashemabadi/afzi-intro): I built Afzi to shorten an http or https address; opening the short link opens that same page.
- [alweryar-intro](https://github.com/mnhashemabadi/alweryar-intro): I built Alweryar for collaboration on listing review and on sales for Alwer.
- [alwerchi-intro](https://github.com/mnhashemabadi/alwerchi-intro): I built Alwerchi for a shop whose goods and stock show on the Alwer market while the buyer stays on Alwer.

یادداشت مهندسی کوتاه‌تر: [docs/engineering.md](docs/engineering.md)

Shorter engineering note: [docs/engineering.md](docs/engineering.md)
