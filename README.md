# Şimşek Kurye - Proje Yönetim Paneli

⚡ Modern, basit ve gerçek zamanlı proje yönetim dashboard'u.

## Özellikler

- 📝 Metin bazlı döküman yönetimi
- � **Belge yükleme** (PDF & DOCX desteği)
- �🔄 Gerçek zamanlı senkronizasyon (Firebase)
- ➕ Sekme ekleme/silme
- ✏️ İçerik düzenleme
- 📱 Responsive tasarım
- 📤 Sürükle-bırak dosya yükleme
- 📥 Belge indirme ve görüntüleme

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
4. **Authentication** > Anonymous girişi etkinleştirin
5. **Firestore Database** oluşturun
6. **Storage** > Storage oluşturun (Belge yükleme için gerekli)

### 3. Firebase Storage Kuralları

Firebase Console > Storage > Rules bölümünde aşağıdaki kuralları ayarlayın:

```javascript
rules_version = '2';
service firebase.storage {
  match /b/{bucket}/o {
    match /documents/{allPaths=**} {
      allow read: if true;
      allow write: if request.auth != null 
        && request.resource.size < 10 * 1024 * 1024  // 10MB limit
        && (request.resource.contentType.matches('application/pdf') 
            || request.resource.contentType.matches('application/vnd.openxmlformats-officedocument.wordprocessingml.document')
            || request.resource.contentType.matches('application/msword'));
    }
  }
}
```

### 4. Config dosyasını oluşturun

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

### 5. Çalıştırın

```bash
python3 -m http.server 8000
```

Tarayıcıda açın: http://localhost:8000

## Kullanım

### Yeni Sekme Ekleme

1. Sol paneldeki **+** butonuna tıklayın
2. Sekme türü seçin:
   - **Metin**: Not veya metin içeriği için
   - **Belge**: PDF veya DOCX dosyası yüklemek için
3. Belge seçtiyseniz:
   - **Cihazdan Yükle**: Bilgisayarınızdan dosya seçin
   - **Google Drive**: (Yakında) Drive'dan dosya seçin
4. Dosyanızı sürükleyip bırakın veya tıklayarak seçin
5. Başlık girin ve yükleyin

### Desteklenen Dosya Formatları

- 📕 **PDF**: Tarayıcıda doğrudan görüntülenir
- 📘 **DOCX**: HTML'e dönüştürülerek gösterilir
- 📄 **DOC**: Word belgesi (eski format)

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
- Belge boyutu 10MB ile sınırlıdır
- Sadece PDF ve DOCX formatları kabul edilir

## Lisans

MIT
