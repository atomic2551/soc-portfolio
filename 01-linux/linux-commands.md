# Linux: asosiy buyruqlar bilan ishlash

Linuxda eng muhim qismlardan biri — terminalda buyruqlar bilan ishlash.

## Navigatsiya va fayllarni ko'rish

| Buyruq | Vazifasi |
|--------|----------|
| `pwd` | Hozirgi joylashuvni (joriy papka yo'lini) ko'rsatadi |
| `ls` | Papka ichidagi fayl va papkalarni ko'rsatadi |
| `ls -a` | Yashirin fayllarni ham ko'rsatadi (yashirin fayllar nomi `.` bilan boshlanadi, masalan `.bashrc`) |
| `ls -l` | Batafsil ro'yxat: huquqlar, egasi, hajmi, sanasi |
| `ls -la` | `-l` va `-a` birgalikda: batafsil ro'yxat + yashirin fayllar |
| `cat fayl` | Faylning tarkibini o'qib, ekranga chiqaradi |

Misol:

```bash
pwd
ls -la
cat notes.txt
```

## find — fayl qidirish

Sintaksisi:

```bash
find <qayerdan> <shart>
```

### Hajm bo'yicha qidirish (`-size`)

```bash
find / -size 1021c
```

Bu buyruq `/` ichidan aynan **1021 bayt** hajmli faylni topadi.

Hajm birliklari (bu Kali'da emas, barcha Linux tizimlarida bir xil):

| Belgi | Ma'nosi |
|-------|---------|
| `c` | bayt |
| `k` | kilobayt |
| `M` | megabayt |
| `G` | gigabayt |

Qo'shimcha: `+` dan katta, `-` dan kichik ma'nosini beradi.

```bash
find / -size +10M     # 10 MB dan katta fayllar
find / -size -5k      # 5 KB dan kichik fayllar
```

### Nom bo'yicha qidirish

```bash
find / -name "passwd"       # aniq nom
find / -name "*.txt"        # nomining bir qismi / kengaytma bo'yicha
find / -iname "flag*"       # katta-kichik harfni farqlamaydi
```

### Boshqa mezonlar

```bash
find / -type f              # faqat fayllar (d — papkalar)
find / -mtime -1            # oxirgi 1 kunda o'zgartirilgan
find / -user root           # egasi root bo'lgan
find / -perm -4000          # SUID fayllar (cyber security uchun muhim)
```

### Maslahat

`/` dan qidirganda "Permission denied" xatolari ko'p chiqadi. Ularni yashirish uchun:

```bash
find / -name "flag.txt" 2>/dev/null
```
