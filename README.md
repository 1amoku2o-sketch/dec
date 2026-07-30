# مشروع كشوف درجات البكالوريا

## موقع المشروع

```
https://releveeducationgovmrcandidat.dpdns.org/?id=رقم_الملف
```

- **النطاق:** `releveeducationgovmrcandidat.dpdns.org` (مجاني من DigitalPlat)
- **GitHub:** `https://github.com/1amoku2o-sketch/dec`
- **الاستضافة:** GitHub Pages + Cloudflare (DNS + Proxy)

---

## هيكل الملفات

```
dec/
├── index.html       # الصفحة الوحيدة (كل شيء فيها)
├── logo.png         # شعار موريتانيا (مربع أبيض)
└── README.md
```

---

## البيانات (candidates)

### مكانها في الملف

في `index.html` داخل الوسم `<script>`، السطر 83:

```javascript
const candidates = {
  "رقم_الملف": {
    nni:        "رقم NNI"
    dossier:    "رقم الملف",
    serie:      "اسم الشعبة (مثال: Mathématiques)",
    decision:   "القرار (مثال: Admis)",
    centreAr:   "اسم المركز بالعربية",
    centreFr:   "اسم المركز بالفرنسية",
    nomAr:      "اسم المترشح بالعربية",
    nomFr:      "اسم المترشح بالفرنسية",
    lieuAr:     "مكان الولادة بالعربية",
    lieuFr:     "مكان الولادة بالفرنسية",
    dateNais:   "تاريخ الميلاد (مثال: 21/12/2006)",
    moy:        "المعدل العام (مثال: 14.5128125)",
    anonyme:    "رقم ANONYME",
    etcc:       "رمز ETCC (مثال: MT09)"
  }
}
```

### إضافة مترشح جديد

أضف عنصرًا جديدًا داخل `candidates` بنفس تنسيق العناصر الموجودة.
**تحذير:** بعد كل فاصلة `,` ما عدا آخر عنصر.

### مثال حقيقي من الملف (00309)

```javascript
"00309": {
  nni: "3898414384",
  dossier: "00309",
  serie: "Mathématiques",
  decision: "Admis",
  centreAr: "ثانوية التميز 3",
  centreFr: "Lycée Excellence 3",
  nomAr: "عبدالله محمد عبدالرحمن الدين",
  nomFr: "Abdallahi Mohamed Abderahmane Dine",
  lieuAr: "تيارت",
  lieuFr: "Teyaret",
  dateNais: "21/12/2006",
  moy: "14.5128125",
  anonyme: "3898414384",
  etcc: "MT09"
}
```

---

## الترجمة (translations)

### مكانها في الملف

السطر 120.

```javascript
const translations = {
  fr: {
    navTitle:     "Relevés des notes du BAC",      // عنوان المتصفح
    home:         "Accueil",                         // رابط الرئيسية
    langSwitch:   "العربية",                         // نص زر التبديل
    title:        "Candidat",                        // عنوان البطاقة
    nni:          "Numéro National d'Identification (NNI)",
    dossier:      "N° Dossier",
    serie:        "Serie",
    decision:     "Décision",
    centreAr:     "Centre en Arabe",
    centreFr:     "Centre en Français",
    nomAr:        "Nom en Arabe",
    nomFr:        "Nom",
    moy:          "Moy Générale",
    anonyme:      "No ANONYME",
    etcc:         "No ETCC",
    lieuAr:       "Lieu Naissance en Arabe",
    lieuFr:       "Lieu Naissance",
    dateNais:     "Dat Naissance",
    btnText:      "Retour",
    notFound:     "Aucun candidat trouvé pour ce numéro."
  },
  ar: {
    navTitle:     "كشوف درجات البكالوريا",
    home:         "الصفحة الرئيسية",
    langSwitch:   "Français",
    title:        "المترشح",
    nni:          "الرقم الوطني للتعريف",
    dossier:      "رقم الترشح",
    serie:        "الشعبة",
    decision:     "القرار",
    centreAr:     "Centre en Arabe",
    centreFr:     "Centre en Français",
    nomAr:        "Nom en Arabe",
    nomFr:        "الإسم",
    moy:          "المعدل العام",
    anonyme:      "No ANONYME",
    etcc:         "No ETCC",
    lieuAr:       "Lieu Naissance en Arabe",
    lieuFr:       "Lieu Naissance",
    dateNais:     "Dat Naissance",
    btnText:      "رجوع",
    notFound:     "لم يتم العثور على مترشح بهذا الرقم."
  }
};
```

**ملاحظة:** بعض التسميات بالعربية فيها إنجليزية (`"Centre en Arabe"`, `"No ANONYME"`...) لأن الموقع الحكومي الأصلي هكذا.

---

## دالة render

في السطر 167. تستقبل كائن المرشح `c` وتولّد HTML ديناميكيًا باستخدام `innerHTML`.

الحقول المعروضة (بالترتيب):
1. nni
2. dossier
3. serie
4. decision
5. centreAr
6. centreFr
7. nomAr
8. nomFr
9. moy
10. anonyme
11. etcc
12. lieuAr
13. lieuFr
14. dateNais

يجب تحديث `render()` إذا أضفت حقلًا جديدًا إلى `candidates`.

---

## شريط التنقل (Navbar)

```
<nav data-cy="navbar" class="navbar navbar-dark navbar-expand-md bg-dark">
```

- الخلفية: `bg-dark` (أسود)
- الشعار: `<span class="logo-img"></span>` (فارغ، يتم تعبئته بالصورة عبر CSS)
- زر القائمة: `<a class="navbar-toggler d-lg-none">` يظهر فقط في الشاشات الصغيرة
- لون Bootstrap: `navbar-dark`

---

## CSS ملاحظة

- تنسيق `.jh-entity-details` يستخدم `display: grid` بعمودين
- في LTR (`dir="ltr"`): التسميات (`dt`) محاذاة لليسار
- في RTL (`dir="rtl"`): التسميات (`dt`) محاذاة لليمين
- في الجوال: العنوان يقل حجمه (`font-size: 0.85rem`) واللوقو يصغر (`38px`)

---

## الروابط

| الرابط | ماذا يحدث |
|--------|-----------|
| `releveeducationgovmrcandidat.dpdns.org` | redirect → `releve.education.gov.mr/` |
| `releveeducationgovmrcandidat.dpdns.org/?id=00309` | يعرض بيانات 00309 |
| `releveeducationgovmrcandidat.dpdns.org/?id=52477` | يعرض بيانات 52477 |
| `releveeducationgovmrcandidat.dpdns.org/?id=99999` | يعرض "غير موجود" |

---

## رفع التعديلات إلى GitHub

```powershell
git add -A
git commit -m "وصف التعديل"
git push
```

**بعد الرفع:** امسح Cloudflare cache يدويًا:
- https://dash.cloudflare.com/ → اختر النطاق → Caching → Purge Everything

---

## النشر الأولي (للتذكير فقط)

1. سجّل النطاق في https://dash.domain.digitalplat.org/
2. Nameservers: `paityn.ns.cloudflare.com` + `sage.ns.cloudflare.com`
3. GitHub Pages مفعّل على `master` branch
4. Cloudflare: A records ← 185.199.108.153 + 109 + 110 + 111 (Proxy ON)
5. Cloudflare: Page Rule ← `releveeducationgovmrcandidat.dpdns.org/` redirect 302 → `https://releve.education.gov.mr/`
