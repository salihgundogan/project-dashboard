# Şimşek Kurye - Proje Yönetim Paneli

⚡ Modern, basit ve gerçek zamanlı proje yönetim dashboard'u.

## Özellikler

- � Metin bazlı döküman yönetimi
- 🔄 Gerçek zamanlı senkronizasyon (Firebase)
- ➕ Sekme ekleme/silme
- ✏️ İçerik düzenleme
- 📱 Responsive tasarım

## Kurulum

### 1. Depoyu klonlayın
```bash
git clone https://github.com/KULLANICI_ADINIZ/simsek-kurye-dashboard.git
cd simsek-kurye-dashboard
```

### 2. Firebase yapılandırması

1. [Firebase Console](https://console.firebase.google.com)'a gidin
2. Yeni proje oluşturun
3. Web uygulaması ekleyin
4. Authentication > Anonymous girişi etkinleştirin
5. Firestore Database oluşturun

### 3. Config dosyasını oluşturun

`firebase-config.example.js` dosyasını `firebase-config.js` olarak kopyalayın:

```bash
cp firebase-config.example.js firebase-config.js
```

Kendi Firebase bilgilerinizi girin:

```javascript
window.FIREBASE_CONFIG = {
    apiKey: "SIZIN_API_KEY",
    authDomain: "SIZIN_PROJECT_ID.firebaseapp.com",
    projectId: "SIZIN_PROJECT_ID",
    storageBucket: "SIZIN_PROJECT_ID.appspot.com",
    messagingSenderId: "SIZIN_SENDER_ID",
    appId: "SIZIN_APP_ID"
};
```

### 4. Çalıştırın

```bash
python3 -m http.server 8000
```

Tarayıcıda açın: http://localhost:8000

## Netlify'a Deploy

1. GitHub'a push yapın
2. [Netlify](https://netlify.com)'a gidin
3. "New site from Git" seçin
4. Repo'yu bağlayın
5. Deploy!

⚠️ **Önemli**: Netlify'da Environment Variables olarak Firebase config'i ayarlayın veya `firebase-config.js` dosyasını manuel ekleyin.

## Dosya Yapısı

```
├── index.html                  # Ana uygulama
├── firebase-config.js          # Firebase bilgileri (gitignore'da)
├── firebase-config.example.js  # Örnek config
├── README.md                   # Bu dosya
└── .gitignore
```

## Güvenlik

- `firebase-config.js` dosyası `.gitignore`'da, GitHub'a yüklenmez
- Firebase güvenlik kurallarını ayarlamayı unutmayın

## Lisans

MIT
