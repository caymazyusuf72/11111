
3D CUTLIST OPTIMIZER - DirectAdmin Kurulum Talimatları
========================================================

Bu paket, 3D Cutlist Optimizer web uygulamasının DirectAdmin hosting panelinde çalışacak şekilde hazırlanmış versiyonudur.

KURULUM ADIMLARı:
================

1. DirectAdmin paneline giriş yapın
2. File Manager'ı açın
3. public_html klasörüne gidin
4. Bu zip dosyasının içindeki TÜM dosyaları public_html klasörüne yükleyin
5. Dosyaların doğru yüklendiğinden emin olun:
   - index.html
   - assets/ klasörü (CSS, JS ve resim dosyaları)
   - .htaccess dosyası

ÖNEMLI NOTLAR:
=============

- .htaccess dosyası React Router'ın düzgün çalışması için gereklidir
- Eğer .htaccess dosyası görünmüyorsa, File Manager'da "Show Hidden Files" seçeneğini aktifleştirin
- Uygulama tamamen client-side çalıştığı için PHP veya veritabanı gerektirmez
- Modern tarayıcılarda (Chrome, Firefox, Safari, Edge) çalışır

ÖZELLIKLER:
==========

✓ 3D görselleştirme ile malzeme optimizasyonu
✓ Büyük blok boyutları girişi (X ve Z eksenleri)
✓ Küçük parçalar için detaylı form
✓ Y ekseni otomatik optimizasyonu (1-240 cm arası)
✓ Fire hesaplama (m³ cinsinden)
✓ Responsive tasarım (mobil uyumlu)
✓ Modern, kullanıcı dostu arayüz

TEKNIK DETAYLAR:
===============

- Framework: React + Three.js
- Dosya boyutu: ~1.8 MB
- Tarayıcı desteği: ES6+ destekleyen tüm modern tarayıcılar
- Hosting gereksinimleri: Statik dosya hosting (PHP/MySQL gerekmez)

DESTEK:
=======

Herhangi bir sorun yaşarsanız:
- .htaccess dosyasının yüklendiğinden emin olun
- Tarayıcı cache'ini temizleyin
- Modern bir tarayıcı kullandığınızdan emin olun

© 2025 3D Cutlist Optimizer - Tüm hakları saklıdır

