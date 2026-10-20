# Veb hujumlarini loglardan aniqlash: SQLi, XSS, Open Redirect

Maqsad: veb-server access log'ida hujum izini topib, uni qanday tasdiqlashni bilish.

## Access log nimani ko'rsatadi
Manba IP, vaqt, so'ralgan URL, HTTP usuli, User-Agent va javob kodi (ba'zan javob hajmi).

## Umumiy aniqlash qadamlari
1. **URL'ni dekodlang.** Brauzer maxsus belgilarni `%27`, `%20`, `%3C` ko'rinishiga o'tkazadi. Dekodlagach, hujum so'zlari ochiq ko'rinadi.
2. **Vaqtga qarang.** Bir soniyada o'nlab so'rov (masalan, 50+) bo'lsa, bu avtomatik skaner.
3. **User-Agent'ni tekshiring.** Ba'zi vositalar o'zini ko'rsatadi (`sqlmap`, `urllib` kutubxonasi va hokazo).
4. **Yuklamaning murakkabligi.** Qo'lda sinaydigan odam oddiy yuklamadan boshlaydi. Birdaniga murakkab yuklamalar avtomatik vositaning belgisi.
5. **Manba IP'ni tekshiring.** Agar IP Cloudflare kabi CDN'ga tegishli bo'lsa, haqiqiy manba ko'rinmaydi.
6. **Hujum muvaffaqiyatli bo'ldimi?** Javob hajmi yoki javob kodiga qarab taxmin qilinadi. Aniq bilmasangiz, katta tahlilchiga yuboring (escalate).

> Muhim: real log'larni uchinchi tomon onlayn dekoderlariga yuklamang. O'quv log'lari bundan mustasno.

## SQL Injection (SQLi)
Foydalanuvchi kiritgan ma'lumot tozalanmasdan SQL so'roviga qo'shilganda yuzaga keladi.

- **Turlari:** in-band (klassik), inferential (blind), out-of-band (javob boshqa kanal orqali, masalan, DNS).
- **Oddiy misol:** kirish maydoniga `' OR 1=1 -- -` yuborilsa, shart doim to'g'ri bo'lib qoladi va parol tekshirilmaydi.
- **Logda izlash:** `UNION`, `SELECT`, `INSERT`, `WHERE`, apostrof `'`, tire `--`, qavslar, `CHR`.
- **Himoya:** parametrli so'rovlar (xom SQL'dan qochish), kiritishni tekshirish, frameworkni yangilab turish.

## Cross-Site Scripting (XSS)
Foydalanuvchi kiritgan ma'lumot javobga tozalanmasdan qo'shilib, brauzerda JavaScript ishlab ketadi.

- **Turlari:** reflected (so'rovda), stored (serverda saqlanadi, eng xavfli), DOM-based.
- **Misol yuklama:** `<script>alert(1)</script>`
- **Logda izlash:** `script`, `alert`, `prompt`, `console.log`, `<`, `>`, `onerror`.
- **Oqibat:** sessiyani o'g'irlash, login ma'lumotlarini olish.
- **Himoya:** chiqishni HTML-kodlash (encoding), framework imkoniyatlari, kiritishni tekshirish.

## Open Redirect
Sayt foydalanuvchi bergan URL'ni tekshirmay, boshqa manzilga yo'naltirganda yuzaga keladi.

- **Misol:** `https://sayt.uz/redirect.php?url=http://zararli.example`. Havola ishonchli saytdan boshlanadi, foydalanuvchi esa zararli saytga tushadi.
- **Logda izlash:** `url=`, `redirect=`, `next=` kabi parametrlarda boshqa domen.
- **Oqibat:** phishing, zararli dastur tarqatish.
- **Himoya:** ruxsat etilgan manzillar ro'yxati (whitelist), foydalanuvchi kiritgan URL'dan to'g'ridan-to'g'ri foydalanmaslik.

Manba: LetsDefend SOC Analyst kursi. Konspekt o'z so'zlarim bilan yozildi.
