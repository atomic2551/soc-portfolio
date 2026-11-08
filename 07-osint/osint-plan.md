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

> Har bir mashq tugatilgach, shu faylga qanday metod ishlatilgani va nima topilgani qisqa yozib boriladi.
