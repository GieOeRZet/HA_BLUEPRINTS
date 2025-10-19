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


🧮 Jak działa logika ramp (obliczanie jasności)

Blueprint korzysta z wbudowanego w Home Assistant silnika Jinja2,
który umożliwia dynamiczne obliczanie proporcji czasu i jasności światła.

🔹 Założenia

Każdy kanał światła ma:

start_time → moment rozpoczęcia rampy rozjaśniania,

ramp_minutes → długość rampy rozjaśniania,

target_pct → maksymalna jasność (np. 80%),

dim_time → moment rozpoczęcia rampy ściemniania,

dim_minutes → długość rampy ściemniania.

W każdej minucie blueprint sprawdza, w jakiej fazie znajduje się oświetlenie,
i oblicza aktualną jasność proporcjonalnie do upływu czasu.

🔹 Wzory obliczeniowe
🟢 Faza rozjaśniania

Jeśli bieżący czas (now_ts) mieści się między start_ts a ramp_end:

elapsed = (now_ts - start_ts) / 60
brightness_pct = (elapsed / ramp_minutes) * target_pct


czyli:

𝑗
𝑎
𝑠
𝑛
𝑜
𝑠
ˊ
𝑐
ˊ
=
𝑐
𝑧
𝑎
𝑠
𝑜
𝑑
_
𝑠
𝑡
𝑎
𝑟
𝑡
𝑢
𝑐
𝑧
𝑎
𝑠
𝑟
𝑎
𝑚
𝑝
𝑦
×
𝑗
𝑎
𝑠
𝑛
𝑜
𝑠
ˊ
𝑐
ˊ
𝑑
𝑜
𝑐
𝑒
𝑙
𝑜
𝑤
𝑎
jasno
s
ˊ
c
ˊ
=
czas
rampy
	​

czas
od_startu
	​

	​

×jasno
s
ˊ
c
ˊ
docelowa
	​


Przykład:
Rozjaśnianie trwa 30 minut, docelowo 80%.
Po 15 minutach:
→ jasność = (15 / 30) × 80 = 40%

🟡 Faza stabilna

Jeśli bieżący czas jest po zakończeniu rampy rozjaśniania, a przed ściemnianiem:

brightness_pct = target_pct


czyli światło świeci na pełnej jasności, aż do momentu dim_time.

🔵 Faza ściemniania

Jeśli bieżący czas (now_ts) mieści się między dim_ts a dim_end:

elapsed_dim = (now_ts - dim_ts) / 60
brightness_pct = target_pct - ((elapsed_dim / dim_minutes) * target_pct)


czyli:

𝑗
𝑎
𝑠
𝑛
𝑜
𝑠
ˊ
𝑐
ˊ
=
𝑗
𝑎
𝑠
𝑛
𝑜
𝑠
ˊ
𝑐
ˊ
𝑑
𝑜
𝑐
𝑒
𝑙
𝑜
𝑤
𝑎
−
(
𝑐
𝑧
𝑎
𝑠
𝑜
𝑑
_
𝑠
ˊ
𝑐
𝑖
𝑒
𝑚
𝑛
𝑖
𝑎
𝑛
𝑖
𝑎
𝑐
𝑧
𝑎
𝑠
𝑠
ˊ
𝑐
𝑖
𝑒
𝑚
𝑛
𝑖
𝑎
𝑛
𝑖
𝑎
)
×
𝑗
𝑎
𝑠
𝑛
𝑜
𝑠
ˊ
𝑐
ˊ
𝑑
𝑜
𝑐
𝑒
𝑙
𝑜
𝑤
𝑎
jasno
s
ˊ
c
ˊ
=jasno
s
ˊ
c
ˊ
docelowa
	​

−(
czas
s
ˊ
ciemniania
	​

czas
od_
s
ˊ
ciemniania
	​

	​

)×jasno
s
ˊ
c
ˊ
docelowa
	​


Przykład:
Ściemnianie trwa 30 minut, start przy 80%.
Po 15 minutach:
→ jasność = 80 - (15/30 × 80) = 40%

⚫ Po zakończeniu rampy

Jeżeli now_ts jest późniejszy niż dim_end (koniec rampy ściemniania),
lub wcześniejszy niż start_time (przed rozpoczęciem dnia):

light.turn_off


czyli światło zostaje całkowicie wyłączone.

🔹 Dodatkowe zabezpieczenia

Wszystkie obliczenia są zaokrąglane i ograniczone do zakresu 0–100:

brightness_pct: "{{ [pct, target_pct]|min }}"   # dla rozjaśniania
brightness_pct: "{{ [pct, 0]|max }}"           # dla ściemniania


Dzięki temu:

jasność nigdy nie przekroczy wartości docelowej,

w fazie ściemniania nie spadnie poniżej zera.

🔹 Cykliczne działanie (time_pattern)

Blueprint posiada wyzwalacz:

- platform: time_pattern
  minutes: "/1"


Dzięki temu co minutę aktualizuje jasność świateł.
To gwarantuje:

płynność rampy (bez „skoków” po restarcie),

kontynuację procesu po ponownym uruchomieniu HA,

aktualizację nawet przy drobnych zmianach czasu systemowego.

🔹 Kompensacja po restarcie

Podczas restartu HA blueprint wykonuje ten sam blok logiki,
ale jednorazowo – natychmiast ustawia właściwą jasność wszystkich świateł
zgodnie z aktualnym czasem, a następnie wchodzi w rytm aktualizacji minutowej.

To pozwala uniknąć sytuacji, w której światło po restarcie świeci niepoprawnie
(np. zbyt jasno lub zbyt ciemno w połowie rampy).

🔹 Schemat przebiegu ramp
Jasność (%)
│
│             _________
│            /         \
│           /           \
│__________/             \__________
│
└───────────────────────────────────────→ czas
   ↑start         ↑dim_time
   Rozjaśnianie   Ściemnianie

🧭 Podsumowanie logiki ramp
Faza	Zakres czasu	Działanie	Przykład jasności (target = 80%)
Przed start_time	< start_time	Wyłączone	0%
Rozjaśnianie	start_time → start_time + ramp_minutes	Narastanie	0–80%
Pełna jasność	po rampie, przed dim_time	Stała wartość	80%
Ściemnianie	dim_time → dim_time + dim_minutes	Opadanie	80–0%
Po dim_end	> dim_time + dim_minutes	Wyłączone	0%

💬 Dzięki temu blueprint w wersji 2025.02 FINAL jest w pełni deterministyczny,
niezależny od restartów i gwarantuje ciągłość stanu oświetlenia w każdej chwili dnia.
