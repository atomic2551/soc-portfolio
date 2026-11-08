# Tarmoq kriminalistikasi (Network Forensics) — o'rganish rejasi

IIV'dagi suhbatda tavsiya etilgan yo'nalish: real tarmoq trafigini Wireshark orqali tahlil qilish — HTTP/HTTPS, DNS so'rovlarini kuzatish va shubhali faoliyatni aniqlash.

## Nega muhim

SOC/tergov ishida ko'p hollarda "nima bo'ldi" degan savolga javob — tarmoq trafigida yashiringan bo'ladi: qaysi domenga ulanildi, qanday ma'lumot yuborildi, hujum qaysi protokol orqali amalga oshirildi. Wireshark — bu ma'lumotni ko'rish uchun standart vosita.

## Amaliyot manbalari

- [TryHackMe — Wireshark: The Basics](https://tryhackme.com/room/wiresharkthebasics) — interfeys, filtrlar, asosiy navigatsiya
- [TryHackMe — Wireshark: Packet Operations](https://tryhackme.com/room/wireshark) — paketlarni qo'lga olish va saqlash
- [TryHackMe — Wireshark: Traffic Analysis](https://tryhackme.com/room/wiresharktrafficanalysis) — real hujum trafigini tahlil qilish
- [Malware-Traffic-Analysis.net](https://www.malware-traffic-analysis.net/) — haqiqiy zararli dastur trafigi namunalari (`.pcap`), mustaqil mashq uchun

## Boshlang'ich filtrlar (eslatma sifatida)

```
http.request                      # barcha HTTP so'rovlari
dns                                # barcha DNS so'rovlari
ip.addr == 192.168.1.10            # aniq IP bilan bog'liq trafik
tcp.port == 4444                   # shubhali/noodatiy port
http.request.method == "POST"      # ma'lumot yuborilayotgan so'rovlar
```

## SOC/tergov nuqtai nazaridan diqqat qilinadigan belgilar

- Noodatiy portga (masalan 4444, 1337) ketma-ket ulanishlar — C2 (Command & Control) belgisi
- Ko'p sonli DNS so'rovlari tasodifiy nomlar bilan — DGA (Domain Generation Algorithm) yoki tunnel orqali ma'lumot sizib chiqishi
- Shifrlanmagan HTTP orqali parol/login yuborilishi — xavfsizlik kamchiligi

## Holat

- [ ] Wireshark: The Basics — bajarilmagan
- [ ] Wireshark: Packet Operations — bajarilmagan
- [ ] Wireshark: Traffic Analysis — bajarilmagan
- [ ] Malware-Traffic-Analysis.net'dan 1 ta real namunani mustaqil tahlil qilish — bajarilmagan

> Har bir xona tugatilgach, shu faylga topilgan natija va 3-4 jumlali o'z so'zim bilan xulosa qo'shiladi (portfolio sifatida).
