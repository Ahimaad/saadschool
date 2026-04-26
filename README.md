# 🏫 بوابة مدرسة سعد بن أبي وقاص الرسمية للغات

<div align="center">

![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen?logo=github)
![Firebase](https://img.shields.io/badge/Firebase-Connected-orange?logo=firebase)
![Mobile Ready](https://img.shields.io/badge/Mobile-Ready-blue?logo=android)
![Security](https://img.shields.io/badge/Security-Protected-red?logo=shield)
![Arabic RTL](https://img.shields.io/badge/Arabic-RTL-gold)

**بوابة تعليمية رقمية متكاملة — إدارة الفشن التعليمية — محافظة بني سويف**

[🌐 زيارة الموقع](https://username.github.io) · [🐛 الإبلاغ عن مشكلة](../../issues) · [💡 اقتراح ميزة](../../issues)

</div>

---

## ✨ المميزات

| الميزة | الوصف |
|--------|-------|
| 🎓 **استعلام النتائج** | بحث فوري بالصف ورقم الجلوس مع مشاركة واتساب |
| 📁 **رفع الملفات** | دعم كامل لكل الأنواع (PDF, Word, صور, فيديو...) مع Drag & Drop |
| 🖼️ **المعرض الرقمي** | عرض الصور والملفات بشكل بطاقات مع تعليقات |
| 📖 **المكتبة الرقمية** | تخزين واسترجاع المراجع والكتب |
| 📰 **ركن الأخبار** | تعميمات ومستجدات المدرسة |
| 🌙 **الوضع الليلي** | Dark Mode مع حفظ التفضيل |
| 📱 **تصميم متجاوب** | يعمل على الجوال والتابلت واللابتوب |
| 🔐 **لوحة إدارة** | صلاحيات خاصة للمدير مع حماية Brute Force |
| 🔒 **أمان كامل** | Firebase Secrets محمية عبر GitHub Actions |
| ⚡ **أداء عالي** | AOS Animations + Swiper Slider + Counter Animations |

---

## 🗂️ هيكل المشروع

```
school-portal/
│
├── 📄 index.html                          ← الموقع الكامل
├── 🖼️ logo.jpg                            ← شعار المدرسة
├── 📖 README.md                           ← هذا الملف
├── 🚫 .gitignore                          ← ملفات محظورة من الرفع
│
└── 📁 .github/
    └── 📁 workflows/
        └── ⚙️ deploy.yml                  ← النشر التلقائي
```

---

## 🚀 الإعداد خطوة بخطوة

### الخطوة 1 — إعداد Firebase

1. اذهب إلى [Firebase Console](https://console.firebase.google.com)
2. أنشئ مشروعاً جديداً أو استخدم الموجود
3. فعّل **Realtime Database** واضبط القواعد:

```json
{
  "rules": {
    "results": {
      ".read": true,
      ".write": false
    },
    "gallery_section": {
      ".read": true,
      ".write": true
    },
    "library_section": {
      ".read": true,
      ".write": true
    },
    "art_section": {
      ".read": true,
      ".write": true
    },
    "student_files": {
      ".read": true,
      ".write": true
    }
  }
}
```

4. فعّل **Storage** واضبط القواعد:

```
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /uploads/{allPaths=**} {
      allow read: if true;
      allow write: if request.resource.size < 50 * 1024 * 1024;
    }
  }
}
```

5. أضف دومين GitHub Pages في **Authentication → Settings → Authorized Domains**:
   ```
   username.github.io
   ```

---

### الخطوة 2 — إضافة GitHub Secrets

في GitHub Repository اذهب إلى:
**Settings → Secrets and variables → Actions → New repository secret**

أضف هذه الـ Secrets بالضبط:

| اسم الـ Secret | من أين تأخذه |
|----------------|-------------|
| `FIREBASE_API_KEY` | Firebase Console → Project Settings → apiKey |
| `FIREBASE_AUTH_DOMAIN` | Firebase Console → authDomain |
| `FIREBASE_DATABASE_URL` | Firebase Console → databaseURL |
| `FIREBASE_PROJECT_ID` | Firebase Console → projectId |
| `FIREBASE_STORAGE_BUCKET` | Firebase Console → storageBucket |
| `FIREBASE_MESSAGING_SENDER_ID` | Firebase Console → messagingSenderId |
| `FIREBASE_APP_ID` | Firebase Console → appId |
| `ADMIN_SECRET_KEY` | نتيجة `btoa("كلمة_سرك")` في console المتصفح |

> **💡 كيف تحصل على ADMIN_SECRET_KEY؟**
> افتح المتصفح، اضغط F12، ثم في Console اكتب:
> ```js
> btoa("كلمة_سرك_القوية_هنا")
> ```
> انسخ النتيجة وضعها في الـ Secret

---

### الخطوة 3 — تفعيل GitHub Pages

1. اذهب إلى **Settings → Pages**
2. في **Source** اختر: **GitHub Actions**
3. احفظ الإعدادات

---

### الخطوة 4 — رفع الكود وتشغيل النشر

```bash
# استنساخ أو تهيئة المستودع
git init
git add .
git commit -m "🚀 Initial commit - School Portal"
git branch -M main
git remote add origin https://github.com/username/school-portal.git
git push -u origin main
```

بعد الرفع، اذهب إلى **Actions** في GitHub وستجد الـ workflow يعمل تلقائياً. ✅

---

### الخطوة 5 — إضافة النتائج لقاعدة البيانات

في **Firebase Console → Realtime Database** أضف البيانات بهذا الشكل:

```json
{
  "results": {
    "p6": {
      "1001": {
        "name": "أحمد محمد علي",
        "subjects": {
          "اللغة العربية": 95,
          "الرياضيات": 88,
          "العلوم": 91,
          "اللغة الإنجليزية": 85
        },
        "total": 359,
        "percentage": 89.75,
        "grade": "ممتاز"
      }
    }
  }
}
```

---

## 🔄 سير عمل النشر

```
رفع الكود على main
        ↓
GitHub Actions يشتغل تلقائياً
        ↓
✅ فحص: index.html موجود؟
✅ فحص: لا توجد API Keys مكشوفة؟
        ↓
🔐 حقن Firebase Secrets في الكود
        ↓
🔑 تحديث كلمة سر الإدارة
        ↓
📅 إضافة تاريخ آخر تحديث
        ↓
📤 رفع الملفات لـ GitHub Pages
        ↓
🌐 الموقع يعمل على الإنترنت
```

---

## 🔒 الأمان

- ✅ **Firebase Config** محمية في GitHub Secrets — لا تظهر في الكود
- ✅ **كلمة السر** مشفرة ومخزنة كـ Secret
- ✅ **Brute Force Protection** — قفل تلقائي بعد 5 محاولات خاطئة
- ✅ **XSS Protection** — تنظيف كل المدخلات
- ✅ **File Size Limit** — 50 MB حد أقصى للرفع
- ✅ **Storage Rules** — قيود على رفع الملفات

---

## 📱 الأجهزة المدعومة

| الجهاز | الدعم |
|--------|-------|
| 📱 الجوال (iOS / Android) | ✅ كامل + شريط تنقل سفلي |
| 📟 التابلت | ✅ كامل |
| 💻 اللابتوب | ✅ كامل + قائمة جانبية |
| 🖥️ الكمبيوتر | ✅ كامل |

---

## 🛠️ التقنيات المستخدمة

| التقنية | الاستخدام |
|---------|-----------|
| **Firebase Realtime DB** | تخزين النتائج والملفات والتعليقات |
| **Firebase Storage** | رفع وتخزين الملفات |
| **Bootstrap 5** | التصميم المتجاوب |
| **Swiper.js** | السلايدر الاحترافي |
| **AOS** | حركات عند التمرير |
| **SweetAlert2** | نوافذ تنبيه جميلة |
| **Font Awesome 6** | الأيقونات |
| **Cairo Font** | الخط العربي |
| **GitHub Actions** | النشر التلقائي الآمن |
| **GitHub Pages** | الاستضافة المجانية |

---

## 📞 التواصل

**مدرسة سعد بن أبي وقاص الرسمية للغات**
إدارة الفشن التعليمية — محافظة بني سويف

---

<div align="center">
صُنع بـ ❤️ لدعم العملية التعليمية الرقمية
</div>
