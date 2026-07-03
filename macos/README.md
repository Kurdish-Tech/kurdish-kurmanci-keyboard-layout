# ⌨️ Kurmancî Keyboard Layout — macOS

## بالعربية

### الوصف
هذا المجلد يحتوي على تخطيط لوحة المفاتيح الكردية اللاتينية (الكرمانجية) لنظام macOS، المطابق لتخطيط "Kurdish-US" الرسمي على ويندوز. الأحرف الإنجليزية تبقى كما هي، بينما تتم إضافة الحروف الكردية الخاصة (Ç ç, Ê ê, Î î, Ş ş, Û û) عبر مفتاح **Option (⌥)** على نفس مواقع المفاتيح المستخدمة في نسخة ويندوز:

| المفتاح | بدون Option | مع Option | مع Shift + Option |
|---|---|---|---|
| `[` | `[` | `û` | `Û` |
| `]` | `]` | `ş` | `Ş` |
| `\` | `\` | `ç` | `Ç` |
| `;` | `;` | `ê` | `Ê` |
| `'` | `'` | `î` | `Î` |

### التثبيت اليدوي (الطريقة الأسرع)
1. انسخ ملف [`Kurmanci.bundle/Contents/Resources/Kurmanci.keylayout`](Kurmanci.bundle/Contents/Resources/Kurmanci.keylayout) إلى:
   - `~/Library/Keyboard Layouts/` (للمستخدم الحالي فقط، لا حاجة لصلاحيات المدير)، أو
   - `/Library/Keyboard Layouts/` (لكل المستخدمين على الجهاز، يتطلب صلاحيات المدير)
2. سجّل الخروج وأعد الدخول (Log out / Log in) حتى يتعرف macOS على التخطيط الجديد.
3. اذهب إلى **System Settings → Keyboard → Input Sources → Edit… → +** وابحث عن **Kurmancî (Kurdish Latin)** أضفه.

### التثبيت كحزمة (Bundle)
لتضمين اسم وأيقونة مخصصة، استخدم مجلد `Kurmanci.bundle` كاملاً بدلاً من الملف المفرد فقط، وانسخه إلى نفس المسارات أعلاه (`~/Library/Keyboard Layouts/Kurmanci.bundle`).

---

## Bi Kurmancî

### Danasîn
Ev peldank nexşeya klavyeya Kurmancî ya Latînî ji bo macOS-ê vedihewîne, li gorî heman sêwirana nexşeya "Kurdish-US" ya fermî ya Windowsê. Tîpên Îngilîzî bêyî guherîn dimînin; tîpên taybet ên Kurdî (Ç ç, Ê ê, Î î, Ş ş, Û û) bi riya bişkoja **Option (⌥)** têne peyda kirin, li ser heman bişkojên ku di guhertoya Windows de têne bikaranîn (li jorê tabloyê binêre).

### Sazkirin (Rêbaz a Destan)
1. Pelê [`Kurmanci.bundle/Contents/Resources/Kurmanci.keylayout`](Kurmanci.bundle/Contents/Resources/Kurmanci.keylayout) kopî bikin li:
   - `~/Library/Keyboard Layouts/` (tenê ji bo hesabê te, destûra rêveberî ne pêwîst e), an
   - `/Library/Keyboard Layouts/` (ji bo hemû bikarhênerên komputerê, destûra rêveberî pêwîst e)
2. Derkevin û dîsa têkevin hesabê xwe (Log out / Log in) da ku macOS nexşeya nû nas bike.
3. Herin **System Settings → Keyboard → Input Sources → Edit… → +**, lêgerînê bikin **Kurmancî (Kurdish Latin)** û zêde bikin.

---

## Building a distributable installer (.pkg / .dmg)

The `.keylayout` file is plain XML — it does not need compiling. To ship it as a proper installer for less technical users:

### Option A — `.pkg` (recommended)
```bash
# 1. Stage the payload exactly as it should land on disk
mkdir -p pkgroot/Library/Keyboard\ Layouts
cp -R Kurmanci.bundle "pkgroot/Library/Keyboard Layouts/"

# 2. Build the component package
pkgbuild \
  --root pkgroot \
  --identifier tech.kurdish.keyboardlayout.kurmanci \
  --version 1.0.0 \
  --install-location / \
  Kurmanci-component.pkg

# 3. (Optional) Wrap it in a distribution package with a welcome/readme screen
productbuild \
  --distribution distribution.xml \
  --package-path . \
  Kurmanci-Kurdish-Keyboard.pkg
```
After install, tell the user to log out and back in once, then add the layout from **Input Sources**.

### Option B — `.dmg` (simplest, drag-and-drop)
```bash
mkdir dmg-root
cp -R Kurmanci.bundle dmg-root/
hdiutil create -volname "Kurmancî Keyboard" \
  -srcfolder dmg-root \
  -ov -format UDZO \
  Kurmanci-Kurdish-Keyboard.dmg
```
Users mount the `.dmg` and drag `Kurmanci.bundle` into `~/Library/Keyboard Layouts/` themselves.

> Note: Apple does not notarize keyboard-layout bundles as "apps," so unsigned `.pkg`/`.dmg` files will trigger a Gatekeeper warning ("unidentified developer"). For public distribution, sign with a `Developer ID Installer` certificate and notarize via `xcrun notarytool submit`.
