# Linux: ruxsatlar, tarmoq va loglar

Bu konspekt SOC Analyst yo'lida kerak bo'ladigan uchta blokni qamrab oladi: fayl ruxsatlari/jarayonlar, tarmoq/servislar va log fayllar.

## 1. Ruxsatlar va jarayonlar

| Buyruq | Vazifasi |
|--------|----------|
| `chmod` | Faylga kirish huquqini (o'qish/yozish/bajarish) o'zgartiradi |
| `chown` | Faylning egasi/guruhini o'zgartiradi |
| `ps aux` | Hozir ishlayotgan barcha jarayonlarni ko'rsatadi |
| `top` | Jarayonlarni CPU/xotira sarfi bo'yicha real vaqtda ko'rsatadi |
| `kill -9 <PID>` | Berilgan PID'li jarayonni majburan to'xtatadi |

```bash
chmod 755 script.sh      # egasi: hammasi, boshqalar: o'qish+bajarish
chown user:group f.txt   # egasi va guruhini almashtiradi
ps aux | grep nginx      # nginx jarayonini qidirish
top                      # jonli monitoring
kill -9 1234             # 1234-PID'li jarayonni to'xtatish
```

**SOC nuqtai nazaridan:** `777` ruxsatli fayl yoki `/tmp` ichida ishlayotgan noma'lum nomli jarayon — shubha uyg'otadigan belgilar.

## 2. Tarmoq va servislar

| Buyruq | Vazifasi |
|--------|----------|
| `ip a` | Tarmoq interfeyslari va IP manzillarni ko'rsatadi |
| `ss -tulnp` | Ochiq (tinglovchi) portlar va ularni ochgan jarayonlarni ko'rsatadi |
| `curl <url>` | URL'ga HTTP so'rov yuboradi |
| `ssh user@host` | Masofaviy serverga xavfsiz ulanadi |
| `systemctl status <xizmat>` | Xizmat holatini ko'rsatadi |
| `journalctl -u <xizmat> -f` | Xizmatning systemd log'ini jonli kuzatadi |

```bash
ip a
ss -tulnp
systemctl status ssh
journalctl -u ssh -f
```

**SOC nuqtai nazaridan:** `ss -tulnp` natijasida tanish bo'lmagan portga ulangan jarayon — C2 (Command & Control) aloqasi belgisi bo'lishi mumkin.

## 3. Loglar

| Fayl | Mazmuni |
|------|---------|
| `/var/log/syslog` yoki `/var/log/messages` | Umumiy tizim hodisalari |
| `/var/log/auth.log` (Debian/Ubuntu) yoki `/var/log/secure` (RHEL) | Autentifikatsiya hodisalari — SOC uchun eng muhim fayllardan biri |

```bash
tail -f /var/log/auth.log
grep "Failed password" /var/log/auth.log
```

**Auth log'dan odatiy qator ko'rinishi:**

```
Nov  7 09:14:02 server sshd[1234]: Failed password for root from 198.51.100.23 port 51422 ssh2
```

Bu qatordan: **qaysi foydalanuvchi nomi** (`root`) bilan, **qaysi IP manzildan** (`198.51.100.23`) kirish urinishi bo'lgani va u **muvaffaqiyatsiz** (`Failed password`) bo'lgani ko'rinadi.

> **Eslatma:** haqiqiy `auth.log` namunasini tekshirib, shu yerga real misol va tahlilni qo'shish kerak — bu bo'lim hozircha shablon sifatida tayyorlangan.

## Manba

[OverTheWire Bandit](https://overthewire.org/wargames/bandit/) — amaliy mashqlar: [bandit-writeup.md](../05-ctf/bandit-writeup.md)
