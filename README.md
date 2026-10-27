# 🌶️ *Capsicum annuum* ve kapsaisin biyosentezi: keşif amaçlı biyoinformatik denemesi

> **Çalışmanın niteliği:** Bu depo bir bilimsel araştırma yayını, doğrulanmış analiz veya Samandağ biberine ait deneysel/genomik bulgu sunmaz. Biyoinformatik araçlarını denemek ve olası bir iş akışını öğrenmek için hazırlanmış bir prototiptir. Notebook çıktıları yeniden üretilip doğrulanmadıkça sonuç olarak değerlendirilmemelidir.

## Amaç

Bu denemede *Capsicum annuum* için NCBI RefSeq `GCF_002878395.1` (UCD10Xv1.1) referans genomu kullanılarak anotasyonlarda kapsaisin biyosenteziyle ilişkili adları arama, protein dizilerini motif ve hizalama ile inceleme ve seçilmiş protein dizilerini ColabFold Batch biçimine hazırlama adımları bir Jupyter/Colab notebook’unda bir araya getirildi.

Bu referans genom Samandağ’dan alınmış bir örnek olarak tanımlanmamıştır. Dolayısıyla akış, Samandağ biberine özgü bir genom veya kapsaisin miktarı analizi değildir.

## Notebook’ta neler deneniyor?

1. NCBI Datasets CLI ile referans genom paketini indirme.
2. Anotasyon açıklamalarındaki anahtar sözcüklere göre aday CDS ve protein kayıtlarını seçme.
3. Aday proteinlerde BAHD ailesiyle ilişkilendirilen motifleri arama ve bir referans diziyle hizalama denemesi.
4. NCBI Protein veritabanında Türkiye ile ilişkili *Capsicum annuum* kayıtlarını sorgulama.
5. Seçilmiş protein dizilerinden ColabFold Batch girdisi hazırlama.

Bunlar öğrenme ve iş akışı denemeleridir. Anahtar sözcük eşleşmesi, motif bulunması veya otomatik hizalama tek başına bir enzimin işlevini doğrulamaz.

## Bilinen sınırlamalar

- Kullanılan genom UCD10Xv1.1 referansıdır; Samandağ örneğine ait olduğu gösterilmemiştir.
- Notebook’un önceden kaydedilmiş çıktısında Türkiye sorgusundan gelen `WZN32304.1` kaydı Rubisco büyük alt birimi olarak açıklanır. Bu kayıt kapsaisin biyosentez enzimi değildir; Samandağ’a özgü kapsaisin bulgusu olarak yorumlanmamalıdır.
- Önceki sürümde “Pun1 benzerliği (%)” adıyla verilen değerler gerçek yüzde dizi özdeşliği olarak doğrulanmış değildir. Bu yüzden doğrulanmış benzerlik sonucu gibi kullanılmamalıdır.
- Notebook’taki aday listeleri, enzim işlevi ve tür/örnek kökeni için deneysel doğrulama yapılmamıştır.
- ColabFold girdisi hazırlamak, yapı tahmini çalıştırıldığı veya yapının doğrulandığı anlamına gelmez.
- NCBI/UniProt kayıtları ve sorgu sonuçları zamanla değişebilir; tekrar çalıştırıldığında farklı sonuç alınabilir.

## Çalıştırma

Notebook’u Google Colab veya Jupyter ortamında hücre sırasıyla çalıştırmak üzere tasarlanmıştır. İlk hücreler Colab/Linux komutları kullanır; yerel Windows ortamında doğrudan çalışmayabilir. Genom paketi büyüktür ve indirme/işleme için yeterli disk alanı gerekir.

Gerekli Python paketleri:

```bash
pip install -r requirements.txt
```

Kendi FASTA dizilerinizi denemek için notebook’un son bölümündeki `LOCAL_FASTA_FILE` değişkenini düzenleyebilirsiniz. Farklı FASTA kayıtlarının doğru enzim adıyla eşleştiğini ve dizilerin doğru okuma çerçevesinde olduğunu ayrıca kontrol edin.

## Dosyalar

- `capsaicin_pathway_analysis.ipynb` — keşif amaçlı analiz ve ColabFold girdi hazırlama denemesi
- `requirements.txt` — Python paketleri
- `.gitignore` — geçici ve büyük genom verilerini dışarıda tutan kurallar

## Sonraki adımlar

Bu prototipi bilimsel bir analize dönüştürmek istenirse önce örnek kökeni ve veri erişim numaraları belgelenmeli; hizalama ölçütü gerçek yüzde özdeşlik olarak hesaplanmalı; adayların biyolojik anotasyonları kaynaklarla doğrulanmalı; ara ve nihai çıktılar yeniden üretilebilir biçimde sunulmalıdır.
