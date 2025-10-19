# 🌊 Akwarium – Oświetlenie, CO₂, Karmienie i Serwis

![Home Assistant](https://img.shields.io/badge/Home%20Assistant-Blueprint-blue)
![Status](https://img.shields.io/badge/Status-Stable-brightgreen)
![Version](https://img.shields.io/badge/Version-1.0.0-blue)

---

## 💡 Opis

Kompletny **blueprint do automatycznego sterowania akwarium** w Home Assistant.  
Zaprojektowany do precyzyjnego zarządzania oświetleniem, CO₂, filtracją, karmieniem i trybem serwisowym.

- 🌅 **Sterowanie oświetleniem** – do 4 kanałów (Front, Tył, Sun, Grow)
- 🌙 **Rampa rozjaśniania/ściemniania** z płynnym przejściem 1% i zabezpieczeniem przed nakładaniem
- 💨 **Automatyczne sterowanie CO₂** – zgodnie z harmonogramem rampy
- 💧 **Filtracja** – automatycznie sterowana podczas karmienia i serwisu
- 🍽️ **Tryb karmienia** – zatrzymuje filtr na określony czas
- 🔧 **Tryb serwisowy** – zapamiętuje i przywraca stany po zakończeniu
- ⚙️ **Odporność na restart** – kontynuuje rampy po restarcie HA
- 🔔 **Powiadomienia persistent_notification** z emoji

---

## 🧩 Import do Home Assistant

Aby dodać ten blueprint:

1. Otwórz Home Assistant  
2. Przejdź do **Ustawienia → Automatyzacje i Sceny → Blueprints → Importuj blueprint**
3. Wklej poniższy link 👇

📥 **Link do importu:**

https://github.com/GieOeRZet/akwarium/blob/main/blueprints/automation/gieoerzet/akwarium.yaml


4. Kliknij **Załaduj blueprint**

---

## ⚙️ Wymagania

- Home Assistant 2024.8 lub nowszy  
- Zdefiniowane encje:
  - Światła (1–4 kanały)
  - Opcjonalnie: przełączniki CO₂ i Filtr
  - Opcjonalnie: `input_boolean` (Karmienie, Serwis)
  - Opcjonalnie: `timer` (Czas karmienia)
  - Opcjonalnie: `input_text` (Pamięć stanu)

---

## 📘 Autor

👤 **GieOeRZet**  
🔗 [GitHub – Akwarium Blueprint](https://github.com/GieOeRZet/akwarium)  
📅 Wersja: 1.0.0  
🧱 Licencja: MIT

---

💙 Dziękuję za korzystanie z blueprintu!  
Jeśli blueprint Ci się podoba – ⭐ dodaj gwiazdkę na GitHubie!
