# إعداد المزامنة مع حساب Google (مرة واحدة)

اسم الحزمة: `com.personal.myapp`
بصمة SHA-1: `66:DB:4E:C4:73:84:20:FC:1E:08:B9:24:AF:6D:E4:72:DB:2D:19:9B`

1. افتحي console.firebase.google.com ← Add project ← سمّيه «hawshi» (عطّلي Analytics).
2. Project settings ← Add app ← Android: الحزمة `com.personal.myapp`، وفي Add fingerprint ضعي SHA-1 أعلاه.
3. Build ← Authentication ← Get started ← Sign-in method ← Google ← Enable ← Save.
4. Build ← Firestore Database ← Create ← اختاري أقرب موقع (لا يتغير لاحقاً) ← Production mode.
5. Firestore ← Rules، الصقي ثم Publish:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{uid}/{document=**} {
      allow read, write: if request.auth != null && request.auth.uid == uid;
    }
  }
}
```
6. Project settings ← Your apps ← حمّلي google-services.json (بعد خطوة 3 فقط!).
7. ارفعيه إلى المستودع my-app في الجذر بجانب app.zip، وسيبني GitHub نسخة جديدة تلقائياً.
8. ثبّتي الـAPK ← ⚙️ ← تسجيل الدخول بحساب Google.
