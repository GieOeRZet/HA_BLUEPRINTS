# 💡 Akwarium – Automatyzacja światła, CO₂, karmienia i serwisu

Kompletny **blueprint Home Assistant** do inteligentnego sterowania akwarium — w pełni konfigurowalny, bez potrzeby ręcznej edycji YAML.

---

## 📦 Funkcje

✅ **Sterowanie oświetleniem (4 kanały):**  
Każdy kanał (Biały Front, Biały Tył, Sun, Grow) ma:
- Start i koniec oświetlenia (czas)
- Czas rampy rozjaśniania i ściemniania (1–240 min)
- Jasność docelową (%)
- Automatyczne rampy z krokiem co 30 sekund

✅ **Sterowanie CO₂:**  
- Włącza się **z najwcześniejszym startem światła**
- Wyłącza się **30 minut przed ostatnim wygaszeniem**

✅ **Tryb karmienia:**  
- Włącza się przez `input_boolean`  
- Wyłącza filtr na czas karmienia  
- Automatycznie uruchamia `timer`  
- Po zakończeniu przywraca filtr  
- Obsługuje ręczne przerwanie

✅ **Tryb serwisowy:**  
- Wszystkie światła → 90%  
- Filtr i CO₂ → wyłączone  
- Zapisuje stany do `input_text`  
- Po wyłączeniu przywraca poprzedni stan

✅ **Bezpieczne opóźnienie startowe:**  
- Po restarcie Home Assistant → automatyzacja startuje po 10 sekundach

---

## ⚙️ Wymagane helpery (opcjonalne)
| Funkcja | Typ | Opis |
|----------|------|------|
| Tryb karmienia | `input_boolean` | Włączanie trybu karmienia |
| Timer karmienia | `timer` | Odliczanie czasu karmienia |
| Tryb serwisowy | `input_boolean` | Aktywacja trybu serwisowego |
| Bufor stanu | `input_text` | Zapamiętuje stany świateł i urządzeń |

---

## 🧩 Import do Home Assistant

1. Skopiuj poniższy link:
   https://github.com/GieOeRZet/akwarium/blob/main/akwarium.yaml


2. W Home Assistant przejdź do:  
**Ustawienia → Automatyzacje i sceny → Blueprints → Importuj blueprint**

3. Wklej powyższy link i kliknij **Importuj**.

4. W nowej automatyzacji przypisz swoje encje (`light`, `switch`, `input_boolean`, `timer`, `input_text`).

---

## 🕓 Domyślne czasy
| Kanał | Włączenie | Ściemnianie | Jasność |
|--------|------------|--------------|----------|
| Wszystkie | `15:30` | `21:30` | wg ustawienia (70–85%) |

---

## 📜 Autor
👨‍💻 Blueprint przygotowany przez **ChatGPT (GPT-5)** we współpracy z użytkownikiem [GieOeRZet](https://github.com/GieOeRZet)

---

> 💬 Masz pytania lub chcesz dodać nowe funkcje (np. automatyczne karmienie, chłodzenie, mgiełkę)?  
> Otwórz **issue** lub napisz w komentarzu — projekt można łatwo rozszerzyć.
> 
