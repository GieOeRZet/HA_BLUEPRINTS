# 🧠 GieOeRZet – Kolekcja Blueprintów dla Home Assistant

Zbiór moich blueprintów automatyzacji dla **Home Assistant**.  
Każdy blueprint jest w pełni konfigurowalny z GUI i posiada osobny plik dokumentacji (`*_README.md`).  
Repozytorium zaprojektowane z myślą o przejrzystości, stabilności i rozwoju automatyzacji.

---

## 💡 Dostępne Blueprinty

|  | Nazwa | Opis | Import |
|:--:|:------|:------|:------|
| <img src="https://github.com/GieOeRZet/HA_BLUEPRINTS/raw/main/blueprints/automation/gieoerzet/assets/aquarium_icon.svg" width="42" alt="Akwarium icon"/> | [**🌊 Akwarium – Oświetlenie, CO₂ i Karmienie**](akwarium.yaml)  <br/>[📘 Dokumentacja](akwarium_README.md) | Zaawansowany blueprint do automatyzacji akwarium: rampy świetlne, CO₂, filtr i karmienie.  <br/>W pełni odporna na restart kompensacja ramp. | [Importuj w Home Assistant](https://github.com/GieOeRZet/HA_BLUEPRINTS/blob/main/blueprints/automation/gieoerzet/akwarium.yaml) |
| <img src="https://github.com/GieOeRZet/HA_BLUEPRINTS/raw/main/blueprints/automation/gieoerzet/assets/lights_icon.svg" width="42" alt="Lights icon"/> | [**💡 Podbitka – Automatyczne światła (pełny cykl dobowy)**](swiatla_zewnetrzne.yaml)  <br/>[📘 Dokumentacja](swiatla_zewnetrzne_README.md) | Kompleksowa automatyzacja oświetlenia podbitki i podjazdu.  <br/>Obsługuje tryby: wieczór, poranek, brama, drzwi, święta i blokadę dzienną. | [Importuj w Home Assistant](https://github.com/GieOeRZet/HA_BLUEPRINTS/blob/main/blueprints/automation/gieoerzet/swiatla_zewnetrzne.yaml) |

---

## ⚙️ Jak zainstalować blueprint

1. Skopiuj link z kolumny **Import** (pełny adres `.yaml`).  
2. W Home Assistant przejdź do:  
   **Ustawienia → Automatyzacje i sceny → Blueprinty → Załaduj blueprint z adresu URL**  
3. Wklej link i kliknij **Załaduj**.  
4. Po załadowaniu blueprinta wybierz **Utwórz automatyzację** i uzupełnij parametry.  
5. Zapisz i aktywuj automatyzację.

---

## 📁 Struktura katalogu



## 📁 Struktura katalogu

HA_BLUEPRINTS/
└── blueprints/
    └── automation/
      └── gieoerzet/
        ├── akwarium.yaml
        ├── akwarium_README.md
        ├── swiatla_zewnetrzne.yaml
        ├── swiatla_zewnetrzne_README.md
        └── README.md <-- ten plik (index)


---

## 🧩 Dobre praktyki

✅ Każdy blueprint zawiera `source_url:` wskazujący jego oryginał w tym repo.  
✅ Home Assistant automatycznie pokaże link do źródła w interfejsie.  
✅ Dokumentacje (`*_README.md`) można edytować niezależnie, np. dodając changelog, wersje, czy przykłady automatyzacji.  
✅ Nowe blueprinty dodawaj w tym samym katalogu, a do tabeli powyżej dopisz nowy wiersz.

---

## 👨‍💻 Autor

**GieOeRZet**  
📦 Repozytorium: [github.com/GieOeRZet/HA_BLUEPRINTS](https://github.com/GieOeRZet/HA_BLUEPRINTS)  
💬 Kontakt / pytania: przez [Issues](https://github.com/GieOeRZet/HA_BLUEPRINTS/issues)

---

🟢 _Ostatnia aktualizacja:_ **2025-10-21**
