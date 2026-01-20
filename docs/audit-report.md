# Browser Extension Security Auditor Proje Raporu

## 1. Proje Amacı

Bu projenin amacı, seçilen bir tarayıcı uzantısının (browser extension) güvenlik açısından analiz edilmesi ve potansiyel risklerin tespit edilmesidir. Çalışma kapsamında Lightshot ekran görüntüsü alma eklentisi incelenmiştir.

---

## 2. İncelenen Uzantı Bilgileri

Uzantı Adı: Lightshot Screenshot Tool  
Platform: Google Chrome  
Sürüm: 7.0.1  
Kaynak: Chrome Web Store  

---

## 3. Kullanılan Yöntem

Analiz sürecinde aşağıdaki adımlar uygulanmıştır:

- Uzantı kaynak dosyaları elde edilmiştir.
- manifest.json dosyası incelenmiştir.
- İzinler ve erişim yetkileri analiz edilmiştir.
- Arka plan servisleri ve sayfa etkileşimleri değerlendirilmiştir.
- Potansiyel güvenlik riskleri belirlenmiştir.

---

## 4. Güvenlik Bulguları

### 🔴 Bulgu 1: Tüm Web Sitelerine Erişim İzni

Risk Seviyesi: Yüksek  

Yapılan incelemede uzantının tüm web sitelerine erişim izni istediği tespit edilmiştir. Bu izin sayesinde uzantı, kullanıcının ziyaret ettiği tüm sayfalardaki içeriklere erişebilir.

Bu durum özellikle banka siteleri, sosyal medya platformları ve kişisel bilgi içeren sayfalar açısından gizlilik riski oluşturmaktadır.

Kanıt:
"host_permissions": ["*://*/*"]

Öneri:  
Uzantının yalnızca gerekli alan adlarına erişim izni istemesi, tüm sitelere genel erişim izninden kaçınılması önerilmektedir.

---

### 🔴 Bulgu 2: Çerez (Cookies) Erişim Yetkisi

Risk Seviyesi: Yüksek  

Uzantının tarayıcı çerezlerine erişim yetkisi olduğu görülmüştür. Çerezler oturum bilgileri ve kullanıcı kimlik verileri içerebilir.

Bu durum kötü niyetli kullanım senaryolarında hesap ele geçirme ve gizlilik ihlallerine yol açabilir.

Kanıt:
"permissions": ["cookies"]

Öneri:  
Çerez erişimi sadece zorunlu durumlarda kullanılmalı ve mümkünse tamamen kaldırılmalıdır.

---

### 🟠 Bulgu 3: Panoya Yazma Yetkisi (Clipboard)

Risk Seviyesi: Orta  

Uzantının pano içeriğini değiştirme yetkisine sahip olduğu tespit edilmiştir. Bu durum kullanıcının kopyaladığı verilerin değiştirilmesine veya zararlı bağlantıların panoya eklenmesine neden olabilir.

Kanıt:
"permissions": ["clipboardWrite"]

Öneri:  
Kullanıcıya pano işlemleri sırasında bilgilendirme yapılması ve yetkinin sınırlandırılması önerilmektedir.

---

### 🟠 Bulgu 4: Arka Plan Servis Çalışması

Risk Seviyesi: Orta  

Uzantı arka planda çalışan bir servis (service worker) kullanmaktadır. Bu servis uzantı kapalı olsa bile bazı işlemleri gerçekleştirebilir.

Bu durum gizli veri iletimi ve sürekli ağ iletişimi açısından potansiyel risk oluşturabilir.

Kanıt:
"background": { "service_worker": "sw.js" }

Öneri:  
Arka planda çalışan işlemler sınırlandırılmalı ve gereksiz veri iletimi engellenmelidir.

---

## 5. Genel Değerlendirme ve Sonuç

Yapılan analiz sonucunda Lightshot uzantısının bazı yüksek ve orta seviyeli güvenlik riskleri barındırdığı tespit edilmiştir. Özellikle tüm sitelere erişim ve çerez kullanımı kullanıcı gizliliği açısından dikkat edilmesi gereken noktalardır.

Uzantının güvenliğinin artırılması için izinlerin sınırlandırılması ve arka plan işlemlerinin kontrol altına alınması önerilmektedir.
