# OSINT (Ochiq manbalardan razvedka) — o'rganish rejasi

IIV'dagi suhbatda tavsiya etilgan ikkinchi yo'nalish: fishing saytlar, telefon raqamlar va IP-manzillarni **qonuniy**, ochiq servislar orqali qidirish metodlari.

## Nega muhim

OSINT — kiberjinoyatchilikni tergov qilishda dastlabki ma'lumot yig'ish bosqichi: kim, qayerdan, qanday infratuzilma orqali hujum/firibgarlik qilgani — bularning aksariyati **ochiq, umumiy mavjud** manbalardan aniqlanadi, maxsus "buzib kirish" shart emas.

## Muhim chegara (har doim yodda tutish kerak)

OSINT — faqat ochiq, hamma kira oladigan ma'lumotni yig'ish va tizimlashtirish. Quyidagilar OSINT emas, balki huquqbuzarlik:
- Birovning shaxsiy akkauntiga ruxsatsiz kirish yoki parolni sindirish
- Yopiq/himoyalangan tizimlarni skanerlash (ruxsatsiz)
- Yig'ilgan ma'lumotdan shaxsni ta'qib qilish yoki tahdid qilish uchun foydalanish

Davlat xizmatida ishlashda bu chegara ayniqsa qat'iy kuzatiladi — har bir harakat qonun va ichki protokol doirasida bo'lishi kerak.

## Amaliyot manbalari

- [TryHackMe — OhSINT](https://tryhackme.com/room/ohsint) — klassik boshlang'ich OSINT xonasi: bitta rasmdan boshlab, foydalanuvchi haqida ochiq ma'lumot yig'ish zanjiri
- [TryHackMe — Shodan.io](https://tryhackme.com/room/shodan) — internetga ulangan qurilmalarni qonuniy qidirish vositasi, rasmiy xona
- [TryHackMe — OSINT mavzusi (barcha tegishli xonalar)](https://tryhackme.com/topics/osint)

### Qo'shimcha — [uttambodara/TryHackMeRoadmap](https://github.com/uttambodara/TryHackMeRoadmap) ro'yxatidan saralangan

OhSINT va Shodan.io'dan keyin davom ettirish uchun quyidagi nomlar ham ro'yxatda bor (aniq havolasi tasdiqlanmagani uchun TryHackMe qidiruvi orqali topish tavsiya etiladi): **Google Dorking**, **WebOSINT**, **Searchlight - IMINT**, **Geolocating Images** (rasm metama'lumoti orqali joylashuvni aniqlash — tergov ishida ayniqsa foydali ko'nikma).

## Asosiy vositalar (qonuniy, ochiq)

| Vosita | Vazifasi |
|--------|----------|
| Google dorking (`site:`, `filetype:`, `intitle:`) | Qidiruv operatorlari orqali maxsus ma'lumot topish |
| [Shodan](https://www.shodan.io/) | Internetga ulangan qurilmalar/portlarni qidirish |
| [VirusTotal](https://www.virustotal.com/) | Domen/IP/fayl obro'sini (reputatsiyasini) tekshirish |
| WHOIS (`whois domain.com`) | Domen ro'yxatdan o'tkazilgan egasi va sanasi |
| [Have I Been Pwned](https://haveibeenpwned.com/) | Email/akkaunt sizib chiqqan ma'lumotlar bazasida bor-yo'qligini tekshirish |

## Misol — oddiy Google dork

```
site:pastebin.com "password" "uzbekistan"
filetype:xls "parol"
```

## Holat

- [ ] OhSINT xonasini yechish — bajarilmagan
- [ ] Shodan'da oddiy qidiruv sinab ko'rish (masalan ochiq kameralar/routerlar — faqat ko'rish, ulanmasdan)
- [ ] Bitta real fishing domenni WHOIS + VirusTotal orqali tekshirish (masalan oldin uchragan shubhali havola)
- [x] Mustaqil mashq: ochiq, umumiy ko'rinadigan professional profilni cross-platform usulda xaritalash (quyida)

> Har bir mashq tugatilgach, shu faylga qanday metod ishlatilgani va nima topilgani qisqa yozib boriladi.

---

## Mustaqil mashq #1 — Cross-platform username correlation (2026-11-09)

**Maqsad obyekt:** ochiq, hammaga ko'rinadigan professional YouTube kanali (o'z xohishi bilan reklama/brend uchun ochiq qoldirilgan "About" sahifa — shaxsiy, yopiq profil emas).

**Metod:** kanalning "Haqida" (About) bo'limida ko'rsatilgan havolalar zanjirini yig'ish va ularning izchilligini tahlil qilish.

**Topilgan ma'lumotlar (kanal o'zi ochiq ko'rsatgan):**

| Platforma | Username/havola |
|---|---|
| YouTube | `@Nursaidovuz` |
| Veb-sayt | `nursaidov.uz` |
| Telegram | `t.me/nursaidovuz` |
| Facebook | `facebook.com/Nursaidovuz` |
| Instagram | `instagram.com/nursaidovuz` |
| Joylashuv (platforma ko'rsatgan) | Germaniya |

**Tahlil (3-4 jumlada xulosa):**

Barcha platformalarda **bir xil username (`nursaidovuz`)** ishlatilgani — kuchli kross-platforma identifikatsiya belgisi: bitta akkauntni topish orqali butun "raqamli iz" (digital footprint) zanjirini qayta tiklash mumkin. Bu — OSINT'da eng tez-tez ishlatiladigan dastlabki texnikalardan biri, chunki content maker'lar brend izchilligi uchun username'ni har joyda bir xil saqlaydi. Platforma ko'rsatgan joylashuv (Germaniya) va kontent tili (o'zbekcha) o'rtasidagi farq — bu xato yoki shubha emas, balki diaspora kontent-meykerlari uchun odatiy holat, lekin tergov metodologiyasida har doim alohida qayd etiladi. Qo'shimcha chuqurlashtirish (masalan domen WHOIS tarixi) orqali profilni yanada aniqlashtirish mumkin, lekin bu mashqda faqat ochiq ko'rinadigan "About" ma'lumoti bilan cheklanildi.

**Cheklov/eslatma:** bu — shaxsiy, yopiq profil emas, balki o'z ixtiyori bilan ochiq qoldirilgan biznes/brend sahifasi (266 video, 6+ ming obunachi, reklama uchun ochiq kontakt havolalari). OSINT mashqi faqat shunday **ochiq, rozilik bilan e'lon qilingan** ma'lumot bilan cheklanishi kerak — xususiy shaxslarning yopiq profillarini bunday tahlil qilish OSINT emas, balki maxfiylik buzilishi hisoblanadi.
