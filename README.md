# 🌶️ *Capsicum annuum* (Samandağ Biberi) Kapsaisin Biyosentez Yolağı ve Pun1 Enzim Analizi

Bu proje, **NCBI RefSeq** (*Capsicum annuum* `GCF_002878395.1` – UCD10Xv1.1) tam referans genomu üzerinden biberlerde acılık maddesi olan **kapsaisin** ve **dihidrokapsaisin** biyosentezinden sorumlu gen/protein dizilerini izole etmek, **BAHD açiltransferaz (`HXXXD` ve `DFGWG`)** katalitik motifleriyle gerçek **Kapsaisin Sentaz (`Pun1` / `AT3`)** enzimlerini doğrulamak ve **ColabFold / AlphaFold2** ile 3 boyutlu protein yapı tahmini için girdi setleri oluşturmak amacıyla geliştirilmiş uçtan uca bir biyoinformatik iş akışıdır.

---

## 📌 Proje Özeti ve İş Akışı (Pipeline)

1. **Tam Referans Genomun İndirilmesi (NCBI Datasets CLI)**
   * *Capsicum annuum* (`GCF_002878395.1`) referans genomu (~3.1 GB `.fna`), anotasyon (`.gff3`), kodlayan DNA dizileri (`cds_from_genomic.fna` – 79.7 MB) ve protein dizileri (`protein.faa` – 25.3 MB) indirilir.
2. **Kapsaisin Yolağı Aday Dizilerinin Filtrelenmesi**
   * Tam genomdaki protein ve CDS kayıtları taranarak kapsaisin biyosentez yolağıyla ilişkili **993 aday CDS** ve **993 aday protein** dizisi ayıklanır.
3. **Katalitik Motif (`HXXXD` & `DFGWG`) ve Global Sekans Hizalaması ile `Pun1` İzolasyonu**
   * İsim benzerliği nedeniyle gelen `At3g`, `GPAT3`, `LPAT3`, `STAT3` gibi yalancı pozitifler (false positives) elenir.
   * Doğrulanmış aktif *Capsicum annuum* Kapsaisin Sentaz referans proteini (**`AAV66311.1`**, 440 aa) NCBI Entrez üzerinden çekilir.
   * **Uzunluk filtresi (`380–480 aa`)**, **BAHD ailesi katalitik motifleri (`HXXXD` ve `DFGWG`)** ve **`PairwiseAligner` global sekans hizalaması** birleştirilerek gerçek aktif Kapsaisin Sentaz adayları ve 7 çekirdek yolak enzimi izole edilir.
4. **Türkiye / Samandağ Kaynaklı Kayıtların Sorgulanması**
   * NCBI Entrez API ile Türkiye menşeli *Capsicum annuum* kayıtları (`WZN32304.1`) taranır ve FASTA formatında dışa aktarılır.
5. **ColabFold / AlphaFold2 3B Yapı Tahmini Girdi Hazırlığı**
   * Fenilpropanoid ve kapsaisin sentez basamaklarındaki 5 anahtar enzim (`PAL`, `C4H`, `C3H`, `CAOMT`, `CS_AT3`) için nükleotid-protein çevirisi (`translate_cds` – 3 ORF okuma çerçevesi) ve **ColabFold Batch** girdi dosyası (`colabfold_batch_input.csv`) otomatik olarak üretilir.

---

## 🧬 Öne Çıkan Bulgular: Kapsaisin Sentaz (`Pun1`) Adayları

993 aday protein içerisinden hem **`HXXXD`** hem de **`DFGWG`** katalitik motiflerini eksiksiz taşıyan ve kanonik `AAV66311.1` referansıyla en yüksek dizi benzerliğini gösteren aktif açiltransferazlar:

| Protein ID | Uzunluk (aa) | Pun1 Benzerlik (%) | `HXXXD` Motifi | `DFGWG` Motifi | Açıklama |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **`NP_001311698.1`** | 440 | **99.55%** | `HKIGD` (Poz: 169) | `DFGWG` (Poz: 384) | acyltransferase Pun1 [*Capsicum annuum*] |
| **`XP_016560262.2`** | 459 | **80.61%** | `HKIGD` (Poz: 186) | `DFGWG` (Poz: 403) | acyltransferase Pun1 [*Capsicum annuum*] |

---

## 🧪 Hedeflenen Biyosentez Yolağı Enzimleri

| Kısaltma | Enzim Adı | Biyosentez Rolü / UniProt Referansı |
| :--- | :--- | :--- |
| **`Pun1` / `CS_AT3`** | Kapsaisin Sentaz (Açiltransferaz) | Vanililamin ile 8-metil-6-nonenoil-CoA kondenzasyonu (`D2Y3X2` / `AAV66311.1`) |
| **`PAL`** | Fenilalanin Amonyak Liyaz | Fenilpropanoid yolağı başlangıç basamağı (`B5LAW0`) |
| **`C4H`** | Sinamik Asit 4-Hidroksilaz | *p*-Kumarik asit sentezi (`Q9FQY6`) |
| **`C3H`** | *p*-Kumarik Asit 3-Hidroksilaz | Kafeik asit oluşumu (`B5LAT7`) |
| **`CAOMT` / `COMT`** | Kafeik Asit *O*-Metiltransferaz | Ferulik asit dönüşümü (`Q9FQY8`) |
| **`pAMT`** | Vanilin Aminotransferaz | Vanilindan vanililamin sentezi |
| **`KasI` / `FatA` / `BCAT`** | Ketoaçil-ACP Sentaz / Tiyoesteraz / BCAT | Dallı zincirli yağ asidi yolağı enzimleri |

---

## 🚀 Kurulum ve Kullanım

### Gereksinimler
Python 3.9+ ve aşağıdaki kütüphaneler gereklidir:

```bash
pip install -r requirements.txt
```

### Çalıştırma
* [`capsaicin_pathway_analysis.ipynb`](capsaicin_pathway_analysis.ipynb) dosyasını **Google Colab** veya **Jupyter Notebook / JupyterLab** ortamında açarak hücreleri sırasıyla çalıştırabilirsiniz.
* Kendi lokal FASTA dizilerinizi analiz etmek için Notebook'un son bölümündeki `LOCAL_FASTA_FILE` değişkenine dosya yolunuzu tanımlayabilirsiniz.

---

## 📁 Proje Dosya Yapısı

```text
├── capsaicin_pathway_analysis.ipynb   # Ana biyoinformatik analiz ve ColabFold hazırlık notebook'u
├── requirements.txt                   # Python kütüphane bağımlılıkları
├── .gitignore                         # Büyük genomik arşivleri ve geçici dosyaları hariç tutan yapılandırma
└── README.md                          # Proje dokümantasyonu
```
