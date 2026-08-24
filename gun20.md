# Staj Günlüğü - 31 Temmuz 2026

## Issue Araştırması ve Karar Süreci
**Issue Konusu:** Backend ve frontend servislerinin tek bir çatı altında birleştirilmesi mi yoksa ayrı tutulması mı gerektiğinin araştırılması ve sonuçların raporlanması.

### Araştırma Başlıkları ve Kriterler
- **Yönetim ve Dağıtım (Deployment):** Günlük yönetim ve deploy süreçleri açısından hangi yaklaşım daha avantajlı?
- **Hugging Face Uyumluluğu:** İlerleyen aşamalarda Hugging Face üzerinde deploy ederken hangi model daha uygun?
- **Konfigürasyon Gereksinimleri:** Frontend'in derleme zamanında (`build-time`) sabitlenen API adresi ve backend'in CORS ayarları.
- **Hugging Face Ücretsiz Katman Limitleri:** Static Space ile Docker Space arasındaki farklar, inaktivite ve "uykuya dalma" (`sleep`) durumları.
- **Alternatifler:** Cloudflare Pages seçeneğinin değerlendirilmesi.

### Araştırma Sonucu ve Öneri (TL;DR)
- **Frontend ve Backend ayrı tutulmalıdır.**
  - **Frontend:** Hugging Face *Static Space* (veya alternatif olarak Cloudflare Pages)
  - **Backend:** Hugging Face *Docker Space*
- **Gerekçe:** Ayrı tutulması lifecycle (yaşam döngüsü) yönetimini kolaylaştırır, Hugging Face SDK yapısıyla tam uyum sağlar ve platform mimarisine doğal bir şekilde oturur. Konfigürasyon maliyeti ise sadece `VITE_API_URL` (build-time) ve FastAPI CORS ayarlarından ibarettir.