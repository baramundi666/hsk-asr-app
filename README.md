# hsk-asr-app

Zrealizowana w React Native aplikacja będącą interfejsem do modelu rozpoznawania mowy wspierającego naukę języka chińskiego, ze szczególnym naciskiem na poprawną wymowę tonów w języku mandaryńskim.

Aplikacja działa na zasadzie strumieniowania audio do serwisu (przez API), w którym w czasie rzeczywistym odbywałaby się inferencja modelu uczenia maszynowego. Wynik - rozpoznane sylaby, tony oraz ocena wymowy - prezentowany użytkownikowi na bieżąco. Dodatkowo aplikacja korzysta z bazy materiałów do nauki: znaków, słów i zdań z zakresu oficjalnego standardu HSK 3.0.

# Progress

## 12.10.2026 - 18.10.2026
- Project conteptualized

## 19.10.2026 - 25.10.2026


# Functionalities

## Required
- Projekt w Expo z TypeScript'em, nawigacja React Navigation, działanie na Androidzie i iOS
- Moduł do nagrywania audio (z dostępem do ramek w czasie rzeczywistym) wraz z obsługą uprawnień do mikrofonu na obu platformach
- Lokalna baza SQLite z materiałami HSK 3.0 (znaki, słowa, zdania z pinyinem, tonami i tłumaczeniem)
- Przeglądanie materiałów z wyszukiwaniem po znaku, pinyinie i tłumaczeniu oraz filtrem poziomu HSK
- Strumieniowanie audio przez WebSocket w trakcie nagrywania z odbiorem wyników częściowych i końcowych
- Prezentacja wyniku: sylaby kolorowane według poprawności tonu, ton oczekiwany vs rozpoznany, przykład poprawnej wymowy
- Tryb ćwiczeń: wybór elementu -> nagranie -> informacja zwrotna -> kolejny element
- Historia ćwiczeń zapisywana lokalnie w SQLite
- Obsługa błędów i cyklu życia włączonej, zminimalizowanej aplikacji: utrata sieci, ponowne łączenie, ...

## Optional
- wizualizacja wzorcowej wymowy v.s. własnego nagrania (częstotliwości np. dźwięku)
- statystyki najczęściej popełnianych błędów tonalnych z wykresami
- bardziej zaawansowane ustawienia testów
- aktualizacje bazy HSK


# Tech stack (TBD)
 
| Area | Technology |
|---|---|
| App | React Native (Expo), TypeScript |
| Navigation | React Navigation |
| State management | Zustand (?) |
| Audio | react-native-audio-api (16 kHz PCM recording), expo-audio (playback), expo-speech (TTS) |
| Networking | WebSocket (audio streaming), graphql (data) |
| Local storage | SQLite (expo-sqlite), expo-file-system |
| UI | FlashList, Reanimated, react-native-skia, expo-haptics |
| Connectivity / app lifecycle | @react-native-community/netinfo, AppState |
| Build | EAS Build |

