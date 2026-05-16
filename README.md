# LabelApp2 — YOLO Görüntü Etiketleme & Eğitim Aracı

Bounding box etiketleme ve YOLO model eğitimi için masaüstü uygulaması — PyQt5 ile geliştirildi. **Ubuntu** ve **Windows** üzerinde çalışır.

---

## Özellikler

- **Dikdörtgen etiketleme** — sol tık sürükle ile bounding box çiz
- **Taşıma & yeniden boyutlandırma** — boxları sürükleyerek taşı, köşe tutamaçlarıyla boyutlandır
- **Sağ tık menüsü** — herhangi bir box'u sil veya sınıfını değiştir
- **Sınırsız etiket sınıfı** — özel isim ve renk, istediğin zaman yeniden adlandır/renklendir
- **Otomatik kaydetme** — resim değiştirilince etiketler otomatik kaydedilir
- **Alt klasör tarama** — tüm alt klasörlerdeki resimleri otomatik bulur
- **Dış veri seti desteği** — Roboflow, LabelImg, CVAT exportlarındaki `data.yaml` ve `classes.txt` dosyalarını otomatik okur
- **YOLO eğitimi** — YOLO11, YOLOv8, YOLOv9, YOLOv10 desteği, canlı log çıktısı
- **Hazır veri seti kullanımı** — Roboflow/Ultralytics veri setlerini yeniden export etmeden direkt eğit
- **Koyu tema** — uzun etiketleme oturumlarında göz yormaz

---

## Klasör Yapısı

```
fotograflar/
├── foto1.jpg
├── foto2.jpg
└── labels/                  # otomatik oluşturulur
    ├── foto1.txt
    ├── foto2.txt
    └── labelapp_classes.json
```

---

## Kurulum

### Gereksinimler

- Python 3.10+
- Anaconda (önerilir)
- NVIDIA GPU (isteğe bağlı, eğitim için önerilir)

### Adımlar

```bash
# 1. Repoyu klonla
git clone https://github.com/ArifEmreYaman/labelapp2.git
cd labelapp2

# 2. Conda ortamı oluştur
conda create -n labelapp python=3.10 -y
conda activate labelapp

# 3. PyQt5'i conda üzerinden kur (Linux'ta xcb sorununu önler)
conda install pyqt -y

# 4. Diğer kütüphaneleri kur
pip install ultralytics PyYAML numpy opencv-python Pillow
```

---

## Çalıştırma

```bash
conda activate labelapp
cd labelapp2
python main.py
```

---

## Kullanım Kılavuzu

### 1. Etiketleme

| İşlem | Nasıl Yapılır |
|-------|---------------|
| Resim klasörü aç | `Dosya > Klasör Aç` veya araç çubuğu butonu |
| Bounding box çiz | Resim üzerinde sol tık sürükle |
| Box seç | Sol tık ile üzerine tıkla |
| Box taşı | Seçili boxın içine tıklayıp sürükle |
| Box boyutlandır | Beyaz köşe tutamaçlarını sürükle |
| Box sil | Sağ tık → Sil, veya seç + `Del` tuşu |
| Box sınıfını değiştir | Sağ tık → Sınıf Değiştir |
| Sonraki / Önceki resim | `D` / `A` tuşları veya araç çubuğu butonları |
| Kaydet | `Ctrl+S` (resim değiştirilince otomatik kaydedilir) |

### 2. Sınıf Yönetimi

- Sağ panelde **+ Ekle** butonuyla özel renkli sınıf ekle
- Sınıf adına **çift tıklayarak** yeniden adlandır
- **Renk** butonuyla rengini değiştir
- Herhangi bir bounding box'a sağ tık → **Sınıf Değiştir** ile sınıf ata

### 3. Eğitim

1. Araç çubuğundaki **Eğitimi Başlat** butonuna tıkla
2. YOLO modelini seç (YOLO11m önerilir)
3. Epoch sayısı, batch size ve görüntü boyutunu ayarla
4. Çıktı klasörünü seç
5. **Eğitimi Başlat** butonuna bas

> **İpucu:** Roboflow/Ultralytics veri seti açtığında ve klasörde `data.yaml` varsa, uygulama otomatik algılar ve yeniden export etmeden direkt kullanma seçeneği sunar.

---

## Desteklenen Label Formatları (içe aktarma)

Uygulama, label dosyalarını şu konumlarda otomatik arar:

| Format | Konum |
|--------|-------|
| LabelApp2 formatı | `resim_klasoru/labels/resim.txt` |
| LabelImg (inline) | `resim_klasoru/resim.txt` |
| YOLO standart | `images/` klasörü + kardeş `labels/` klasörü |
| Roboflow | `train/images/` + `train/labels/` |

---

## Desteklenen YOLO Modelleri

| Aile | Varyantlar |
|------|------------|
| YOLO11 | n, s, m, l, x |
| YOLOv8 | n, s, m, l, x |
| YOLOv9 | c, e |
| YOLOv10 | n, s, m, l, x |

---

## Sorun Giderme

**Ubuntu'da Qt "xcb" eklentisi hatası:**
```bash
conda install pyqt -y   # pip yerine conda ile kur
```

**Eğitim başarısız — "resim bulunamadı":**
Çıktı klasörünün var olduğundan ve en az 1 etiketlenmiş resim bulunduğundan emin ol.

**Yeniden açınca sınıflar cls0 olarak görünüyor:**
Uygulama sınıf isimlerini `labels/labelapp_classes.json` dosyasına kaydeder. Bu dosya yoksa sağ panelden sınıfları tekrar ekle.

---

## Lisans

MIT Lisansı — özgürce kullanabilir, değiştirebilir ve dağıtabilirsin.

---

## Geliştirici

**Arif Emre Yaman** — [github.com/ArifEmreYaman](https://github.com/ArifEmreYaman)
