# 💡 Podbitka – Automatyczne światła (pełny cykl dobowy)

### 📘 Opis

Kompleksowy blueprint automatyzacji oświetlenia zewnętrznego (podbitka + podjazd),
obejmujący pełny cykl dobowy oraz reakcje na otwarcie bramy i drzwi.  
Zawiera tryb **Święta**, który dezaktywuje automatyzację podbitki oraz blokadę dzienną.

📄 **Plik źródłowy:**  
[https://github.com/GieOeRZet/HA_BLUEPRINTS/blob/main/blueprints/automation/gieoerzet/swiatla_zewnetrzne.yaml](https://github.com/GieOeRZet/HA_BLUEPRINTS/blob/main/blueprints/automation/gieoerzet/swiatla_zewnetrzne.yaml)

---

## 🧭 Logika działania

| Tryb | Aktywacja | Działanie | Koniec |
|------|------------|------------|--------|
| Podbitka wieczorem | `from: daylight` | Zapala rogi + środki | Środki: `22:00`, Rogi: `22:30` |
| Podbitka rano | `from: nightlight` (jeśli <6:00) lub `06:00` | Zapala rogi + środki | Przy `from: dawnlight` |
| Podjazd po bramie | Otwarta brama | Zapala podjazd | Po X minutach |
| Podbitka po bramie | jw., +30s | Zapala podbitkę | Po X minutach |
| Podjazd po drzwiach | Otwarte drzwi | Zapala podjazd (z opóźnieniem) | Po X minutach |
| Podbitka po drzwiach | jw. | Zapala podbitkę | Po X minutach |
| Święta | `input_boolean.swieta = on` | Wyłącza podbitkę i jej automaty | Po wyłączeniu przełącznika |
| Blokada dzienna | `from: dawnlight` | Blokuje bramę i drzwi | Do `from: daylight` |

---

## ⚙️ Parametry w GUI

| Parametr | Typ | Opis |
|-----------|-----|------|
| czujnik_dnia | sensor | np. sensor.period_of_day |
| podbitka_rogi | light | światła rogowe |
| podbitka_srodki | light | światła środkowe |
| podjazd | light | światła podjazdu |
| brama | cover | brama wjazdowa |
| drzwi | binary_sensor | czujnik drzwi |
| swieta | input_boolean | wyłącza tryby podbitki |
| godzina_podbitka_srodki_off | time | godzina wyłączenia środków |
| godzina_podbitka_rogi_off | time | godzina wyłączenia rogów |
| godzina_podbitka_rano | time | aktywacja poranna |
| czas_swiecenia_podbitki | number | minuty świecenia podbitki |
| czas_swiecenia_podjazdu | number | minuty świecenia podjazdu |

---

## 📦 Instalacja

1. Skopiuj YAML do:
config/blueprints/automation/gieoerzet/

2. W Home Assistant → **Ustawienia → Automatyzacje → Blueprinty → Załaduj blueprint z pliku**.
3. Wybierz 💡 *Podbitka – Automatyczne światła (pełny cykl dobowy)*.
4. Uzupełnij wszystkie parametry i zapisz.
