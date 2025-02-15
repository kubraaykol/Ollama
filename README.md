# Ollama
Yapay zeka modellerinin yerel ortamda çalıştırılmasına yarayan özgür yazılım.
<br>

![OLLAMA](./ollama.png)

<br>

Ollama, yerel olarak çalışan yapay zeka modellerini kolayca indirip çalıştırmanı sağlayan bir araçtır. Büyük dil modellerini (LLM - Large Language Models) ve diğer AI modellerini bilgisayarında çalıştırmana olanak tanır. Özellikle, geliştiricilerin kendi cihazlarında AI tabanlı uygulamalar geliştirmesini ve test etmesini kolaylaştırır.

## OLLAMA'nın Temel Özellikleri

**Yerel Çalışma:** Modelleri kendi bilgisayarında çalıştırabilirsin böylece bulut servislerine bağımlı kalmazsınız.

**Kolay Kurulum:** Terminal üzerinden basit komutlarla modelleri yükleyebilir ve çalıştırabilirsin.

**Optimize Edilmiş Performans:** GPU ve CPU destekleri sayesinde donanımına uygun şekilde optimize edilir.

**Geliştirici Dostu:** API desteği sayesinde Python veya diğer dillerle entegre edilebilir.

## Nasıl Kullanılır?

Kurulum için terminalde komutlar aşağıdaki gibidir:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```
 Çalıştılaracak model için:

```bash
ollama run mistral
```

Mistral, popüler ve güçlü açık kaynaklı bir dil modelidir. Ollama, farklı modelleri çalıştırmak için bir API ve CLI (komut satırı arayüzü) sunar. 

Performans ve Verimlilik açısından Mistral 7B, düşük kaynak tüketimiyle güçlü sonuçlar verebilen bir modeldir.

Ollama ile Entegre Çalışması ile Ollama, Mistral gibi açık kaynaklı modelleri doğrudan destekler bu yüzden de kullanımı yaygındır.

#### Desteklediği diğer modeller
Llama 2, Gemma gibi büyük dil modelleri
Code Llama gibi kodlama destekli modeller
Stable Diffusion gibi görsel üretim modelleri

### OLLAMA'nın Mimarisi ve Çalışma Prensibi

Ollama, yerel yapay zeka modellerini optimize eden bir runtime (çalışma zamanı) sunar. Temel olarak şu bileşenlerden oluşur:

**CLI (Command Line Interface)Terminal** üzerinden çalıştırabileceğin arayüz.

**Ollama Daemon:** Modelleri yöneten ve çalıştıran arka plan servisi.

**Modeller (LLM):** Önceden eğitilmiş veya özel olarak eğitilmiş büyük dil modelleri .

Ollama, **GGUF (GPTQ, GGML)** formatındaki modellere odaklanır, yani düşük RAM tüketimi ile CPU/GPU üzerinde optimize çalışabilir.

## OLLAMA Modellerini Kullanma 

Ollama'nın ana komutları Şunlardır:

**Bir modeli çalıştırma:**

```bash
ollama run mistral
```
Bu komut, Mistral modelini indirip çalıştırır ve etkileşimli bir ortam sunar.

**Model indirme ve listeleme:**
```bash
ollama pull llama2
ollama list
```
Bu komut Llama 2 modelini indirir ve yüklü modelleri listeler.

**Modeli API olarak kullanma:**
Ollama, REST API ile entegrasyonu destekler. 
Bknz:Bir modeli HTTP API olarak kullanmak için:

```bash
curl http://localhost:11434/api/generate -d '{
  "model": "mistral",
  "prompt": "Merhaba,bugün hava nasıl?"
  "stream": false
}'
```
CEVAP:

```json
{
  "model": "mistral",
  "response": "Bugün hava durumu değişken görünüyor."
}
```
*Model Listesi:*
```bash
curl http://localhost:11434/api/tags
```
*Dönen Cevap:*
```json
{
  "models": ["mistral", "llama2"]
}
```
*Model Yükleme & Yönetimi:*
```bash
ollama pull gemma
ollama list
ollama create my-model -f Modfile

```

Bu istek (request) Ollama sunucusu üzerinden Mistral modelini çalıştırıp cevap almayı sağlar.

## OLLAMA Modellerini Özelleştirme
Ollama, özel modeller oluşturmayı da destekler. *Modfile* adlı yapı ile kendi modellerini optimize edilebilir.

Örnek bir **Modfile:**
```sql

FROM mistral  
SYSTEM "Sen resmi ve bilgilendirici bir asistansın."  
PARAMETER temperature 0.7  

```
Bu dosya, **Mistral** modelini baz alarak belirli parametrelerle özelleştirir.

**Özel model oluşturma:**
```bash
ollama create my-custom-model -f Modfile
```
Bu komut ile *my-custom-model* adında özel bir model oluşturur.

## OLLAMA GPU Desteği ve Performans Ayarları
Ollama, CPU ve GPU’yu otomatik algılayarak çalışır. GPU kullanımı için:
```bash
OLLAMA_DEVICE=cuda ollama run llama2
```
Bu komut ile  NVIDIA CUDA destekli bir GPU varsa modeli GPU’da çalıştırır.
**GPU hızlandırmasını destekleyen arka uçlar:**

- CUDA (NVIDIA) 
- Metal (Apple M1/M2)
- ROCm (AMD GPU’lar)

## GGUF ve Model Optimizasyonu
Ollama, GGUF (GPTQ-for-GGML Unified Format) model formatını kullanır. Bu format, özellikle düşük bellek tüketimi için optimize edilmiştir.

**Avantajları**
- Küçük dosya boyutlarıyla yüksek performans
- CPU ve GPU desteği (CUDA, ROCm, Metal)
- Llama, Mistral, Falcon gibi modellerle uyumlu

## OLLAMA ile Entegrasyonlar

**Python ile kullanma:**
```python
import ollama
response = ollama.chat(model='mistral', messages=[{"role": "user", "content": "Merhaba!"}])
print(response['message'])
```
**Docker içinde çalıştırma:**
```bash
docker run -p 11434:11434 ollama/ollama
```
Bu, Ollama’yı bir HTTP API olarak sunar.

Docker volume ile veri kalıcılığı eklemek için:
```bash
docker run -v $HOME/.ollama:/root/.ollama -p 11434:11434 ollama/ollama

```
<br>

![DOCKEROLLAMA](./dockerollama.png)
<br>