# OverTheWire: Bandit — Level 0 → 15

[Bandit](https://overthewire.org/wargames/bandit/) — Linux buyruqlari, fayl tizimi va SSH asoslarini amaliyotda mustahkamlash uchun bepul, qonuniy wargame. Har bir daraja oldingi darajaning parolini topish orqali ochiladi.

Bu yerda **parollarning o'zi emas**, balki **har bir darajani qanday yechganim (metodologiya)** keltirilgan — bu portfolio sifatida ko'proq qiymatga ega.

Ulanish: `ssh banditN@bandit.labs.overthewire.org -p 2220`

| Daraja | Vazifa | Yechim g'oyasi |
|--------|--------|-----------------|
| 0→1 | `readme` faylini o'qish | `cat readme` |
| 1→2 | Fayl nomi `-` | `cat ./-` (to'liq yo'l bilan murojaat) |
| 2→3 | Fayl nomida bo'sh joy | `cat "fayl nomi"` yoki `cat fayl\ nomi` |
| 3→4 | Yashirin fayl | `ls -a` — nuqta bilan boshlanuvchi fayllarni ko'rsatadi |
| 4→5 | 10 fayldan faqat bittasi matn | `file ./-file*` — turini aniqlab, `ASCII text`ni topish |
| 5→6 | Aniq hajm (1033 bayt) + bajariluvchi emas | `find . -type f -size 1033c ! -executable` |
| 6→7 | Butun tizimda, egasi/guruh bo'yicha | `find / -user X -group Y -size Nc 2>/dev/null` |
| 7→8 | Katta faylda kalit so'z | `grep "so'z" data.txt` |
| 8→9 | Faqat bir marta uchraydigan qator | `sort data.txt \| uniq -u` |
| 9→10 | Binary ichidan matn ajratish | `strings data.txt \| grep '='` |
| 10→11 | Base64 | `base64 -d data.txt` |
| 11→12 | ROT13 | `tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt` |
| 12→13 | Ko'p marta siqilgan (hex→gzip→bzip2→tar→...) | `xxd -r`, so'ng `file` bilan har safar turini aniqlab, mos arxiv vositasi bilan ochish (qatlamma-qatlam) |
| 13→14 | SSH private key bilan boshqa foydalanuvchiga kirish | `ssh -i sshkey.private bandit14@<host>` |
| 14→15 | Portga parolni yuborib, javobda yangi parolni olish | `echo "$PASS" \| nc localhost 30000` |

## Qiziq uchragan muammo — Level 13→14

**Muammo:** `ssh -i sshkey.private bandit14@localhost` buyrug'i klassik yechim bo'lsa-da, server tomonidan **"Connecting from/to localhost is blocked to conserve resources"** xabari bilan rad etildi — hatto `127.0.0.1` va turli `known_hosts` sozlamalari bilan sinalganda ham.

**Sabab:** `ssh -v` (verbose) rejimida log'larni ko'rganimda, autentifikatsiya boshlanmasdan turib serverning o'zi ulanishni rad etayotgani aniqlandi — bu OverTheWire infratuzilmasidagi real cheklov ekan.

**Yechim:** Server xabarining o'zi yo'l ko'rsatdi — "directly from your client machine". `sshkey.private` faylini `scp` orqali **o'z kompyuterimga** ko'chirib, undan **to'g'ridan-to'g'ri** (bandit13 ichidan emas) bandit14'ga ulandim:

```bash
scp -P 2220 bandit13@bandit.labs.overthewire.org:~/sshkey.private .
ssh -i sshkey.private -p 2220 bandit14@bandit.labs.overthewire.org
```

Windows'da bu safar yana bir to'siq chiqdi: **"UNPROTECTED PRIVATE KEY FILE"** — kalit fayli ruxsatlari juda ochiq edi. Buni `icacls` bilan faqat joriy foydalanuvchiga cheklab, muammo hal bo'ldi:

```powershell
icacls sshkey.private /inheritance:r
icacls sshkey.private /grant:r "$($env:USERNAME):(R)"
```

**Xulosa:** xato xabarini diqqat bilan o'qish va server o'zi bergan maslahatga amal qilish — muammoni "to'g'ridan-to'g'ri" yechishdan ko'ra tezroq yo'l bo'ldi.
