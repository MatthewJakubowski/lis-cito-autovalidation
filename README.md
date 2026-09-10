# 🔬 LIS CITO Autovalidation Suite (XAI Glass-Box)
### Explainable AI & Human-in-the-Loop STAT Laboratory Decision Engine

[![Live Demo](https://img.shields.io/badge/Live_Simulator-GitHub_Pages-0ea5e9?style=for-the-badge&logo=github)](https://MatthewJakubowski.github.io/lis-cito-autovalidation/)
[![License: MIT](https://img.shields.io/badge/License-MIT-emerald.svg?style=for-the-badge)](LICENSE)
[![Compliance](https://img.shields.io/badge/Compliance-ISO_15189_%7C_EU_AI_Act-indigo.svg?style=for-the-badge)](#-compliance-by-design)
[![Cases](https://img.shields.io/badge/STAT_Cases-250_Validated_Scenarios-amber.svg?style=for-the-badge)](#-baza-scenariuszy-cito)

> **Interaktywny symulator konsoli Laboratory Information System (LIS) pracujący w reżimie ostrego dyżuru medycznego (CITO / STAT).**  
> Projekt demonstruje deterministyczną, 5-stopniową kaskadę walidacji wyników laboratoryjnych opartą na architekturze **Explainable AI (XAI Glass-Box)** oraz paradygmacie **Human-in-the-Loop (HITL)**, eliminując zjawisko niebezpiecznych "czarnych skrzynek" w medycynie stanów nagłych.

---

## ⚡ Live Demo
Wypróbuj symulator bezpośrednio w przeglądarce (Zero-Backend, 100% Client-Side Execution):  
👉 **[https://MatthewJakubowski.github.io/lis-cito-autovalidation/](https://MatthewJakubowski.github.io/lis-cito-autovalidation/)**

---

## 🏛️ Architektura Kaskady Walidacyjnej (L1–L5)

Aplikacja symuluje rzeczywiste obciążenie dyżurowe analityka medycznego pod presją czasu (TAT Timer), weryfikując każdą próbkę przez 5 poziomów kontroli:

| Poziom | Moduł Walidacji | Mechanizm i Reguła Diagnostyczna | Działanie Systemu |
|:---:|:---|:---|:---|
| **L1** | **SQC & Westgard Rules** | Weryfikacja stabilności analitycznej serii pomiarowej ($1_{3s}, 2_{2s}, R_{4s}, 10_x$). | Blokada wydania wyników z serii dotkniętej błędem losowym lub systematycznym. |
| **L2** | **Indeksy HIL** | Spektrofotometryczna ocena interferencji hemolizy ($H$), żółtaczki ($I$) oraz lipemii ($L$). | Wstrzymanie analitów wrażliwych na uwolnienie hemoglobiny wewnątrzkomórkowej lub zmętnienie próbki. |
| **L3** | **Panic Values (CITO)** | Wykrycie stężeń bezpośredniego zagrożenia życia (np. $K^+ < 2.5$ lub $> 6.5\text{ mmol/l}$, troponina, glukotoksyczność). | Zatrzymanie cichej autowalidacji, alarm dźwiękowo-wizualny, wymuszenie protokołu telefonicznego na oddział. |
| **L4** | **Centralny Delta Check** | Kinetyka zmian parametrów pacjenta w oknie czasowym ($\Delta t$). Różnicowanie dynamiki patologii od zamiany probówek. | Wykrycie niefizjologicznych skoków stężeń (np. gwałtowny spadek kreatyniny lub skok aminotransferaz). |
| **L5** | **Korelacja Matrycy Biologicznej** | Spójność fizykochemiczna i fizjologiczna (reguła trzech Hb/Hct, luka anionowa, chelatacja dwuwartościowych kationów przez EDTA). | Detekcja błędów przedanalitycznych (np. pseudohiperkaliemia i hipokalcemia przy skażeniu wersenianem). |

---

## ⚖️ Compliance-by-Design & Ramy Prawne

System od pierwszej linijki kodu został zaprojektowany zgodnie z restrykcyjnymi wytycznymi medycznymi i technologicznymi:

* **Ustawa o medycynie laboratoryjnej (Dz.U. 2022 poz. 2280):** Wyłączną odpowiedzialność prawną i merytoryczną za autoryzację wyniku ponosi uprawniony diagnosta laboratoryjny. AI pełni wyłącznie rolę asystującą (Decision Support System).
* **EU AI Act (Rozporządzenie 2024/1689):** Implementacja wymogów dla systemów wysokiego ryzyka w medycynie:
  * *Art. 14 (Human-in-the-Loop):* Bezwzględny nadzór ludzki nad każdym alertem krytycznym.
  * *Art. 13 (Transparentność i Wyjaśnialność):* Pełna atrybucja cech (Feature Attribution) i jawne uzasadnienie decyzji silnika w oknie audytu.
  * *Art. 12 (Rejestracja Zdarzeń):* Logowanie każdego kroku walidacji.
  * *Art. 2 ust. 6:* Zwolnienie z rygorów certyfikacji systemów dedykowanych wyłącznie do badań i edukacji (R&D Exclusion).
* **PN-EN ISO 15189:2023 Audit Trail:** Każda podjęta decyzja generuje kryptograficzny hash **SHA-256**, znacznik czasu UTC (NTP) oraz kompletny zrzut parametrów gotowy do eksportu JSON lub wydruku karty audytowej.
* **RODO / MDR / IVDR:** Wszystkie rekordy w bazie `cases.json` są w 100% danymi syntetycznymi (Zero Personal Health Data).

---

## 📦 Baza Scenariuszy CITO (`cases.json`)

Sercem silnika jest znormalizowana baza **250 rzeczywistych i syntetycznych scenariuszy ostrego dyżuru**:
* **Klasyki przedanalityki:** Skażenie probówki EDTA solą potasową ($K^+ \uparrow\uparrow$, $Ca^{2+} \downarrow\downarrow$, $Mg^{2+} \downarrow\downarrow$), rozcieńczenie wlewem dożylnym, hemoliza in vitro.
* **Stany nagłe (SOR / OIT):** Ciężka kwasica ketonowa z poszerzoną luką anionową (HAGMA), ostre zespoły wieńcowe (kinetyka hs-cTnI), przełomy tarczycowe, rabdomioliza.
* **Interaktywne Narzędzia Badawcze:**
  * 🔀 **Losowe CITO (Shuffle):** Trening decyzji dyżurowych.
  * 🔍 **Wyszukiwarka wieloparametrowa:** Błyskawiczne filtrowanie analitów, rozpoznań i poziomów kaskady L1–L5.
  * 🎯 **Tryb Dyżuru (STAT Exam):** 10 losowych prób z oceną zgodności z procedurami laboratoryjnymi.

---

## 🛠️ Stack Technologiczny

* **Core:** Vanilla JavaScript (ES6+), HTML5, Web Audio API (akustyczna symulacja analizatorów klinicznych).
* **Styling & UX:** Tailwind CSS (Dark LIS Console Theme), Canvas API (spektrofotometria HIL).
* **Kryptografia:** Web Crypto API (SubtleCrypto SHA-256).
* **Architektura:** Zero-Backend, Client-Side Only (brak transferu danych wrażliwych na zewnętrzne serwery).

---

## 👨‍🔬 Autor & Architektura Systemu

**Mateusz Jakubowski**  
*Starszy Technolog Medyczny | AI & Machine Learning Specialist*  
*15 lat doświadczenia przy aparaturze w laboratoriach diagnostycznych*  

* 🌐 **Portfolio & Web Showcase:** [mateusz-jakubowski.ai.studio](https://mateusz-jakubowski.ai.studio/)
* 💼 **LinkedIn:** [Profil LinkedIn](https://www.linkedin.com/in/mateusz-jakubowski/)
* 🚀 **Inicjatywa:** `#FromPipetteToPython` &bull; `#BuildInPublic`

---

## 📄 Licencja

Projekt udostępniany na zasadach otwartej licencji [MIT](LICENSE) do celów edukacyjnych, badawczych i demonstracyjnych.
