# ⌨️ Kurdish Latin (Kurmancî / Kurdish-US) Keyboard Layout

Nekşeya klavyeya Kurmancî ya klasîk û fermî — ji bo Windows, macOS, û Linux.
تخطيط لوحة المفاتيح الكردية اللاتينية (الكرمانجية) الرسمي — لأنظمة ويندوز، ماك، ولينكس.

---

## 📌 Der barê vê Depoyê de / عن هذا المستودع

**Bi Kurmancî:** Ev depo nexşeya klavyeya Kurmancî ya klasîk û fermî (Kurdish-US) pêşkêş dike, niha ji bo sê pergalan jî amade ye: **Windows**, **macOS**, û **Linux**. Armanca me hêsankirina bikaranîna ziman û çanda Kurdî ye di qada dîjîtal de, bi rêya amûrên belaş û çavkanîvekirî.

**بالعربية:** يقدم هذا المستودع تخطيط لوحة المفاتيح الكردية اللاتينية الكلاسيكية والرسمية (Kurdish-US)، وهو الآن متوفر لثلاثة أنظمة تشغيل: **ويندوز**، **ماك (macOS)**، و**لينكس**. نهدف من خلال هذه المبادرة إلى تطويع التكنولوجيا لخدمة اللغة والثقافة الكردية عبر برمجيات مجانية ومفتوحة المصدر للجميع.

## Nexşeya Klavyeyê / تخطيط الأحرف

Ji bilî tîpên latînî yên standard, pênc tîpên taybet ên Kurmancî bi riya bişkoja **AltGr** (Windows / Linux) an **Option ⌥** (macOS) têne peyda kirin, li ser heman cihên bişkojan di her sê pergalan de:

الطباعة اللاتينية العادية تبقى كما هي، وتُضاف الحروف الكردية الخمسة الخاصة عبر مفتاح **AltGr** (ويندوز / لينكس) أو **Option ⌥** (ماك)، على نفس مواقع المفاتيح في الأنظمة الثلاثة:

| Bişkoj / Key | Bêyî guherîn / عادي | + AltGr / Option | + Shift + AltGr / Option |
|---|---|---|---|
| `[` | `[` | `û` | `Û` |
| `]` | `]` | `ş` | `Ş` |
| `\` | `\` | `ç` | `Ç` |
| `;` | `;` | `ê` | `Ê` |
| `'` | `'` | `î` | `Î` |

Werin binêrin [`index.html`](index.html) ji bo nexşeya wênekî ya klavyeyê.
انظر إلى [`index.html`](index.html) للخريطة المرئية الكاملة للوحة المفاتيح.

## 🗂️ Hiyerarşiya Depoyê / هيكلية المستودع


```
.
├── Readme.md              # Vê pelê / هذا الملف
├── index.html             # Rûpela malperê ya nîşandana nexşeyê
├── windows/                # Windows — .msi / setup.exe / .dll (amd64, i386, ia64, wow64)
│   └── README.md
├── macos/                  # macOS — .keylayout / .bundle
│   ├── README.md
│   └── Kurmanci.bundle/Contents/Resources/Kurmanci.keylayout
└── linux/                  # Linux — XKB symbols
    ├── README.md
    └── xkb/
        ├── symbols/ku
        └── rules/evdev.xml.fragment
```

## Sazkirin / التثبيت

### 🪟 Windows
Binêrin [`windows/README.md`](windows/README.md). Bi kurtahî: **[Releases](../../releases)** → `krlat_us.zip` daxînin → `setup.exe` bimeşînin.

انظر [`windows/README.md`](windows/README.md). باختصار: **[Releases](../../releases)** ← حمّل `krlat_us.zip` ← شغّل `setup.exe`.

### 🍎 macOS
Binêrin [`macos/README.md`](macos/README.md) ji bo rêbernameya têkûz (sazkirina destan û çêkirina `.pkg`/`.dmg`). Bi kurtahî: pelê [`macos/Kurmanci.bundle/Contents/Resources/Kurmanci.keylayout`](macos/Kurmanci.bundle/Contents/Resources/Kurmanci.keylayout) bikişînin `~/Library/Keyboard Layouts/` û careke din têkevin hesabê xwe.

انظر [`macos/README.md`](macos/README.md) للدليل الكامل (التثبيت اليدوي وبناء حزمة `.pkg`/`.dmg`). باختصار: انسخ [`macos/Kurmanci.bundle/Contents/Resources/Kurmanci.keylayout`](macos/Kurmanci.bundle/Contents/Resources/Kurmanci.keylayout) إلى `~/Library/Keyboard Layouts/` ثم سجّل الخروج وأعد الدخول.

### 🐧 Linux
Binêrin [`linux/README.md`](linux/README.md) ji bo rêbernameya têkûz (sazkirina XKB û çêkirina pakêtên `.deb`/`.rpm`). Bi kurtahî:
```bash
sudo cp linux/xkb/symbols/ku /usr/share/X11/xkb/symbols/kumr
setxkbmap -layout kumr -variant basic
```

انظر [`linux/README.md`](linux/README.md) للدليل الكامل (تثبيت XKB وبناء حزم `.deb`/`.rpm`). باختصار:
```bash
sudo cp linux/xkb/symbols/ku /usr/share/X11/xkb/symbols/kumr
setxkbmap -layout kumr -variant basic
```

---

## Beşdarî / المساهمة

Pêşniyar û çewtiyên xwe di beşa [Issues](../../issues) de parve bikin.
شارك اقتراحاتك أو أي ملاحظات عبر قسم [Issues](../../issues).

## Lîsans / الترخيص

Ev proje vekirî ye û ji bo mirovahiya Kurd tê pêşkêşkirin.
هذا المشروع مفتوح المصدر ومُقدَّم لخدمة المجتمع الكردي.
