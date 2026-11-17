# Local LLM Security Mitigation & Guardrails 🛡️
**OWASP Vulnerability Defense (Prompt Injection, Jailbreaking, XSS)**

Proyek ini adalah implementasi sistem keamanan aplikasi berbasis Large Language Model (LLM) yang dijalankan secara lokal. Dibangun menggunakan Flask sebagai *middleware* untuk menangkis berbagai eksploitasi keamanan berdasarkan standar OWASP Top 10 for LLMs.

## 🛠️ Tech Stack & Infrastructure
- **LLM Engine:** Ollama (Local Deployment via Docker)
- **Model:** Qwen 3 (8B)
- **Backend & UI:** Python (Flask), HTML
- **Security Library:** MarkupSafe

## 🚀 4-Layer Security Implementation
Sistem ini menggunakan pendekatan *Defense in Depth* untuk melindungi *secret flag* (data diagnostik) dari eksploitasi AI:
1. **System Prompt Hardening:** Menerapkan instruksi absolut pada AI untuk menolak mode Developer/Root dan melarang pencetakan data sensitif.
2. **Input Guardrails (WAF):** Memfilter input *user* dari kata kunci berbahaya (seperti "abaikan", "root", "flag") sebelum dikirim ke *engine* LLM guna mencegah *Bypass* dan *Prompt Injection*.
3. **Output Guardrails:** Lapis pertahanan terakhir yang mendeteksi dan melakukan *redaction* `[REDACTED]` secara otomatis jika AI mengalami *jailbreak* dan membocorkan data.
4. **Anti-XSS (Cross-Site Scripting):** Memproses *output* AI menggunakan `escape()` untuk menetralisir injeksi *script* HTML/JS berbahaya (Stored XSS).

## ⚙️ Cara Menjalankan Aplikasi Lokal
1. Pastikan Docker dan Ollama sudah berjalan.
2. Pull dan jalankan model lokal: `ollama run qwen3:8b`
3. Install dependensi Python: `pip install -r requirements.txt`
4. Jalankan Flask server: `python app.py`
5. Buka `http://localhost:5000` di *browser*.