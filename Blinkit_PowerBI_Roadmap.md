# BLINKIT Power BI Dashboard — To'liq Ish Rejasi (Roadmap)

**Manba:** YouTube video darsligi — "Blinkit Grocery Sales Analysis — End-to-End Power BI Project"
**Ma'lumot fayli:** `BlinkIT Grocery Data.xlsx` (8 523 qator, 12 ustun)
**Format:** Har bir qadam uchun — *nima qilindi → qanday qilindi → nima uchun qilindi*

Bu hujjat video ichida ko'rsatilgan **aynan o'sha ketma-ketlikda** tuzilgan — ya'ni siz videoni ochib, shu bosqichlarni birma-bir bajarib borsangiz, natija videodagi dashboard bilan bir xil chiqadi.

---

## 0. Loyiha haqida umumiy tushuncha

Blinkit — Zomato'ga tegishli hindistonlik onlayn oziq-ovqat yetkazib berish (grocery) xizmati. Loyihada siz ham "mijoz" (Blinkit egasi), ham "developer" (Power BI mutaxassisi) rolida bo'lasiz: avval o'zingizga biznes talab (business requirement) qo'yasiz, keyin o'sha talablarga javob beradigan dashboard quriladi.

**Nima uchun aynan shunday tartib muhim:** video davomida muallif alohida ta'kidlaydi — real loyihalarning **~70% qismi** talablarni to'g'ri yozib olish va ma'lumotda o'sha ma'lumot bor-yo'qligini tekshirishda "tugaydi". Ya'ni avval nima kerakligini qog'ozga yozib, keyin data ustunlarini shu talab bilan solishtirish kerak — aks holda o'rtada qayta ishlashga to'g'ri keladi.

---

## 1-BOSQICH: Biznes talablarini yig'ish (Business Requirements)

Power BI'ni ochishdan OLDIN bajariladi. Video mualliflig o'zi "mijoz" sifatida quyidagi talablarni beradi.

### 1.1. KPI (Key Performance Indicator) talablari

| # | KPI | Ta'rifi | Nima uchun kerak |
|---|---|---|---|
| 1 | **Total Sales** | Sotilgan barcha mahsulotlardan olingan umumiy tushum | Biznesning yuqori darajadagi umumiy holatini bir raqamda ko'rsatadi |
| 2 | **Average Sales** | Har bir buyurtma/qator bo'yicha o'rtacha savdo qiymati | Bitta o'rtacha tranzaksiya qanchalik "og'ir"ligini ko'rsatadi |
| 3 | **Number of Items** | Sotilgan mahsulotlar (qatorlar) soni | Umumiy hajm/aylanmani ko'rsatadi |
| 4 | **Average Rating** | Mijozlar tomonidan qo'yilgan reyting o'rtachasi | Xizmat va mahsulot sifatini (mijoz mamnuniyatini) ko'rsatadi |

**Nima uchun aynan shu 4 tasi:** bular — yuqori darajadagi (high-level) ko'rsatkichlar; ular bilan "biznes to'g'ri yo'nalishda ketyaptimi" degan savolga bir qarashda javob olinadi. Detalga chuqur kirish uchun esa grafiklar kerak bo'ladi (keyingi band).

### 1.2. Grafik (Chart) talablari

| # | Tahlil mavzusi | Asosiy metrik | Qo'shimcha metrikalar (dinamik) | Tavsiya etilgan grafik turi |
|---|---|---|---|---|
| 1 | Total Sales **by Fat Content** | Total Sales | Avg Sales, Number of Items, Avg Rating | Donut chart |
| 2 | Total Sales **by Item Type** | Total Sales | Avg Sales, Number of Items, Avg Rating | Bar chart |
| 3 | Fat Content **by Outlet (location)** for Total Sales | Total Sales | Avg Sales, Number of Items, Avg Rating | Stacked/Clustered bar chart |
| 4 | Total Sales **by Outlet Establishment** (yil) | Total Sales | — | Line chart |
| 5 | Sales **by Outlet Size** | Total Sales | — | Donut chart |
| 6 | Sales **by Outlet Location** (Tier 1/2/3) | Total Sales | — | Funnel chart |
| 7 | Barcha metrikalar **by Outlet Type** | Total Sales, Number of Items, Avg Sales, Avg Rating, Item Visibility | — | Matrix (jadval) |

**Nima uchun grafik turi mijoz tomonidan berilgan:** real loyihalarda mijoz har doim ham grafik turini aytmaydi — ba'zida faqat talabni beradi, tanlov sizga qoladi. Bu yerda video mualliflig o'quv maqsadida grafik turlarini ham tavsiya qilib beradi, lekin bu qat'iy qoida emas — tajriba bilan "qaysi grafik qaysi ma'lumot uchun ko'proq insight beradi" degan savolga javob topish kerak.

**Muhim amaliy qoida:** har bir talab uchun o'zingizga savol bering — *"Bu ko'rsatkichni hisoblash uchun menda kerakli ustun bormi?"* Agar yo'q bo'lsa — uni hisoblab chiqarish (DAX yoki Power Query orqali) yo'lini toping.

---

## 2-BOSQICH: Xom ma'lumot bilan tanishish (Data Walkthrough)

Excel faylini ochib, tuzilishini o'rganish — Power BI'ga tegishdan oldin.

**Hajm:** 8 523 qator (order/qator = bitta sotilgan mahsulot), 12 ustun (12 field).

| # | Ustun nomi | Tavsifi | Turi |
|---|---|---|---|
| 1 | Item Fat Content | Mahsulotdagi yog' miqdori toifasi (Low Fat / Regular) | Dimension (matn, tozalash talab qiladi) |
| 2 | Item Identifier | Mahsulotni bir noyob kod bilan aniqlovchi ID (masalan FDX32) | Dimension (ID) |
| 3 | Item Type | Mahsulot toifasi (Snack Foods, Soft Drinks, Frozen Foods, Household va h.k.) | Dimension |
| 4 | Outlet Establishment Year | Do'kon (outlet) qaysi yilda ochilgani | Dimension (yil) |
| 5 | Outlet Identifier | Do'konni aniqlovchi noyob kod | Dimension (ID) |
| 6 | Outlet Location Type | Do'kon joylashgan shahar toifasi — Tier 1 / Tier 2 / Tier 3 | Dimension |
| 7 | Outlet Size | Do'kon hajmi — Small / Medium / High | Dimension |
| 8 | Outlet Type | Do'kon turi — Supermarket Type1/2/3 yoki Grocery Store | Dimension |
| 9 | Item Visibility | Mahsulotning qidiruvda/ilovada qanchalik ko'rinishi (visibility ko'rsatkichi) | O'lchov (foiz) |
| 10 | Item Weight | Mahsulot og'irligi (ba'zi qatorlarda bo'sh — muammo emas) | O'lchov |
| 11 | Sales | O'sha buyurtma bo'yicha savdo summasi | O'lchov (asosiy metrik manbasi) |
| 12 | Rating | Mijoz tomonidan qo'ygan baho | O'lchov |

**Nima uchun bu qadam muhim:** Har bir ustunni 1-bosqichdagi talablar bilan solishtirib chiqiladi — masalan "Total Sales by Fat Content" talabi uchun `Item Fat Content` va `Sales` ustunlari borligi tasdiqlanadi. Shu tekshiruv keyingi barcha ishni osonlashtiradi.

---

## 3-BOSQICH: Power BI'ni ma'lumotga ulash (Data Connection)

| # | Qilingan ish | Qanday qilinadi | Nima uchun |
|---|---|---|---|
| 1 | Bo'sh Power BI Desktop workbook ochish | Power BI Desktop dasturi ishga tushiriladi | Loyihani boshlash uchun toza muhit kerak |
| 2 | Ma'lumotga ulanish | `Home → Get Data → Excel Workbook` → faylni (`BlinkIT Grocery Data.xlsx`) tanlash | Excel — bu loyihadagi manba (source) format |
| 3 | Jadvalni tanlash va yuklash | Navigator oynasida jadval tanlanadi → **Load** bosiladi | Load — ma'lumotni to'g'ridan-to'g'ri modelga olib kiradi (keyinroq tozalash uchun Transform ham ishlatiladi) |
| 4 | Yuklangan qatorlar sonini tekshirish | Table View'da pastda 8 523 qator ko'rsatilishini tasdiqlash | Excel'dagi 8 524 qator (header bilan) — header hisobga olinmagani uchun Power BI'da 1 ta kam ko'rinadi; bu **normal holat**, xato emas |
| 5 | Ustun tiplarini ko'zdan kechirish | Har bir ustun yonidagi belgi (ABC=matn, 123=son, Σ=summalanadigan son) tekshiriladi | Power BI raqamli ustunlarni avtomatik aniqlaydi, lekin buni bilish (interview savoli sifatida ham) muhim |

---

## 4-BOSQICH: Ma'lumot sifatini tekshirish va tozalash (Power Query)

Bu — **Power Query Editor** (`Home → Transform Data`) ichida bajariladi.

| # | Qilingan ish | Qanday qilinadi | Nima uchun qilindi |
|---|---|---|---|
| 6 | Power Query Editor'ni ochish | `Home → Transform Data` | Barcha tozalash amallari shu yerda bajariladi va tarixi saqlanadi (**Applied Steps** paneli) |
| 7 | `Item Fat Content` ustunidagi nomuvofiqliklarni aniqlash | Ustun ustiga bosib, mavjud qiymatlarni ko'rish: `LF`, `Low Fat`, `low fat`, `Regular`, `RG` | Bitta ma'noni bildiruvchi qiymatlar turlicha yozilgan bo'lsa, grafiklarda alohida-alohida (noto'g'ri) kategoriya bo'lib chiqadi |
| 8 | `LF` → `Low Fat` almashtirish | O'ng tugma → **Replace Values** → "LF" → "Low Fat" | Qisqartma to'liq va tushunarli nomga keltiriladi |
| 9 | `RG` → `Regular` almashtirish | Xuddi shunday **Replace Values** orqali | Xuddi shu sabab — nomlanishni birxillashtirish |
| 10 | `low fat` → `Low Fat` (katta-kichik harf) almashtirish | Yana **Replace Values** orqali case (registr) to'g'rilanadi | "low fat" va "Low Fat" Power BI'da ikkita **turli** matn sifatida ko'riladi — vizual darajasida bittalashtirish uchun ustunni ham tozalash shart |
| 11 | Har bir qadamning **Applied Steps** panelida saqlanganini tekshirish | Panelga qarab, 3 ta "Replaced Value" qadami ro'yxatda ko'rinishi kuzatiladi | Bu — o'zgarishlar tarixi; boshqa foydalanuvchi/hamkasb keyinchalik qanday tozalash qilinganini shu yerdan ko'ra oladi |
| 12 | Ustun sifatini tekshirish (**Column Quality**) | `View → Column Quality` yoqiladi | Har bir ustun uchun **Valid / Error / Empty** foizini ko'rsatadi — sifat nazorati uchun standart amaliyot |
| 13 | Dimension ustunlar 100% Valid ekanini tasdiqlash | `Item Fat Content` kabi ustunlarda Valid = 100%, Error = 0%, Empty = 0% ko'rilishi kerak | Tavsiflovchi (kategoriya) ustunlarda bo'sh/xato qiymat bo'lmasligi kerak — aks holda tahlil chalg'iydi |
| 14 | `Item Weight` ustunidagi bo'sh qiymatlarga e'tibor berish, lekin ularni **tuzatmaslik** | Column Quality'da Valid ≈ 84%, Empty ≈ 16% ko'riladi | Bu ustun dashboardda ishlatilmagani uchun hozircha muammo emas — **faqat kerakli ustunlarga vaqt sarflanadi**, bu ustun kelajakda kerak bo'lsa qaytib tozalanadi |
| 15 | O'zgarishlarni modelga qaytarish | `Home → Close & Apply` | Power Query'da qilingan barcha tozalash amallari asosiy Power BI modeliga (jadval va vizuallarga) qo'llaniladi |

**Nima uchun bu bosqich butun loyihaning eng muhim qismlaridan biri:** noto'g'ri yoki nomuvofiq matn qiymatlari keyinchalik grafiklarda, slicerlarda va DAX hisob-kitoblarida noto'g'ri natija beradi — masalan "Low Fat" bo'lib ikki marta hisoblanadigan mahsulotlar sabab umumiy foiz noto'g'ri chiqadi.

---

## 5-BOSQICH: DAX o'lchovlarini (Measures) yaratish

Report View'da, jadval ustiga o'ng tugma bosib **New Measure** orqali yaratiladi.

| # | Measure nomi | DAX formulasi | Nima uchun aynan shu funksiya |
|---|---|---|---|
| 16 | Total Sales | `Total Sales = SUM(BlinkIT_Data[Sales])` | Barcha savdolarning yig'indisi — umumiy tushum |
| 17 | Average Sales | `Average Sales = AVERAGE(BlinkIT_Data[Sales])` | Har bir buyurtma bo'yicha o'rtacha qiymatni beradi |
| 18 | Number of Items | `Number of Items = COUNTROWS(BlinkIT_Data)` | Har bir qator = bitta sotilgan mahsulot, shuning uchun qatorlar soni sanaladi (SUM emas, COUNT) |
| 19 | Average Rating | `Average Rating = AVERAGE(BlinkIT_Data[Rating])` | Mijozlar bahosining o'rtachasini beradi |

**Nima uchun measure (o'lchov) sifatida, ustun sifatida emas:** measure'lar dinamik — qaysi filtr/slicer tanlansa, o'sha kesimga mos avtomatik qayta hisoblanadi. Bu dashboardni interaktiv qiladi.

---

## 6-BOSQICH: Sahifa (canvas) va umumiy dizayn asosini sozlash

| # | Qilingan ish | Sozlama | Nima uchun |
|---|---|---|---|
| 20 | Report sahifasi o'lchamini o'zgartirish | `Format page → Canvas settings → Type: Custom` — balandlik **800px**, kenglik **1400px** | Standart 16:9 o'lcham keng dashboardlar uchun tor keladi; custom o'lcham barcha elementlarga joy beradi |
| 21 | Canvas fonini sozlash | Fon rangi — oq (`#FFFFFF`), shaffoflik **40%** | Ortiqcha yorqin oq fon o'rniga yumshoqroq, professional ko'rinish beradi |
| 22 | Umumiy rang palitrasini tanlash | Asosiy ranglar — **sariq** (`#FFD200`) va **yashil** | Blinkit brendining o'zi ilovasida sariq-yashil ranglardan foydalanadi — dashboard shu brend uslubiga moslashtiriladi (brend izchilligi) |

---

## 7-BOSQICH: Chap panel (branding) va sarlavha qurish

| # | Qilingan ish | Qanday qilinadi | Nima uchun |
|---|---|---|---|
| 23 | Chap tomonda "banner" shakl qo'yish | `Insert → Shapes → Rounded tab both top`, 90° aylantirilib, balandlik 750px, kenglik 205px, rang `#FFD200`, Shadow yoqilgan | Dashboardga vizual "chegara"/brend paneli beradi, chap tomonni asosiy kontentdan ajratadi |
| 24 | Dashboard nomini qo'shish | `Insert → Text Box` — "BLINKIT" matni, shrift 36pt, Segoe UI Bold, yashil rang | Foydalanuvchi birinchi qarashda qaysi kompaniya/mahsulot haqida ekanini bilishi uchun |
| 25 | Subtitle qo'shish | "India's last minute app" matni, kichikroq shrift (≈10pt, bold) | Blinkitning brend shiori — dashboardga qo'shimcha kontekst va professional ko'rinish beradi |

---

## 8-BOSQICH: KPI kartalarini qurish

| # | Qilingan ish | Qanday qilinadi | Nima uchun |
|---|---|---|---|
| 26 | 4 ta **Card (New)** vizualini qo'shish | Har biriga navbatma-navbat Total Sales, Average Sales, Number of Items, Average Rating measure'lari tortiladi | 1-bosqichdagi 4 ta KPI talabini to'g'ridan-to'g'ri bajaradi |
| 27 | Kartalarni 2×2 grid qilib joylashtirish | `Format visual → Layout → Grid`, max rows = 2, max columns = 2, spacing = 0 | Har birini alohida-alohida joylashtirish o'rniga, avtomatik va tekis grid beradi |
| 28 | Sarlavhalarni katta harfga o'tkazish | Har bir maydonni qo'lda tahrirlab (masalan "Total Sales" → "TOTAL SALES") nomlash | Vizual izchillik va "dashboard" uslubiga mos ko'rinish uchun |
| 29 | Qiymat va label formatini sozlash | Shrift Segoe UI Semibold, o'lcham va rang moslashtiriladi, label pastda joylashadi | O'qilishni osonlashtiradi, barcha kartalarda bir xil uslub saqlanadi |
| 30 | Sonlarni formatlash | Total Sales — Millions birligida, valyuta belgisi (`$`) qo'shilgan, 2 xona kasr; Average Rating — 1 xona kasr; Number of Items — butun son | Katta raqamlar (millionlab) o'qilishi qiyin bo'lib qolmasligi uchun qisqartiriladi |
| 31 | Har bir kartaga fon rasm va icon qo'shish | `Format visual → Images` — har bir KPI uchun mos ikonka (savdo, reyting va h.k.) va fon rasmi (`background kpi.png`), shaffoflik 40% | Dashboardni "gapiradigan" (informativ va jozibali) qiladi — faqat raqam emas, vizual ma'no ham qo'shadi |
| 32 | Karta shaklini formatlash | Rounded rectangle, radius 10px, Shadow yoqilgan, wide padding, chap tomonda accent bar (5px, to'q yashil) | Zamonaviy "card" dizayn uslubi — har bir KPI alohida ajralib turadigan blok ko'rinishida bo'ladi |

---

## 9-BOSQICH: "Mahsulot" (Product) bo'limi grafiklari

Bu bo'limda 3 ta grafik quriladi: Fat Content, Fat by Outlet, Item Type.

| # | Qilingan ish | Qanday qilinadi | Nima uchun |
|---|---|---|---|
| 33 | Grafiklar uchun konteyner (placeholder) shakl qo'yish | `Insert → Shapes → Rounded rectangle`, oq rang 10% shaffoflik, border va shadow | Grafiklarni vizual jihatdan bir guruh (panel) ichiga jamlaydi |
| 34 | **Field Parameter** yaratish (nomi: `Metrics`) | `Modeling → New parameter → Fields` — Total Sales, Average Sales, Number of Items, Average Rating tanlanadi | Bitta grafikda 4 ta har xil metrikani (Total Sales / Avg Sales / va h.k.) **almashtirib ko'rsatish** uchun — foydalanuvchi bir grafikni 4 xil ko'rinishda ko'ra oladi, alohida-alohida grafik yasash shart emas |
| 35 | **Donut chart**: Fat Content by Metrics | `Fat Content` — Legend'ga, `Metrics` (field parameter) — Values'ga qo'yiladi | 1.2-band talabi: Total Sales by Fat Content + qo'shimcha metrikalar bo'yicha dinamik ko'rish |
| 36 | Field parameter'ni **slicer** sifatida qo'shish | Yaratilgan `Metrics` jadvali slicer sifatida donut chart yoniga joylashtiriladi, single-select | Foydalanuvchi qaysi metrikani (Total Sales / Avg Sales / Items / Rating) ko'rmoqchi bo'lsa, shuni tanlab, donut chart avtomatik yangilanadi |
| 37 | Donut markaziga jami qiymat kartasi qo'shish | Kichik **Card** vizuali donut chart markaziga joylashtiriladi, fon o'chirilgan | Donut chartning markazidagi bo'sh joydan foydalanib, tanlangan metrikaning umumiy summasini ko'rsatadi |
| 38 | Rang kodlash | Low Fat va Regular uchun alohida hex ranglar beriladi (sariq/yashil palitraga mos) | Kategoriyalarni vizual jihatdan aniq va brendga mos ajratish uchun |
| 39 | **Clustered bar chart**: Fat by Outlet | X-axis: `Metrics`, Y-axis: `Outlet Location Type`, Legend: `Item Fat Content` | 1.3-band talabi: Fat Content by Outlet — qaysi tier'da qaysi fat content ko'proq sotilishini ko'rsatadi |
| 40 | **Stacked bar chart**: Item Type | X-axis: `Item Type`, Values: `Metrics` | 1.2-band talabi: Total Sales by Item Type — qaysi mahsulot toifasi eng ko'p sotilishini ko'rsatadi |
| 41 | Bo'limlar orasiga ajratuvchi chiziqlar (divider) qo'shish | `Insert → Shapes → Line`, ingichka, kulrang | Grafiklarni vizual jihatdan bir-biridan ajratib, o'qishni osonlashtiradi |

**Nima uchun Field Parameter ishlatilgan (umumiy tushuntirish):** Agar har bir metrik (Total Sales, Avg Sales, Items, Rating) uchun alohida-alohida grafik yasalsa, dashboard juda katta va tartibsiz bo'lib qolardi. Field Parameter bitta grafik joyidan 4 xil tahlilni olish imkonini beradi — bu Power BI'dagi ilg'or (advanced) va joy tejaydigan texnika.

---

## 10-BOSQICH: "Outlet" (do'kon) bo'limi grafiklari

Bu bo'limda 4 ta grafik quriladi: Establishment (Line), Size (Donut), Location (Funnel), Type (Matrix).

| # | Qilingan ish | Qanday qilinadi | Nima uchun |
|---|---|---|---|
| 42 | **Line chart**: Outlet Establishment | X-axis: `Outlet Establishment Year`, Values: `Total Sales` | 1.4-band talabi: qaysi yilda ochilgan do'konlar qanday savdo qilayotganini trend sifatida ko'rsatadi |
| 43 | Line chart formatlashtirish | Smooth interpolatsiya, shaded area (soya), markerlar, data label | O'qish uchun aniqroq va vizual jihatdan boy chiziq grafik |
| 44 | **Donut chart**: Outlet Size | Legend: `Outlet Size`, Values: `Total Sales` | 1.5-band talabi: Small / Medium / High o'lchamdagi do'konlar bo'yicha savdo taqsimoti |
| 45 | **Funnel chart**: Outlet Location | Category: `Outlet Location Type` (Tier 1/2/3), Values: `Total Sales` | 1.6-band talabi: qaysi tier eng ko'p savdo qilishini pog'onali (funnel) ko'rinishda ko'rsatadi |
| 46 | **Matrix (jadval)**: Outlet Type bo'yicha barcha metrikalar | Rows: `Outlet Type`, Values: Total Sales, Number of Items, Average Sales, Average Rating, Item Visibility | 1.7-band talabi: bitta jadvalda barcha asosiy ko'rsatkichlarni Outlet turi bo'yicha taqqoslash |
| 47 | Matrix'ni formatlashtirish | Layout — Minimal, har bir ustunga alohida fon rangi (masalan Total Sales — sariq, Number of Items — yashil), sub-totalllar o'chirilgan | O'qishni osonlashtiradi va har bir metrikani rang orqali tezda ajratib olish imkonini beradi |

---

## 11-BOSQICH: Slicer (filtr)larni qo'shish

| # | Qilingan ish | Qanday qilinadi | Nima uchun |
|---|---|---|---|
| 48 | **Outlet Location Type** slicer | `Outlet Location Type` maydoni slicer sifatida qo'yiladi, dropdown, multi-select | Foydalanuvchi Tier 1/2/3 bo'yicha butun dashboardni filtrlashi uchun |
| 49 | **Outlet Size** slicer | `Outlet Size` maydoni slicer sifatida qo'yiladi | Small/Medium/High bo'yicha filtrlash imkoniyati |
| 50 | **Item Type** slicer | `Item Type` maydoni slicer sifatida qo'yiladi | Har bir mahsulot toifasi (masalan faqat "Dairy") bo'yicha butun dashboardni ko'rish imkoniyati |
| 51 | Slicerlarni formatlashtirish | Fon — sariq (`#FFD200`), matn — Segoe UI Semibold, border qo'shilgan | Dashboardning umumiy rang uslubiga mos, alohida ajralib turadigan filtr paneli |

---

## 12-BOSQICH: Interaktivlikni sozlash (Edit Interactions)

| # | Qilingan ish | Qanday qilinadi | Nima uchun |
|---|---|---|---|
| 52 | Har bir vizual uchun **Edit Interactions** rejimini yoqish | Bir grafik tanlanadi → `Format → Edit interactions` | Standart holatda Power BI bosilgan elementni faqat **highlight** (bo'yab ko'rsatish) qiladi, to'liq filtrlamaydi |
| 53 | Highlight o'rniga **Filter** rejimini tanlash | Har bir boshqa vizual ustidagi ikonkalardan "Filter" varianti bosiladi (barcha grafik-grafik juftliklari uchun takrorlanadi) | Foydalanuvchi bir chartning bo'lagini (masalan "Low Fat") bossa, boshqa barcha grafiklar **to'liq filtrlanib**, faqat shu kesimga oid ma'lumotni ko'rsatishi uchun — bu "highlight"dan ko'ra ancha aniq va tushunarli tajriba beradi |

---

## 13-BOSQICH: Navigatsiya va yakuniy UX elementlari

| # | Qilingan ish | Qanday qilinadi | Nima uchun |
|---|---|---|---|
| 54 | Filtr panelига sarlavha/icon qo'shish | "Filters" matni va filtr belgisi (icon) chap panelga joylashtiriladi | Foydalanuvchi filtr paneli qayerdaligini tezda tushunishi uchun |
| 55 | **Reset/Clear filters** imkoniyatini tushuntirish | Power BI Desktop'da `Ctrl` bosib slicer elementiga bosilsa, tanlov bekor qilinadi (Power BI Service'da esa oddiy bosish yetarli) | Foydalanuvchi barcha filtrlarni bitta harakat bilan tozalab, to'liq ma'lumotga qaytishi uchun |
| 56 | **Home** tugmasi qo'yish | Shakl/icon qo'yilib, unga (agar bir nechta sahifa bo'lsa) asosiy sahifaga qaytish harakati bog'lanadi | Ko'p sahifali dashboardlarda foydalanuvchi tajribasini yaxshilaydi — bu loyihada 1 sahifa bo'lsa ham, kengaytirish uchun tayyor infratuzilma sifatida qo'yiladi |

---

## 14-BOSQICH: Insightlarni yig'ish va yakuniy xulosa

Har bir chart tayyor bo'lgach, undan qanday insight (xulosa) olish mumkinligini yozib borish kerak — bu mijozga taqdim etiladigan yakuniy hisobotning asosini tashkil qiladi.

| Grafik | Video davomida chiqqan asosiy insight |
|---|---|
| KPI kartalar | Jami savdo ≈ **$1.2 mln**, o'rtacha savdo ≈ **$141**, jami **8 523 ta** mahsulot sotilgan, o'rtacha reyting **3.9** (4 dan past — xizmat/sifatni yaxshilash zarurligini ko'rsatadi) |
| Fat Content (donut) | Buyurtmalarning **≈65%** Low Fat, **≈35%** Regular mahsulotlarga to'g'ri keladi |
| Fat by Outlet | **Tier 3** shaharlarda eng ko'p savdo, undan keyin Tier 2, so'ng Tier 1; barcha tier'larda Low Fat ustunlik qiladi |
| Item Type | **Fruits & Vegetables** eng ko'p sotiladigan toifa, undan keyin Snack Foods va Household mahsulotlar |
| Outlet Establishment (line) | 2011-yilda ochilgan do'konlar past savdo qiladi; 2012–2017 oralig'ida barqaror; **2018-yilda ochilganlar eng yuqori savdo** ko'rsatadi; 2020 va 2022 ham o'rtacha yaxshi natija beradi |
| Outlet Size (donut) | **Medium** hajmdagi do'konlar eng ko'p savdo qiladi, keyin Small, eng kam esa **High** (yangi ochilganligi sabab bo'lishi mumkin) |
| Outlet Location (funnel) | Tier taqsimoti Fat by Outlet grafigidagi tendensiyani tasdiqlaydi — Tier 3 yetakchi |
| Outlet Type (matrix) | Turli do'kon turlari (Supermarket Type1/2/3, Grocery Store) bo'yicha barcha 5 ta metrikani bir joyda taqqoslash imkonini beradi |

**Nima uchun bu bosqich alohida ajratilgan:** dashboard — bu vosita, lekin loyihaning yakuniy qiymati undan chiqarilgan **xulosalarda**. Har bir chartdan 1–2 gapli insight yozib borish, keyinchalik mijozga (yoki portfolio/rezyume uchun) yig'ma xulosa (executive summary) tayyorlashni osonlashtiradi.

---

## Umumiy ketma-ketlik jadvali (qisqacha)

| Bosqich | Nima qilinadi | Asosiy vosita |
|---|---|---|
| 1. Business Requirements | KPI va chart talablarini yozib olish | Qog'oz / matn hujjat |
| 2. Data Walkthrough | Excel ustunlarini talablar bilan solishtirish | Excel |
| 3. Data Connection | Faylni Power BI'ga ulash va yuklash | Power BI — Get Data |
| 4. Data Cleaning | Nomuvofiq matnlarni tozalash, sifatni tekshirish | Power Query Editor |
| 5. DAX Measures | 4 ta asosiy o'lchovni yozish | Power BI — DAX |
| 6. Canvas Setup | Sahifa o'lchami, fon, rang palitrasini belgilash | Power BI — Format page |
| 7. Branding | Chap panel, sarlavha, subtitle | Shapes, Text box |
| 8. KPI Cards | 4 ta KPI kartani qurish va formatlash | Card visual |
| 9. Product Charts | Fat Content, Fat by Outlet, Item Type grafiklari + Field Parameter | Donut, Bar, Field Parameter |
| 10. Outlet Charts | Establishment, Size, Location, Type grafiklari | Line, Donut, Funnel, Matrix |
| 11. Slicers | 3 ta interaktiv filtr qo'shish | Slicer visual |
| 12. Edit Interactions | Highlight'ni Filter'ga almashtirish | Format → Edit interactions |
| 13. Navigation/UX | Filtr paneli, Home tugmasi, reset tushunchasi | Shapes, bookmarks (ixtiyoriy) |
| 14. Insights | Har bir grafikdan xulosa yozib borish | Yakuniy hisobot |

---

## Texnik eslatmalar

- **Rang kodlari** (masalan `#FFD200`, `#CDA900`, `#568949` va h.k.) videoda ovoz orqali aytilgan bo'lib, aniqligini o'zingiz videoni pauza qilib, Power BI'dagi rang tanlash oynasida tekshirib ko'rishingiz tavsiya etiladi — transkripsiyada raqamlar noaniq eshitilishi mumkin.
- Ushbu papkada loyiha uchun tayyor resurslar mavjud: `BlinkIT Grocery Data.xlsx` (asosiy ma'lumot fayli), `background kpi.png` va `Images` papkasi (KPI kartalar uchun fon/ikonkalar), shuningdek `SQL Data and Doc` papkasi (agar xohlasangiz, xuddi shu ma'lumot ustida SQL orqali ham mashq qilish uchun).
- Field Parameter (9-bosqich, 34-band) — Power BI Desktop'ning nisbatan yangi va "advanced" funksiyasi; agar sizning Power BI versiyangizda ko'rinmasa, `File → Options → Preview features`dan yoqilganini tekshiring.

---

*Ushbu roadmap YouTube video darsligining audio transkripti asosida tuzildi va bosqichlar videodagi haqiqiy ketma-ketlikka mos keladi. Har bir bosqichni video bilan parallel bajarib borish tavsiya etiladi.*
