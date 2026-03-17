# UniBot: Yerel LLM Tabanlı Doküman Soru-Cevap Servisi

## Proje Tanımı
UniBot, yerel bir Büyük Dil Modeli (LLM) kullanarak kullanıcı tarafından sisteme yüklenen dokümanlar (PDF, TXT, Markdown) üzerinden içerik analizi yapan ve soruları yanıtlayan bir Doküman Soru-Cevap uygulamasıdır. Proje, temel RAG (Retrieval-Augmented Generation) mimarisi üzerine inşa edilmiştir.

## Projenin Amacı
Bu çalışma, yerel bir LLM üzerinden doküman setleri ile etkileşim kuran bir servis geliştirmek amacıyla tasarlanmıştır. Projenin odak noktası, harici veya ücretli bulut servislerine ihtiyaç duymadan yerel kaynaklarla verimli bir soru-cevap altyapısı oluşturmak ve bu süreci bir REST API üzerinden sunmaktır.

---

# Teknik Mimari ve Kullanılan Teknolojiler

Proje kapsamında kullanılan ana teknolojiler ve tercih edilme nedenleri aşağıda açıklanmıştır.

## Python
Projenin ana geliştirme dili olarak seçilmiştir. Veri işleme ve yapay zeka kütüphaneleri ile geniş uyumluluğu nedeniyle tercih edilmiştir.

## FastAPI
Yüksek performanslı ve asenkron mimarisi sayesinde backend API katmanında kullanılmıştır. Ayrıca otomatik Swagger dokümantasyonu sağlamaktadır.

## Ollama (Yerel LLM)
Veri gizliliğini korumak ve yerel çıkarım (inference) yapabilmek amacıyla kullanılmıştır. Llama 3 veya Mistral gibi modelleri yerel olarak çalıştırmayı sağlar.

## LangChain
Dokümanların parçalara ayrılması (chunking) ve LLM bağlam yönetiminin (context management) sistematik olarak yürütülmesi için kullanılmıştır.

## ChromaDB
Doküman parçalarının vektör temsillerini saklamak ve semantik benzerlik araması (vector search) gerçekleştirmek için tercih edilmiştir.

## Streamlit
API ile uçtan uca etkileşimi görselleştirmek amacıyla minimal bir kullanıcı arayüzü oluşturmak için kullanılmıştır.

---

# Kurulum ve Çalıştırma Adımları

## 1. Yerel LLM Sunucusunun Hazırlanması

Proje, Ollama üzerinden çalışan yerel bir model kullanmaktadır.

1. Ollama uygulamasını sisteminize indirin ve kurun.
2. Terminal üzerinden tercih ettiğiniz modeli çekin:

```bash
ollama pull llama3
```

3. Ollama servisinin arka planda çalıştığından emin olun.

Varsayılan adres:

```
http://localhost:11434
```

---

## 2. Projenin Ayağa Kaldırılması

### Bağımlılıkların Kurulması

```bash
pip install -r requirements.txt
```

### Backend Servisinin Başlatılması

```bash
python app.py
```

### Kullanıcı Arayüzünün Başlatılması (Opsiyonel)

```bash
streamlit run ui.py
```

---

# Klasör Yapısı ve Kod Düzeni

Proje, sürdürülebilirlik ve okunabilirlik prensiplerine uygun olarak modüler şekilde tasarlanmıştır.

## API Katmanı
REST uç noktalarını (endpoints) ve istek yönetimini içerir.

## Doküman İşleme Katmanı
Dokümanların parçalanması, embedding oluşturulması ve vektör veritabanı işlemlerini yönetir.

## LLM Katmanı
Yerel LLM modeli ile iletişimi sağlar ve cevap üretim sürecini yönetir.

## Test Katmanı
Temel fonksiyonların doğruluğunu kontrol eden birim testlerini (unit tests) içerir.