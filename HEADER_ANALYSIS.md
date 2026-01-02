# Header Analizi - Shopify Tema

## 📍 Header Dosyası Konumu
- **Ana Dosya**: `sections/header.liquid` (4294 satır)
- **JavaScript**: `assets/section.header.js` (904 satır)
- **Layout'ta Kullanımı**: `layout/theme.liquid` - Satır 259: `{% section 'header' %}`

## 🏗️ Header Yapısı

### 1. **Başlangıç ve Hazırlık (Satır 1-77)**
```liquid
{% include 'global-variables' %}
```
- Global değişkenler yüklenir
- Design mode kontrolü yapılır
- Block tipleri filtrelenir:
  - `tape` - Üst banner/tape
  - `info_line` - Bilgi satırı
  - `colorize` - Renklendirme
  - `megamenu` - Mega menü blokları
  - `menu` - Menü blokları
  - `megamenu_label` - Menü etiketleri (hot, sale, new)
  - `megamenu_title_image` - Menü başlık görselleri
  - `icon` - İkonlar

### 2. **Sticky Header Ayarları (Satır 78-93)**
- Desktop ve mobile sticky header desteği
- Sticky logo ayarları
- Farklı header tipleri için özel sticky davranışları

### 3. **CSS Değişkenleri ve Stil Tanımlamaları (Satır 99-995)**
- CSS custom properties (CSS variables) ile dinamik stil yönetimi
- 4 farklı header style:
  - `style-1`: Varsayılan stil
  - `style-2`: Koyu tema
  - `style-3`: Açık/koyu karışım
  - `style-4`: Özel stil
- 7 farklı header type:
  - `type-1` ila `type-7`: Farklı layout düzenleri
- Responsive font boyutları
- Renk şemaları (theme, theme2, theme3, theme4, theme-primary)
- Animasyon süreleri

### 4. **HTML Yapısı (Satır 999-4294)**

#### Ana Header Elementi
```html
<header-section data-section-id="{{ section.id }}" data-section-type="header">
  <header id="header" class="header header--type-{{ section.settings.type }} header--style-{{ section.settings.style }}">
```

#### Bileşenler:

**a) Tape/Banner (Satır 1004-1022)**
- Üstte gösterilen banner mesajları
- Cookie ile kapatma özelliği
- Delay (gecikme) ayarı
- Otomatik kapatma

**b) Info Line (Satır 1023-1038)**
- Üst bilgi satırı
- Sosyal medya linkleri
- HTML içerik desteği

**c) Sticky Header Wrapper (Satır 1001-1003)**
```html
<sticky-header class="header--sticky-type-{{ section.settings.desktop_sticky_type }}">
```

**d) Logo (Satır 1050-1074)**
- Desktop ve mobile logo desteği
- SVG ve image format desteği
- Sticky header için ayrı logo
- Farklı header tiplerine göre konumlandırma

**e) Menü Butonu (Satır 1039-1049)**
- Mobil hamburger menü
- Navigation popup tetikleyicisi

**f) Account Butonu (Satır 1075-1100+)**
- Growave entegrasyonu
- Customer login/logout
- Dropdown menü

**g) Search (Satır 1100+)**
- Arama butonu
- AJAX arama desteği

**h) Cart (Satır 1100+)**
- Sepet butonu
- Sepet sayacı
- Popup sepet

**i) Menüler**
- Ana menü (horizontal)
- Vertical menü
- Mega menü desteği
- Dropdown menüler
- Mobile menü navigasyonu

## ⚙️ JavaScript Fonksiyonalitesi

### 1. **MenuBuilder Class** (`section.header.js`)

#### Özellikler:
- **Vertical Menu**: Dikey menü yönetimi
- **Mobile Menu**: Mobil menü navigasyonu
- **Mega Menu**: Büyük dropdown menüler
- **Dropdown Menu**: Normal dropdown menüler
- **Preview Images**: Menü öğelerinde görsel önizleme

#### Ana Fonksiyonlar:

**a) `init()`**
- Menü elementlerini başlatır
- Event handler'ları ekler
- Responsive handler'ları ayarlar

**b) `_toggleMegamenu()`**
- Mega menü açma/kapatma
- Animasyon yönetimi
- Curtain (perde) efekti
- Height hesaplamaları

**c) `closeMobileMenu()`**
- Mobil menüyü kapatır
- Level sıfırlama
- Transition yönetimi

**d) Vertical Menu Özellikleri**
- Fixed pozisyon desteği
- Height kontrolü
- "See All" butonu
- Scroll yönetimi

### 2. **HeaderSection Class** (Custom Element)

#### Web Component olarak tanımlanmış:
```javascript
customElements.define('header-section', HeaderSection);
```

#### Metodlar:

**a) `load()`**
- Container'ı başlatır
- Menüleri başlatır
- Tape'i başlatır
- Currency ve language switcher'ları başlatır

**b) `menuInit()`**
- Ana menüyü başlatır
- Vertical menüyü başlatır
- MenuBuilder instance'ları oluşturur

**c) `tapeInit()`**
- Header tape/banner'ı yönetir
- Cookie kontrolü
- Delay ve show-once ayarları
- Slide animasyonları

**d) `currencyInit()`**
- Para birimi değiştirme formu
- Select change event handler

**e) `languagesInit()`**
- Weglot entegrasyonu
- Dil değiştirme dropdown'u
- Aktif dil gösterimi

**f) `widthLimitInit()`**
- Header genişlik limitleri
- Responsive genişlik hesaplamaları
- Edge detection

## 🔄 Çalışma Akışı

### 1. **Sayfa Yüklendiğinde:**
```
1. Layout'ta {% section 'header' %} çağrılır
2. sections/header.liquid render edilir
3. CSS değişkenleri hesaplanır
4. HTML yapısı oluşturulur
5. JavaScript yüklenir (section.header.js)
6. HeaderSection custom element oluşturulur
7. MenuBuilder instance'ları başlatılır
```

### 2. **Menü Etkileşimi:**
```
Desktop:
- Mouse hover → Mega menu/dropdown açılır
- Mouse leave → Kapanır
- Animasyonlu geçişler

Mobile:
- Hamburger tıkla → Navigation popup açılır
- Menü öğesine tıkla → Alt menü gösterilir
- Back butonu → Üst seviyeye dön
- Close butonu → Menüyü kapat
```

### 3. **Sticky Header:**
```
Scroll down:
- Header sabitlenir (sticky)
- Logo değişebilir (sticky logo)
- Scroll up'da gizlenebilir (hide when scroll down)
```

## 📦 İlgili Snippet'ler

- `snippets/header-get-menu.liquid` - Menü HTML'i oluşturur
- `snippets/header-get-menu-megamenu.liquid` - Mega menü yapısı
- `snippets/header-get-menu-dropdown.liquid` - Dropdown yapısı
- `snippets/header-get-menu-labels.liquid` - Menü etiketleri
- `snippets/header-get-menu-icons.liquid` - Menü ikonları
- `snippets/logo.liquid` - Logo render
- `snippets/bss-b2b-header.liquid` - B2B header entegrasyonu

## 🎨 Özelleştirme Noktaları

### Section Settings (Shopify Theme Editor):
- Header type (1-7)
- Header style (1-4)
- Sticky settings
- Transparent background
- Menu seçimi
- Vertical menu seçimi

### Blocks:
- Tape blocks
- Info line blocks
- Megamenu blocks
- Menu blocks
- Icon blocks
- Colorize blocks

## 🔧 Teknik Detaylar

### CSS Variables Kullanımı:
- Tüm renkler ve boyutlar CSS variables ile yönetiliyor
- Theme editor'dan değiştirilebilir
- Responsive breakpoint'lerde otomatik güncellenir

### Responsive Handler:
- Desktop ve mobile için ayrı event handler'lar
- Breakpoint değişimlerinde otomatik yeniden başlatma
- Namespace ile event çakışmaları önlenir

### Animation System:
- CSS transitions
- jQuery animate
- Custom duration ayarları
- Theme animation settings'e bağlı

## 🚀 Performans Optimizasyonları

1. **Lazy Loading**: Inline styles template olarak yüklenir
2. **Event Delegation**: Performans için event delegation kullanılır
3. **Responsive Handlers**: Sadece gerekli breakpoint'lerde aktif
4. **Destroy Methods**: Component unmount'ta temizlik yapılır

## 📝 Notlar

- Header çok büyük bir dosya (4294 satır)
- Modüler yapıda snippet'ler kullanılıyor
- Custom element (Web Component) kullanımı
- jQuery bağımlılığı var
- Theme global object'e bağımlı

