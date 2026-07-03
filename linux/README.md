# ⌨️ Kurmancî Keyboard Layout — Linux (XKB)

## بالعربية

### الوصف
هذا المجلد يحتوي على ملف XKB لتخطيط الكيبورد الكردي اللاتيني (الكرمانجية)، المطابق لتخطيط "Kurdish-US" الرسمي على ويندوز. الطباعة الإنجليزية العادية لا تتأثر؛ الحروف الكردية الخاصة (Ç ç, Ê ê, Î î, Ş ş, Û û) تُضاف عبر مفتاح **AltGr** على نفس مواقع مفاتيح نسخة ويندوز: `[ ] \ ; '`.

### ⚠️ تنبيه مهم قبل التثبيت
معظم توزيعات لينكس تأتي مسبقاً بملف `ku` ضمن حزمة `xkeyboard-config` (مخصص للكردية السورانية بالحروف العربية). **لا تستبدل هذا الملف مباشرة**، وإلا فقد تفقد ذلك التخطيط. اختر إحدى الطريقتين:

- **الطريقة الآمنة (موصى بها):** ثبّت الملف تحت اسم مختلف، مثلاً `kumr`، ثم استخدمه عبر `setxkbmap -layout kumr`.
- **الدمج:** أضف `xkb_symbols "kurmanci"` الموجود داخل [`xkb/symbols/ku`](xkb/symbols/ku) كنسخة إضافية (variant) داخل ملف `ku` الموجود أصلاً على نظامك، بدلاً من استبداله بالكامل.

### التثبيت اليدوي (تجربة سريعة بدون صلاحيات جذر)
```bash
# نسخ الملف باسم آمن غير متعارض
sudo cp linux/xkb/symbols/ku /usr/share/X11/xkb/symbols/kumr

# تفعيله مباشرة في الجلسة الحالية للتجربة
setxkbmap -layout kumr -variant basic
```

### التثبيت الدائم (مع ظهوره في إعدادات النظام)
1. انسخ الملف كما في الأعلى إلى `/usr/share/X11/xkb/symbols/kumr`.
2. ادمج محتوى [`xkb/rules/evdev.xml.fragment`](xkb/rules/evdev.xml.fragment) داخل `/usr/share/X11/xkb/rules/evdev.xml` (بدّل `ku` بـ `kumr` في الاسم إن اخترت الاسم الآمن)، وأضف نفس الإدخال داخل `evdev.lst` بصيغته المبسطة.
3. أعد تشغيل الجلسة، ثم أضف التخطيط من إعدادات لوحة المفاتيح في نظامك (GNOME Settings / KDE System Settings).

---

## Bi Kurmancî

### Danasîn
Ev peldank pelê XKB yê nexşeya klavyeya Kurmancî ya Latînî vedihewîne, li gorî heman sêwirana nexşeya "Kurdish-US" ya fermî ya Windowsê. Nivîsandina Îngilîzî bêyî guherîn dimîne; tîpên taybet ên Kurdî (Ç ç, Ê ê, Î î, Ş ş, Û û) bi riya bişkoja **AltGr** têne peyda kirin, li ser heman bişkojan: `[ ] \ ; '`.

### ⚠️ Hişyarî berî sazkirinê
Gelek dabeşên Linuxê jixwe pelekî bi navê `ku` di pakêta `xkeyboard-config`-ê de tînin (ji bo Kurdiya Soranî ya bi tîpên Erebî). **Vî pelî rasterast neguherînin**, wekî din dibe ku hûn wê nexşeyê winda bikin. Yek ji van du rêbazan bikar bînin:

- **Rêbaza ewle (pêşniyar):** Pelî bi navekî cuda saz bikin, wek mînak `kumr`.
- **Yekkirin:** `xkb_symbols "kurmanci"` ya di [`xkb/symbols/ku`](xkb/symbols/ku) de wek variantek zêde têkevin nav pelê `ku` yê heyî li ser pergala we.

### Sazkirina Destan
```bash
sudo cp linux/xkb/symbols/ku /usr/share/X11/xkb/symbols/kumr
setxkbmap -layout kumr -variant basic
```

---

## Packaging into `.deb` and `.rpm` installers

### `.deb` (Debian / Ubuntu)
```
kurmanci-kbd/
├── DEBIAN/
│   ├── control
│   └── postinst
└── usr/share/X11/xkb/symbols/
    └── kumr                 # copy of linux/xkb/symbols/ku
```

`DEBIAN/control`:
```
Package: kurmanci-kbd
Version: 1.0.0
Section: x11
Priority: optional
Architecture: all
Maintainer: Kurdish Tech Organization <noreply@kurdish-tech.github.io>
Description: Kurmancî (Kurdish Latin) XKB keyboard layout
 Adds the official "Kurdish-US" Latin keyboard layout as an XKB symbols
 file, matching the Windows krlat_us layout key-for-key.
```

`DEBIAN/postinst` (registers the layout in the input-source picker):
```bash
#!/bin/sh
set -e
XML=/usr/share/X11/xkb/rules/evdev.xml
if [ -f "$XML" ] && ! grep -q '<name>kumr</name>' "$XML"; then
    # Merge linux/xkb/rules/evdev.xml.fragment here (see README for the
    # exact <layout>/<variant> block), e.g. via xmlstarlet or a small
    # Python/sed script run at package-build time rather than at runtime.
    :
fi
exit 0
```

Build it:
```bash
chmod 755 kurmanci-kbd/DEBIAN/postinst
dpkg-deb --build --root-owner-group kurmanci-kbd
sudo dpkg -i kurmanci-kbd.deb
```

### `.rpm` (Fedora / RHEL / openSUSE)
`kurmanci-kbd.spec`:
```spec
Name:           kurmanci-kbd
Version:        1.0.0
Release:        1%{?dist}
Summary:        Kurmancî (Kurdish Latin) XKB keyboard layout
License:        MIT
BuildArch:      noarch

%description
Adds the official "Kurdish-US" Latin keyboard layout as an XKB symbols
file, matching the Windows krlat_us layout key-for-key.

%install
mkdir -p %{buildroot}/usr/share/X11/xkb/symbols
install -m 644 %{_sourcedir}/ku %{buildroot}/usr/share/X11/xkb/symbols/kumr

%files
/usr/share/X11/xkb/symbols/kumr
```

Build it:
```bash
rpmbuild -bb kurmanci-kbd.spec
sudo rpm -i ~/rpmbuild/RPMS/noarch/kurmanci-kbd-1.0.0-1.*.rpm
```

> Both packages intentionally only install the symbols file under the safe
> `kumr` name. Wiring it into `evdev.xml`/`evdev.lst` automatically at
> install time is distro-specific and risks corrupting a system file if
> done naively — do that merge as part of your package build/CI step and
> test on the target distro before shipping.
