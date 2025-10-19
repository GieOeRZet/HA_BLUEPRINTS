# 🌊 Akwarium – Oświetlenie, CO₂ i Karmienie  
**Wersja:** `2025.02.UI1`  
**Autor:** [GieOeRZet](https://github.com/GieOeRZet)  
**Licencja:** [MIT](LICENSE)  
**Kompatybilność:** Home Assistant 2024.12+  
**Repozytorium:** [github.com/GieOeRZet/akwarium](https://github.com/GieOeRZet/akwarium)

---

## 🐠 Opis

Blueprint do pełnej automatyzacji akwarium w **Home Assistant**,  
obsługujący oświetlenie (do 4 kanałów Shelly RGBW2), CO₂, filtr i karmienie.  

✅ Pełna **kompensacja ramp** (rozjaśnianie i ściemnianie) – odporna na restart HA  
✅ Aktualizacja ramp co minutę  
✅ Obsługa karmienia z timerem i automatycznym włączaniem/wyłączaniem filtra  
✅ Automatyczne sterowanie CO₂ względem ramp  
✅ Brak światła nocnego – po zakończeniu ściemniania światła gasną  

---

## 💡 Funkcje

| Funkcja | Opis |
|----------|------|
| 🌅 Rampy rozjaśniania | Płynne zwiększanie jasności od czasu startu rampy do wartości docelowej |
| 🌙 Rampy ściemniania | Płynne wygaszanie świateł do pełnego zgaszenia |
| 🔁 Kompensacja | Po restarcie HA automatycznie oblicza i przywraca właściwą jasność wg czasu dnia |
| 💨 CO₂ | Włączane na czas ramp, wyłączane 30 min przed ściemnianiem |
| 🍽️ Karmienie | Tryb karmienia – wyłącza filtr, uruchamia timer, po czasie przywraca filtr |
| 💧 Filtr | Wyłączany automatycznie przy karmieniu, sterowany automatycznie |
| ⏱️ Aktualizacja | Wszystkie rampy przeliczane co minutę |
| 🩺 Diagnostyka | Powiadomienia o stanie systemu i komponentów |

---

## ⚙️ Sekcje konfiguracyjne

### 💡 OŚWIETLENIE
Blueprint obsługuje 4 kanały oświetlenia – każdy z osobnymi ustawieniami ramp:

| Kanał | Nazwa | Domyślna jasność | Domyślny czas ramp | Opis |
|-------|-------|------------------|--------------------|------|
| 1 | **Front** | 80 % | 30 min | Główne światło przednie |
| 2 | **Back** | 80 % | 30 min | Tylne światło akwarium |
| 3 | **Sun** | 70 % | 30 min | Symulacja promieni słonecznych |
| 4 | **Grow** | 85 % | 30 min | Światło wspomagające wzrost roślin |

Każdy kanał ma pola:
- `Start rozjaśniania` (godzina),
- `Jasność docelowa (%)`,
- `Czas rozjaśniania (min)`,
- `Start ściemniania` (godzina),
- `Czas ściemniania (min)`.

---

### 💨 CO₂
- Przełącznik (switch) zaworu CO₂.  
- Automatycznie uruchamiany przy starcie ramp,  
  wyłączany **30 minut przed ściemnianiem**.

---

### 💧 Filtr
- Przełącznik (switch) zasilania filtra.  
- Wyłączany na czas karmienia,  
  włączany po zakończeniu timera.

---

### 🍽️ Karmienie
| Element | Typ | Opis |
|----------|------|------|
| `feeding_switch` | `input_boolean` | Aktywuje tryb karmienia |
| `feeding_timer` | `timer` | Odmierza czas karmienia |
| `feeding_duration` | `number` | Długość karmienia (minuty) |

- Po włączeniu karmienia: filtr zostaje wyłączony.  
- Po upływie czasu z timera – filtr automatycznie się włącza, a karmienie wyłącza.

---

## 🔁 Tryb pracy

| Sytuacja | Zachowanie |
|-----------|-------------|
| 💡 Start HA | 10 s opóźnienia → kompensacja ramp |
| ⏱️ Co minutę | Aktualizacja jasności wg czasu dnia |
| 🌇 W trakcie rampy | Jasność płynnie wzrasta lub maleje |
| 🌙 Po rampie | Światła gasną |
| 🕒 Restart | System natychmiast dopasowuje poziomy jasności |

---

## 🔧 Instalacja

1. Skopiuj plik `akwarium.yaml` do katalogu:  
/config/blueprints/automation/gieoerzet/

2. W Home Assistant przejdź do  
**Ustawienia → Automatyzacje → Blueprinty → Importuj Blueprint**
3. Wklej link:
https://github.com/GieOeRZet/akwarium/blob/main/blueprints/automation/gieoerzet/akwarium.yaml

4. Zapisz i utwórz nową automatyzację na podstawie blueprintu.
5. Uzupełnij wszystkie pola według swojego sprzętu i harmonogramu.

---

## 🧠 Wskazówki

- Jeśli używasz Shelly RGBW2 – podłącz każdy kanał jako osobną encję `light`.
- Parametry ramp można ustawić różnie dla każdego kanału.
- System automatycznie przeliczy poziom jasności po restarcie HA – nie wymaga ręcznej interwencji.
- Nie stosuj światła nocnego – po zakończeniu rampy światło wyłączy się automatycznie.

---

## 🩺 Diagnostyka

Blueprint generuje powiadomienia:
- przy uruchomieniu HA (`system gotowy`),
- przy rozpoczęciu i zakończeniu karmienia,
- przy zmianach CO₂ (włączenie / wyłączenie),
- w przypadku błędów konfiguracji.

---

## 📘 Dokumentacja i aktualizacje

🔗 Repozytorium:  
[https://github.com/GieOeRZet/akwarium](https://github.com/GieOeRZet/akwarium)

🗓️ Aktualna wersja: `2025.02.UI1`  
💾 Stabilna baza: `2025.02 FINAL`  
📄 Licencja: MIT  

---

## ❤️ Podziękowania

Dziękuję społeczności Home Assistant za inspiracje oraz testy.  
Projekt rozwijany z pasji do akwarystyki i automatyki domowej.

> „Automatyka to nie tylko wygoda – to harmonia w rytmie akwarium.” 🌿
