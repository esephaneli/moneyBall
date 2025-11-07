# moneyBall
Inspired by the Moneyball movie — a machine learning model that identifies undervalued football players through data-driven performance analysis.

# ⚽ Moneyball Football — 2024–2025  
*Bir filmden ilham al, verilerle hikâyeni yaz.*

---

## 🎬 İlham
Bu proje, **Moneyball (2011)** filminden esinlenerek oluşturuldu.  
Filmde Brad Pitt’in karakteri, kısıtlı bütçeyle istatistiklerle “değerli oyuncuları” keşfediyordu.  
Ben de aynı mantığı futbola taşıdım:  
> “Ucuz ama performans olarak elit oyuncular” bulmak.

---

## 🎯 Amaç
Futbolcuların istatistiklerinden yola çıkarak, **performansına göre düşük maliyetli (undervalued)** oyuncuları tespit etmek.  
Kısacası veriyle “fiyat/performans dengesini” ölçmek.

---

## ⚙️ Adımlar
- 2854 oyuncu, 267 kolon  
- Kolon temizleme, normalizasyon  
- En az 900 dakika filtresi  
- **Per-90 metrikleri:**  
  `xg_per90`, `xag_per90`, `kp_per90`, `prgp_per90`, `prgc_per90`, `tkl_int_per90`, `clr_per90`, `blocks_per90`
- Pozisyona özgü **performans skorları (FW, MF, DF için farklı ağırlıklar)**  
- **Value Index**:  
  `0.60 * perf_score_norm + 0.20 * min_norm + 0.20 * (1 - age_norm)`
- Görselleştirme: Age vs Value Index, Top-10 oyuncu bar grafikleri
- **Model:** `RandomForestRegressor`  
  - Train R² = 0.97  
  - Test R² = 0.73

---

## 📊 En Önemli Özellikler
| Özellik | Açıklama | Importance |
|----------|-----------|------------|
| `clr_per90` | Clearances per 90 | 0.515 |
| `prgp_per90` | Progressive Passes per 90 | 0.279 |
| `tkl_int_per90` | Tackles + Interceptions | 0.054 |
| `prgc_per90` | Progressive Carries | 0.042 |
| `blocks_per90` | Blocks | 0.032 |

---

## 💎 Top-10 Undervalued Defenders
| Oyuncu | Takım | Gerçek | Tahmin |
|---------|--------|---------|---------|
| Dean Huijsen | Bournemouth | 0.84 | 0.77 |
| Guela Doué | Strasbourg | 0.80 | 0.76 |
| Diego Coppola | Hellas Verona | 0.80 | 0.75 |
| Diogo Leite | Union Berlin | 0.79 | 0.75 |
| Antonee Robinson | Fulham | 0.79 | 0.75 |

---

## 🧠 Önceki Çalışma
Aynı veri setiyle ilk olarak **basit polinom regresyon** denemeleri yaptım.  
Ancak futbol çok boyutlu bir oyun olduğu için, o model bazı dinamikleri yakalayamıyordu.  
Bu farkındalık beni pozisyon bazlı “per-90 + Random Forest” yaklaşımına yönlendirdi.

---

## 🧩 Geliştirilebilir Noktalar
- Kaleci (GK) için ayrı modelleme (save%, psxg, cs%)  
- Gerçek piyasa değeriyle fiyat tahmini  
- Optuna / SHAP açıklanabilirlik ekleme  
- Transfer değeri tahmini ve etiketleme

---

## 💬 Son Söz
> “You’re not just buying players, you’re buying wins.”
> "Sadece oyuncu satın almıyorsunuz, galibiyet de satın alıyorsunuz."  
> — Moneyball (2011)
