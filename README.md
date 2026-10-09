# آزادچی

آزادچی را بازار نیازمندی مناطق آزاد و ویژهٔ اقتصادی ساختم. بازار نیازمندی معمولی کل کشور را می‌گیرد؛ آزادچی فقط همین مناطق را. روی [azadchi.ir](https://azadchi.ir) نوشتم «آزاد» یعنی آزادی تجارت در مناطق آزاد و «چی» یعنی پهنهٔ کسب‌وکار در همان مناطق. آگهی و جستجو حول همان منطقه می‌ماند. گفتگو با طرف دیگر داخل آزادچی می‌ماند، نه به‌صورت تماس پراکنده بیرون محصول.

سایت: [azadchi.ir](https://azadchi.ir)

## آنچه بازدیدکننده می‌بیند

ثبت آگهی روی صفحهٔ اصلی: انتخاب منطقهٔ آزاد و دسته، عکس و جزئیات، پیش‌نمایش، انتشار تا آگهی در جستجوی همان منطقه بیاید، بعد جواب پیام خریدار در چت. جستجو منطقه را (یا «همه مناطق آزاد»)، با دسته و کلیدواژه‌ها، می‌گیرد و از روی آگهی به چت با فروشنده می‌رود. این پوشش کل ایران نیست. انتخاب محدوده «همه مناطق آزاد» است، نه کل کشور. صفحه نمونه‌هایی مثل کیش، قشم، ارس، انزلی، اروند و چابهار را نام می‌برد و بقیه را به صفحهٔ مناطق آزاد ارجاع می‌دهد.

مسیر اصلی صفحه، چت روی آگهی است، نه جدول مقایسهٔ پیشنهاد. پیشنهاد قیمت هم هست، ولی صفحه را روی آگهی منطقه و گفتگو متمرکز کردم. سهمیهٔ ثبت رایگان ماهانه را روی ماه جلالی حساب می‌کنم.

## پشتهٔ فنی

کلاینت وب با Vite ^6.0.7 ساخته می‌شود: React ^18.3.1، Tailwind ^3.4.17، React Router ^7.1.1، Leaflet ^1.9.4، `socket.io-client` ^4.8.1 و فونت Vazirmatn. نقشه را با Leaflet گذاشتم چون منطقه باید روی نقشه دیده شود، نه فقط در یک فهرست متنی.

API با Express ^4.21.2 روی Node.js 20 به بالا نوشته شده، با `pg` ^8.13.1 برای Postgres، `ioredis` ^5.4.2 برای Redis، Bull ^4.16.5 برای کار پس‌زمینه، Socket.IO ^4.8.1 برای گفتگوی زنده، `sharp` و `multer` برای تصویر، `web-push` برای اعلان مرورگر، و Helmet و `express-rate-limit` برای سخت‌سازی. سرور هنگام بالا آمدن پایگاه را چک می‌کند، Redis را وصل می‌کند، Socket.IO را به همان سرور HTTP می‌چسباند، ورکرهای Bull را شروع می‌کند و بعد گوش می‌دهد.

اپ موبایل پوستهٔ Flutter است، نسخهٔ `1.0.14+83` با Dart `>=3.5.0 <4.0.0`، `webview_flutter` ^4.10.0 و `speech_to_text` ^7.0.0. بازار و مسیرهای اصلی نیتیو هستند و WebView مسیر جایگزین است.

## فهرست منطقه داخل خود برنامه

محدوده را به یک رشتهٔ آزاد نسپردم. فهرست مناطق داخل خود اپ بسته‌بندی شده و گزینهٔ «همه مناطق آزاد» یکی از انتخاب‌های همان فهرست است. ۲۱ منطقه پوشش داده می‌شود: چابهار، کیش، قشم، ارس، انزلی، اروند، ماکو، فرودگاه امام، اینچه‌برون، بوشهر، اردبیل، سیستان، مهران، قصرشیرین، بانه و مریوان، مازندران، سرخس، دوغارون، سرو، بازارچهٔ مرزی پیرانشهر و بازارچهٔ ساحلی آستارا.

فهرست شهرهای ایران، مختصاتشان و دسته‌ها هم دارایی‌های جدای برنامه هستند و فایل‌های Leaflet برای نقشهٔ داخل برنامه همراهش بسته‌بندی شده‌اند. اگر منطقه فقط برچسب متنی بود، «همه مناطق آزاد» با کل ایران قاطی می‌شد.

## آگهی، جستجو، چت

آگهی ساخته، ویرایش، حذف و تمدید می‌شود و کنارش آگهی‌های مرتبط و برآورد قیمت بازار می‌آید. جستجوی بازار محدودیت نرخ جداگانه دارد.

چت مسیر اصلی گفتگو است: فهرست گفتگو، شروع گفتگو روی یک آگهی، خواندن و فرستادن پیام، ویرایش و حذف، پنهان و آشکار کردن گفتگو. پیوستن به گفتگو و وضعیت «در حال تایپ» روی Socket.IO است. Helmet و CORS و سقف ۱ مگابایت برای بدنهٔ JSON پیش از همهٔ مسیرها اعمال می‌شود.

## English

I built Azadchi as a classifieds market for free zones and special economic zones. A normal classifieds market covers the whole country; Azadchi covers only these zones. On [azadchi.ir](https://azadchi.ir) I wrote that "Azad" means trade freedom in the free zones and "chi" means the business field inside those zones. A listing and a search stay around that zone. The conversation with the other party stays inside Azadchi, not as a scattered contact outside the product.

Site: [azadchi.ir](https://azadchi.ir)

### What a visitor sees

Posting on the homepage: choose a free zone and a category, add photos and details, preview, publish so the listing shows in search for that zone, then answer the buyer in chat. Search takes a zone (or all free zones), a category, and keywords, and opens chat with the seller from the listing. The coverage is not all of Iran. The range choice is all free zones, not the whole country. The page names examples such as Kish, Qeshm, Aras, Anzali, Arvand, and Chabahar, and points the rest at the zones page.

The page's main path is chat on a listing, not an offer-comparison table. Price offers exist too, but I centered the page on the zone listing and the conversation. I count the monthly free quota on the Jalali month.

### Stack

The web client is built with Vite ^6.0.7: React ^18.3.1, Tailwind ^3.4.17, React Router ^7.1.1, Leaflet ^1.9.4, `socket.io-client` ^4.8.1, and the Vazirmatn font. I used Leaflet because a zone has to be visible on a map, not only in a text list.

The API is Express ^4.21.2 on Node.js 20 or later, with `pg` ^8.13.1 for Postgres, `ioredis` ^5.4.2 for Redis, Bull ^4.16.5 for background work, Socket.IO ^4.8.1 for live conversation, `sharp` and `multer` for images, `web-push` for browser notifications, and Helmet and `express-rate-limit` for hardening. On startup the server checks the database, connects Redis, attaches Socket.IO to the same HTTP server, starts the Bull workers, then listens.

The mobile app is a Flutter shell, version `1.0.14+83`, Dart `>=3.5.0 <4.0.0`, `webview_flutter` ^4.10.0 and `speech_to_text` ^7.0.0. The market and the main paths are native and WebView is the fallback.

### The zone list lives in the app

I did not leave the range as a free-typed string. The zone list ships inside the app, and "all free zones" is one choice in that same list. It covers 21 zones: Chabahar, Kish, Qeshm, Aras, Anzali, Arvand, Maku, Imam Khomeini Airport, Incheh Borun, Bushehr, Ardabil, Sistan, Mehran, Qasr-e Shirin, Baneh and Marivan, Mazandaran, Sarakhs, Dogharun, Sero, the Piranshahr border market, and the Astara coastal market.

The Iran city list, city coordinates, and categories are separate app assets, and the Leaflet files ship with the app for the in-app map. If a zone were only a text label, "all free zones" would blur into all of Iran.

### Listing, search, chat

A listing can be created, edited, deleted, and renewed, and it carries related listings and a market price estimate. Market search has its own rate limit.

Chat is the main conversation path: list conversations, start one on a listing, read and send messages, edit and delete, hide and unhide. Joining a conversation and the typing indicator run on Socket.IO. Helmet, CORS, and a 1mb JSON body limit apply before every router.

## پروژه‌های مرتبط

- [hamejoo-intro](https://github.com/mnhashemabadi/hamejoo-intro): همه‌جو را برای بازدیدکننده‌ای ساختم که با یک عبارت آگهی را یک‌جا ببیند و برای جزئیات به سایت منبع برود.
- [alwer-intro](https://github.com/mnhashemabadi/alwer-intro): آلور را برای خریداری ساختم که درخواست بنویسد و پیشنهاد قیمت‌ها را کنار هم ببیند؛ آگهی فروش هم روی همان بازار است.
- [kasbafzar-intro](https://github.com/mnhashemabadi/kasbafzar-intro): کسب‌افزار را برای کسی ساختم که فروش و مشتری و هزینه را ثبت کند و فاکتور را با لینک پرداخت برای مشتری بفرستد.
- [afzi-intro](https://github.com/mnhashemabadi/afzi-intro): افزی را برای کوتاه کردن یک نشانی http یا https ساختم؛ باز کردن لینک کوتاه همان صفحه را باز می‌کند.
- [alweryar-intro](https://github.com/mnhashemabadi/alweryar-intro): آلوریار را برای همکاری در بررسی آگهی و همکاری در فروش آلور ساختم.
- [alwerchi-intro](https://github.com/mnhashemabadi/alwerchi-intro): آلورچی را برای فروشگاهی ساختم که کالا و موجودی‌اش در بازار آلور دیده شود و خریدار در آلور بماند.

## Related

- [hamejoo-intro](https://github.com/mnhashemabadi/hamejoo-intro): I built Hamejoo for a visitor who types one phrase, sees listings in one place, and opens the original site for the listing itself.
- [alwer-intro](https://github.com/mnhashemabadi/alwer-intro): I built Alwer for a buyer who posts a request and compares price offers side by side; a sale listing sits on the same market.
- [kasbafzar-intro](https://github.com/mnhashemabadi/kasbafzar-intro): I built Kasbafzar for someone who records sales, customers, and expenses, and sends the customer an invoice with a payment link.
- [afzi-intro](https://github.com/mnhashemabadi/afzi-intro): I built Afzi to shorten an http or https address; opening the short link opens that same page.
- [alweryar-intro](https://github.com/mnhashemabadi/alweryar-intro): I built Alweryar for collaboration on listing review and on sales for Alwer.
- [alwerchi-intro](https://github.com/mnhashemabadi/alwerchi-intro): I built Alwerchi for a shop whose goods and stock show on the Alwer market while the buyer stays on Alwer.

یادداشت مهندسی کوتاه‌تر: [docs/engineering.md](docs/engineering.md)

Shorter engineering note: [docs/engineering.md](docs/engineering.md)
