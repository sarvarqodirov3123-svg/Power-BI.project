# BlinkIT Grocery Sales — Power BI Dashboard

## Loyiha maqsadi
BlinkIT (tezkor yetkazib berish xizmati) do'konlari bo'yicha savdo ko'rsatkichlarini tahlil qilish, mahsulot va do'kon xususiyatlari kesimida savdo dinamikasini vizual tarzda kuzatish.

## Ma'lumotlar manbasi
**Jadval:** `BlinkIT Grocery Data`

| Maydon | Turi | Tavsif |
|---|---|---|
| Total Sales | Measure | Umumiy savdo summasi |
| Average Sales | Measure | Bitta tranzaksiya/mahsulot bo'yicha o'rtacha savdo |
| Average Rating | Measure | Mijozlar tomonidan qo'yilgan o'rtacha baho |
| Number of Items | Measure | Sotilgan mahsulotlar soni |
| Item Visibility | Measure (Sum) | Mahsulotning do'kon rastasidagi ko'rinuvchanlik darajasi |
| Item Type | Ustun | Mahsulot kategoriyasi (masalan: Dairy, Snacks, Fruits) |
| Item Fat Content | Ustun | Yog'lilik darajasi — Low Fat / Regular |
| Outlet Type | Ustun | Do'kon formati — Supermarket Type1/2/3, Grocery Store |
| Outlet Size | Ustun | Do'kon hajmi — Small / Medium / High |
| Outlet Location Type | Ustun | Joylashuv toifasi — Tier 1 / Tier 2 / Tier 3 |
| Outlet Establishment Year | Ustun | Do'kon ochilgan yil |

## Dashboard tarkibi (1 sahifa, 27 ta vizual)

**KPI panel (4 ta karta):** Total Sales, Average Sales, Average Rating, Number of Items — umumiy holatni bir qarashda ko'rsatadi.

**Taqsimot tahlili (Donut charts):**
- Item Fat Content bo'yicha savdo ulushi
- Outlet Size bo'yicha savdo ulushi

**Qiyosiy tahlil (Bar charts):**
- Item Type bo'yicha savdo hajmi (eng ko'p sotiladigan kategoriyalar)
- Item Fat Content × Outlet Location Type — clustered bar orqali kesishgan taqsimot

**Dinamika (Line chart):** Outlet Establishment Year bo'yicha savdo trendi — do'konlar yoshi savdoga qanday ta'sir qilishini ko'rsatadi.

**Voronka tahlili (Funnel):** Outlet Location Type bo'yicha savdo ustunligi darajasi.

**Batafsil jadval (Pivot table):** Outlet Type kesimida — Total Sales, Average Sales, Average Rating, Number of Items, Item Visibility bir vaqtda solishtiriladi.

**Interaktiv filtrlar (Slicers):** Metrics (KPI almashtirish), Outlet Location Type, Outlet Size — foydalanuvchi dashboardni real vaqtda sozlashi mumkin.

## Dizayn
- Brend sarlavhasi: **blinkit — India's last minute app**
- Fon rasm + 4 ta maxsus ikonka (Sales, Avg Sales, Items, Rating)
- Alohida **"FILTER PANE"** bloki — barcha slayzerlar shu yerda jamlangan

## Texnik tuzilma
```
Loyixa.pbix
├── DataModel        → jadval, ustun va DAX o'lchovlar
├── Report/Layout    → sahifa va vizuallar konfiguratsiyasi
├── StaticResources  → fon rasm, ikonkalar
```
