🌊 Akwarium – Oświetlenie, CO₂ i Karmienie

Wersja: 2025.02 (FINAL)
Autor: GieOeRZet
Licencja: MIT
Repozytorium: https://github.com/GieOeRZet/akwarium

🧩 Opis

Kompletny blueprint automatyzujący akwarium w Home Assistant.
Zarządza oświetleniem (4 kanały Shelly RGBW2 lub inne światła), systemem CO₂, filtrem i karmieniem.

Wersja 2025.02 FINAL to w pełni dopracowana edycja z kompensacją ramp,
która wznawia i kontynuuje rampy rozjaśniania oraz ściemniania po restarcie Home Assistant.
Nie wymaga żadnych zewnętrznych skryptów ani integracji.

⚙️ Funkcjonalność
💡 Oświetlenie

Obsługuje do 4 niezależnych kanałów:

Front, Back, Sun, Grow

Każdy kanał ma:

Czas rozpoczęcia rozjaśniania (start_time)

Jasność docelową (target_pct)

Długość rampy rozjaśniania (ramp_minutes)

Czas rozpoczęcia ściemniania (dim_time)

Długość rampy ściemniania (dim_minutes)

Po restarcie HA światła natychmiast ustawiają się na właściwy poziom jasności (kompensacja).

Rampy są kontynuowane co minutę (dzięki time_pattern: "/1").

💨 CO₂

Automatyczne włączenie o najwcześniejszym czasie startu rampy.

Automatyczne wyłączenie 30 minut przed rozpoczęciem ściemniania.

Działa niezależnie od świateł.

💧 Filtr + 🍽️ Karmienie

Po włączeniu przycisku input_boolean (np. input_boolean.aquarium_feed):

Filtr zostaje wyłączony.

Uruchamiany jest timer (timer.aquarium_feed_timer).

Po zakończeniu timera lub ręcznym wyłączeniu karmienia:

Filtr zostaje ponownie włączony.

Timer zostaje zatrzymany / zresetowany.

🩺 Diagnostyka

Wysyła powiadomienie z aktualnymi danymi:
listą świateł, CO₂, filtra i stanu karmienia.

🔄 Wyzwalacze
Typ	Opis
homeassistant start	Kompensacja po restarcie
time_pattern: /1	Aktualizacja ramp co minutę
state – feeding_switch	Obsługa karmienia
event – timer.finished	Koniec karmienia
🔧 Wymagane encje
Typ	Przykładowa encja	Opis
light	light.shelly_rgbw2_channel_1	Kanał Front (obowiązkowy)
light	light.shelly_rgbw2_channel_2	Kanał Back (opcjonalny)
light	light.shelly_rgbw2_channel_3	Kanał Sun (opcjonalny)
light	light.shelly_rgbw2_channel_4	Kanał Grow (opcjonalny)
switch	switch.co2_valve	Zawór CO₂
switch	switch.filter	Filtr wody
input_boolean	input_boolean.aquarium_feed	Tryb karmienia
timer	timer.aquarium_feed_timer	Timer karmienia
🕹️ Konfiguracja – przykładowe wartości
Ustawienie	Front	Back	Sun	Grow
Start rozjaśniania	15:30	15:35	15:40	15:45
Jasność docelowa	80%	80%	70%	85%
Czas rampy	30 min	30 min	30 min	30 min
Start ściemniania	21:30	21:35	21:40	21:45
Czas ściemniania	30 min	30 min	30 min	30 min
🧠 Jak działa kompensacja ramp

Po restarcie Home Assistant blueprint:

Sprawdza bieżący czas (now()).

Porównuje go z harmonogramem ramp (start_time, dim_time).

Oblicza:

ile minut minęło od początku rampy (elapsed),

jaką jasność powinno mieć światło (brightness_pct).

Natychmiast ustawia odpowiednią jasność.

Co minutę przelicza ponownie – kontynuując rampę płynnie po restarcie.

🧩 Tryby pracy ramp
Faza	Działanie
Przed start_time	Światło wyłączone
Podczas rampy rozjaśniania	Jasność rośnie proporcjonalnie do czasu
Między rampami	Światło świeci na pełnej jasności
Podczas rampy ściemniania	Jasność maleje proporcjonalnie do czasu
Po dim_end	Światło wyłączone
🧪 Testowanie

Uruchom automatyzację ręcznie – sprawdź powiadomienie diagnostyczne.

Ustaw czas rampy rozjaśniania na kilka minut i obserwuj światła.

Zrestartuj Home Assistant w trakcie rampy → światła powinny przyjąć właściwą jasność.

Po restarcie rampa powinna kontynuować się płynnie aż do końca.

Sprawdź, że CO₂ i filtr reagują zgodnie z opisem.


