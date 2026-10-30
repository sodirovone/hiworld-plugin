# hiworld — Claude Code plagini

G'oyadan hujjatlargacha bo'lgan yo'lni avtomatlashtiradigan plagin.
**hiworld.club** uchun. Butun muloqot lotin o'zbek tilida.

```
aniqla   ->  tergov    ->  prdla     ->  kengash     + kotib
g'oyani      savolga        hujjatlar    7 ekspert     har commitda
aniqlash     tutish         paketi       Go/No-Go      hisobot yozadi
```

---

## O'rnatish (2 qadam)

Claude Code ichida quyidagi ikki buyruqni yozing:

```
/plugin marketplace add sodirovone/hiworld-plugin
```

```
/plugin install hiworld@hiworld
```

Tekshirish: `/plugin` deb yozing — ro'yxatda `hiworld` ko'rinadi.
Yoki `/` bosing — `aniqla`, `tergov`, `prdla`, `kengash` ro'yxatda chiqadi.

**Yangilash.** Odatda hech narsa qilish shart emas: Claude Code katalogni sessiya
boshlanganda fon rejimida yangilaydi va yangi versiyani o'zi tortib oladi.

Darhol kerak bo'lsa qo'lda majburlang:

```
/plugin marketplace update hiworld
/plugin update hiworld@hiworld
/reload-plugins
```

Yangilanish loyiha fayllaringizga (PRD, sprints, kod) **tegmaydi** — faqat plagin
skill'lari almashadi.

---

## Nima qiladi

### 1. `aniqla` — g'oyani aniqlash

Xomaki, tumanli g'oyani bitta jumlada aytiladigan g'oyaga keltiradi.

- 2-4 ta aniqlashtiruvchi savol beradi (bittalab, tayyor variantlar bilan)
- G'oya juda keng bo'lsa — toraytiradi, qolganini "kelajak" ro'yxatiga yozadi
- Natija: `[KIM]` uchun `[MUAMMO]`ni hal qiladigan `[YECHIM]` — bitta jumla

```
/aniqla
```

yoki shunchaki: `g'oyamni aniqlab ber: odamlar mashinasini ijaraga bermoqchi...`

### 2. `tergov` — savolga tutish

Aniqlangan g'oyani 5 blok bo'yicha chuqur savolga tutadi.

| Blok | Mavzu |
|------|-------|
| 1/5 | Mahsulot mohiyati |
| 2/5 | Foydalanuvchilar va rollar |
| 3/5 | Asosiy oqim |
| 4/5 | Pul va qoidalar |
| 5/5 | Chegaralar va xavflar |

- Jami 25-30 savol, blokma-blok (hech qachon hammasi birato'la emas)
- Har savolda tayyor variantlar + "o'zim yozaman" + **"bilmayman — keyin hal qilamiz"**
- "Bilmayman" jarimasiz: u **ochiq savol** bo'lib PRD'ga tushadi
- Xulosa `.hiworld/tergov.md`'ga saqlanadi (sessiya uzilsa yo'qolmasligi uchun)

```
/tergov
```

### 3. `prdla` — hujjatlar paketi

Tergov javoblaridan to'liq hujjatlar paketini yozadi:

```
PRD.md          g'oya, rollar, oqim, funksiyalar, ochiq savollar
STACK.md        qotirilgan reference stack + API-first qarori
ROADMAP.md      S1..S6 magistral + tarmoqlar + kelajak
DECISIONS.md    qarorlar jurnali (sana - qaror - sabab)
sprints/        SPRINT-1..6 + SPRINT-SHABLON (7 fayl)
```

Sprint tasklari **sizning loyihangizga konkret** yoziladi — umumiy shablon emas.

```
/prdla
```

### 4. `kengash` — ekspertlar paneli va Go/No-Go

PRD'ni 7 nafar ekspert og'ir savollarga tutadi va loyihani sindirishga harakat qiladi.

| Ekspert | Nimani bosadi |
|---|---|
| 🔍 Bozor tahlilchisi | Bozor bormi, kim urinib ko'rgan va nega o'lgan |
| 💰 VC tanqidchi | Bitta bitim iqtisodiyoti, nega bu biznes |
| 😈 Advokat dyavola | Har javobga qarshi argument |
| 📣 O'sish marketologi | Birinchi 100 foydalanuvchi qayerdan |
| ⚙️ Operatsion direktor | 10 barobar o'ssa nima birinchi bo'lib sinadi |
| ⚖️ Yurist-riskchi | Kim javobgar, shartnoma, maxfiylik |
| 🎭 Mehmon ekspert | Domenga qarab almashadi (firibgarlik, UX, CTO, regulyator...) |

- 2 raund, 6-8 og'ir savol. Javob bo'lmasa — jarima yo'q, ochiq xavf sifatida yoziladi
- Yaxshi javob e'tirozni yopadi va `DECISIONS.md`ga qaror bo'lib tushadi
- Oxirida **yumaloq stol** vizualizatsiyasi: kim nima dedi, kim qanday ovoz berdi
- Qaror arifmetika bilan: **GO** · **SHARTLI GO** (shartlar bilan) · **NO-GO** (2 ta pivot taklifi bilan)
- Natija `KENGASH.md`ga yoziladi

```
/kengash
```

```
─────────── OVOZ BERISH ───────────

 🔍 Bozor tahlilchisi   ⚠️  SHARTLI
 💰 VC tanqidchi        ❌  NO-GO
 😈 Advokat dyavola     ✅  GO
 ...
  ▰▰▰▰▰▱▱  GO 3 · SHARTLI 2 · NO-GO 2

  QAROR:  SHARTLI GO
```

### 5. `kotib` — hisobot agenti

Har commitdan oldin avtomatik ishga tushadi va:

1. Joriy SPRINT faylida bajarilgan tasklarni belgilaydi
2. **Hisobot** bo'limiga 1-2 qator yozadi
3. **Handoff**ni yangilaydi — keyingi sessiya nimadan boshlanadi
4. Sessiyada qaror bo'lgan bo'lsa — `DECISIONS.md`'ga yozadi
5. Sprint yakunlansa — `ROADMAP.md`'da belgilaydi
6. O'zbekcha, mazmunli commit xabarini taklif qiladi

**Uxlash rejimi:** loyihada `sprints/` papkasi paydo bo'lmaguncha kotib
umuman aralashmaydi. Ya'ni plaginni bugun o'rnatsangiz ham, u S1 boshlanganda
o'zi uyg'onadi.

---

## Zanjir

Skill'lar ketma-ket ishlashga mo'ljallangan:

```
aniqla -> tergov -> prdla -> kengash
```

Lekin har biri mustaqil ham chaqiriladi. Kontekstda oldingi bosqich natijasi bo'lmasa,
skill sizni to'g'ri joyga yo'naltiradi (`prdla` avval `tergov`ni so'raydi, `kengash`
esa `PRD.md` yo'q bo'lsa `prdla`ga yuboradi).

---

## Talablar

- Claude Code (istalgan yangi versiya)
- `kotib` avtomatik ishga tushishi uchun — **Node.js** (Claude Code'ni npm orqali
  o'rnatgan bo'lsangiz allaqachon bor). Node bo'lmasa qolgani ishlaydi, faqat commit
  qorovuli ishlamaydi — kotibni qo'lda chaqirasiz.

---

## Muammo bo'lsa

| Muammo | Yechim |
|--------|--------|
| Skill ro'yxatda yo'q | Claude Code'ni qayta ishga tushiring yoki `/reload-plugins` |
| `/plugin install` topmayapti | Avval `/plugin marketplace add sodirovone/hiworld-plugin` |
| Commit to'xtab qolyapti | Kotib agentni ishga tushiring, yoki `.hiworld/kotib-ok` faylini qo'lda yarating |
| Yangi versiya kelmayapti | `/plugin marketplace update hiworld`, keyin `/plugin update hiworld@hiworld` |

---

## Mualliflik

[vibecodinguz](https://github.com/iakadirov/vibecodinguz) (vibecoding.uz, MIT) asosida
qilingan. Batafsil: [CHANGELOG.md](CHANGELOG.md).

## Litsenziya

MIT — [LICENSE](LICENSE)

---

*hiworld plagini · hiworld.club*
