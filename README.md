# مشروع كشوف درجات البكالوريا

## 📁 بنية المشروع

```
dec/
├── index.html       # الصفحة الرئيسية (كل شيء في ملف واحد)
├── logo.png         # شعار الجمهورية
└── README.md        # هذا الملف
```

المشروع عبارة عن **صفحة HTML واحدة** تحتوي كل شيء: HTML + CSS + JavaScript.
البيانات مخزنة في كائن `candidates` داخل JavaScript.

---

## ➕ إضافة مترشح جديد

افتح `index.html` وابحث عن:

```javascript
const candidates = {
  "رقم_الملف": { ... },
  "52477": { ... }
};
```

أضف عنصرًا جديدًا بنفس التنسيق:

```javascript
"رقم_الملف": {
  nni: "رقم_NNI",
  dossier: "رقم_الملف",
  serie: "الشعبة",
  decision: "القرار",
  centreAr: "اسم المركز بالعربية",
  centreFr: "اسم المركز بالفرنسية",
  nomAr: "اسم المترشح بالعربية",
  nomFr: "اسم المترشح بالفرنسية",
  lieuAr: "مكان الولادة بالعربية",
  lieuFr: "مكان الولادة بالفرنسية",
  dateNais: "تاريخ الميلاد",
  moy: "المعدل العام",
  anonyme: "رقم ال anonyme",
  etcc: "رقم ETCC"
}
```

### مثال:

```javascript
"12345": {
  nni: "1234567890",
  dossier: "12345",
  serie: "Sciences Expérimentales",
  decision: "Admis",
  centreAr: "ثانوية example",
  centreFr: "Lycée example",
  nomAr: "اسم المترشح",
  nomFr: "Nom du candidat",
  lieuAr: "مكان الولادة",
  lieuFr: "Lieu naissance",
  dateNais: "1 janv. 2000",
  moy: "15.20",
  anonyme: "12345",
  etcc: "SN14"
}
```

---

## 🖊️ تعديل بيانات مترشح موجود

ابحث عن رقم ملفه في `candidates` وغيّر القيم المطلوبة مباشرة.

**مثال:** لتغيير المعدل لـ 52477:

```javascript
"52477": {
  ...
  moy: "15.00",  // ← غيّر القيمة هنا
  ...
}
```

---

## 🌐 تعديل الترجمة (فرنسي/عربي)

ابحث عن:

```javascript
const translations = {
  fr: { ... },   // ← التسميات بالفرنسية
  ar: { ... }    // ← التسميات بالعربية
};
```

أضف أو عدّل أي تسمية تريدها في اللغتين.

---

## 🚀 رفع التعديلات إلى الإنترنت

افتح **Terminal/PowerShell** في مجلد `dec` واكتب:

```powershell
git add -A
git commit -m "شرح التعديل"
git push
```

### بعد الرفع:

1. امسح **Cloudflare cache**:
   - افتح https://dash.cloudflare.com/
   - اختر `releveeducationgovmrcandidat.dpdns.org`
   - Caching → Configuration → Purge Everything

2. انتظر دقيقة إلى دقيقتين

---

## 🔗 الروابط

| الرابط | الوظيفة |
|--------|---------|
| `releveeducationgovmrcandidat.dpdns.org` | يحوّل إلى الموقع الحكومي |
| `releveeducationgovmrcandidat.dpdns.org/?id=52477` | يعرض بيانات المترشح رقم 52477 |

---

## 📝 ملاحظات

- كل البيانات محفوظة في `index.html` نفسه (لا يوجد قاعدة بيانات)
- عند إضافة مترشح جديد، تأكد أن رقم الملف فريد
- التأكد من كتابة الأسماء العربية بشكل صحيح
- المعدل يُحسب خارجيًا ويُدخل يدويًا
