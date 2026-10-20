# Cyber Kill Chain

Kiberhujum odatda 7 bosqichdan o'tadi (Lockheed Martin modeli). SOC tahlilchisi uchun muhimi: har bosqichda hujumchi qanday iz qoldiradi va biz uni qayerdan ko'ramiz.

| # | Bosqich | Hujumchi nima qiladi | SOC nimani ko'radi yoki qiladi |
|---|---|---|---|
| 1 | Razvedka (Reconnaissance) | Ochiq manbalardan xodimlar, email manzillari va texnologiyalar haqida ma'lumot yig'adi | Veb-saytga g'alati skanerlash, ko'p DNS so'rovlari. Himoya: pentest bilan zaif joylarni oldindan topish |
| 2 | Qurollantirish (Weaponization) | Yig'ilgan ma'lumot asosida vosita tayyorlaydi: makroli hujjat, phishing xat, zararli APK | Odatda to'g'ridan-to'g'ri ko'rinmaydi, threat intelligence orqali bilib olinadi |
| 3 | Yetkazib berish (Delivery) | Vositani nishonga yetkazadi: email, havola, serverga yuklangan zararli fayl | Email himoyasi alertlari, shubhali URL, xodimlarning phishing haqidagi xabarlari |
| 4 | Ekspluatatsiya (Exploitation) | Zararli kod ishga tushadi (masalan, makro) | Word'dan PowerShell yoki cmd ishga tushishi (process tree), EDR alerti |
| 5 | O'rnatish (Installation) | Qurilmada backdoor qoldirib, keyin ham kira olishni ta'minlaydi | Yangi servis (Event ID 7045), yangi rejalashtirilgan vazifa (4698), yangi foydalanuvchi (4720) |
| 6 | Buyruq va boshqaruv (C2) | Zararlangan qurilma va hujumchi serveri o'rtasida aloqa o'rnatiladi | Noma'lum tashqi IP yoki domenga muntazam ulanishlar, g'alati DNS |
| 7 | Maqsadli harakatlar (Actions on Objectives) | Fayllarni o'chiradi yoki shifrlaydi (to'lov talab qiladi), ma'lumot o'g'irlaydi | Ommaviy fayl o'zgarishi, katta hajmli chiquvchi trafik |

**Asosiy xulosa:** 7-bosqichga yetganda himoya qilish kech bo'ladi. Shuning uchun SOC vazifasi hujumni imkon qadar erta (3–5-bosqichlarda) topib to'xtatish yoki zararni kamaytirishdir.

## Topshiriq: telekommunikatsiya tashkilotiga APT hujumi

Stsenariyni bosqichlarga o'zim shunday joyladim (LetsDefend javobi bilan solishtirib chiqing):

| Stsenariydagi qadam | Bosqich |
|---|---|
| Xodimlarning emaillari ijtimoiy tarmoq va ochiq manbalardan yig'ildi | Razvedka |
| Phishing xat shabloni va makroli `Salaries.docx` yaratildi | Qurollantirish |
| Xat belgilangan sanada xodimlarga yuborildi | Yetkazib berish |
| Xodim hujjatni yuklab olib ochdi, makro ishga tushdi | Ekspluatatsiya |
| Makrodagi PowerShell orqali to'lov dasturi o'rnatildi | O'rnatish |
| To'lov dasturi ishga tushdi | Maqsadli harakatlar |
| (C2 aloqasi stsenariyda ko'rsatilmagan) | C2 |

Manba: LetsDefend SOC Analyst kursi. Konspekt o'z so'zlarim bilan yozildi.
