##Görüntü İşleme##
Bu proje, mikroskobik görüntülerde hücrelerin klasik görüntü işleme yöntemleri kullanılarak bölütlenmesini ve sayılmasını amaçlamaktadır. Ayrıca ardışık görüntüler üzerinden hücre sayısındaki zamansal değişimler incelenmektedir.

Çalışmada derin öğrenme yöntemleri kullanılmamıştır.

 Kullanılan Veri Seti

Cell Tracking Challenge – Fluo-N2DH-GOWT1

Veri setinden toplam 30 görüntü seçilmiştir:

- Development: 10 görüntü
- Validation: 5 görüntü
- Test: 15 görüntü

Development ve Validation görüntüleri birinci diziden, bağımsız Test görüntüleri ise ikinci diziden seçilmiştir.

Görüntü seçiminde tekrarlanabilirliği sağlamak amacıyla `14928` rastgelelik tohumu kullanılmıştır.

Kullanılan Yöntemler

Projede aşağıdaki yöntemler karşılaştırılmıştır:

- Contrast Stretching, Histogram Equalization ve CLAHE
- Gaussian, Median ve Sharpening filtreleri
- Sabit eşikleme, Otsu ve Adaptive Thresholding
- Morfolojik Opening ve Closing işlemleri
- Connected Components yöntemiyle hücre sayımı

Development aşamasında toplam 33 deneysel yapılandırma değerlendirilmiştir.

Seçilen Nihai Yöntem

Validation sonuçlarına göre seçilen nihai işlem hattı:

1. Orijinal görüntünün alınması
2. Sabit eşikleme (Threshold = 25)
3. Opening (3×3)
4. Closing (3×3)
5. Connected Components ile hücre sayımı (minimum alan = 50 piksel)

Deney Sonuçları

| Değerlendirme | MAE |
|---|---:|
| Development – Seçilen yöntem | 2.20 |
| Validation – Seçilen yöntem | 1.80 |
| Test – Baseline | 7.27 |
| Test – Nihai yöntem | 13.67 |

Nihai yöntem Validation aşamasında başarılı sonuçlar vermesine rağmen bağımsız Test dizisinde Baseline yönteminden daha yüksek hata üretmiştir.

Bu durum, yöntemin farklı görüntü dizilerine genellenebilirliğinin sınırlı olduğunu göstermektedir.

Kullanılan Teknolojiler

- Python
- OpenCV
- NumPy
- Pandas
- SciPy
- scikit-image
- Matplotlib
- Google Colab

Projenin Çalıştırılması

Gerekli Python kütüphaneleri aşağıdaki komutla yüklenebilir:

```bash
pip install -r requirements.txt
```

Ardından `main.ipynb` dosyası Google Colab ortamında açılarak hücreler sırasıyla çalıştırılabilir.

Veri seti proje kodu aracılığıyla indirilir.

Proje Dosyaları

- `main.ipynb`: Görüntü işleme ve değerlendirme kodları
- `selected_frames.csv`: Seçilen görüntülerin listesi
- `experiments.csv`: Development deneyleri
- `validation_results.csv`: Validation sonuçları
- `final_pipeline.json`: Nihai yöntem parametreleri
- `test_predictions_locked.csv`: Test tahminleri
- `test_results.csv`: Test değerlendirme sonuçları
- `requirements.txt`: Gerekli kütüphaneler

Sonuç

Bu çalışma, klasik görüntü işleme yöntemlerinin hücre segmentasyonu ve sayımı üzerindeki etkilerini karşılaştırmalı olarak incelemektedir. Elde edilen sonuçlar, farklı görüntü dizilerinde performansın değişebileceğini ve bağımsız test değerlendirmenin önemini ortaya koymaktadır.


Veri Setinin Resmî İndirme Bağlantısı

- Cell Tracking Challenge (2D+Time): https://celltrackingchallenge.net/2d-datasets/
- Fluo-N2DH-GOWT1 eğitim veri seti (01 ve 02 dizileri ile mevcut referans anotasyonları içerir): https://data.celltrackingchallenge.net/training-datasets/Fluo-N2DH-GOWT1.zip

Not: Bu projedeki bağımsız test bölümü, yukarıdaki eğitim arşivinin 02 dizisinden seçilmiştir; Cell Tracking Challenge sitesindeki ayrı ve anotasyonsuz yarışma test arşivi kullanılmamıştır. Veri seti görüntüleri ve GT maskeleri bu depoya yüklenmemelidir.
