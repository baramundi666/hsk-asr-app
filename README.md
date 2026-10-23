# hsk-asr-app

React Native app that is the interface to a speech recognition model for Mandarin Chinese learners, focused on correct tone pronunciation.

- Audio is streamed over an API to a service that runs the model in real time.
- Results (recognised syllables, tones, pronunciation assessment) are shown to the user as they arrive.
- Learning material comes from the official HSK 3.0 standard: characters, words and sentences.

# Progress

## 12.10.2026 – 18.10.2026
- Project conceptualised

## 19.10.2026 – 25.10.2026


# What the model provides

## Practice mode (read aloud)
- The user picks an item: a character, word, sentence or minimal pair, filtered by HSK level.
- The model knows the target text, so it checks *how* it was pronounced.
- Feedback for each syllable:
  - tone said vs tone expected (e.g. 卖 mài: said T3, expected T4);
  - segment errors (wrong initial or final, e.g. zh/z, -n/-ng) and skipped syllables.
- Tone sandhi is handled: 3-3 sandhi, 一 and 不, neutral tones, erhua. A correctly applied sandhi is never flagged.
- Glosses and minimal pairs explain why an error matters (买 mǎi "buy" vs 卖 mài "sell").
- Targeted drills:
  - tone pairs (T2/T3);
  - 3-3 sandhi;
  - 一/不 changes;
  - neutral tone;
  - erhua;
  - minimal pairs (买/卖, 汤/糖, 坐/做).

## Free-speech mode (set HSK level)
- The user sets their HSK level (1–9) and speaks freely about anything. The app may suggest a topic or question, but the model does not use it.
- The model returns two things:
  - **what was probably meant**: up to 5 candidate sentences with confidence scores, recovered even when several syllables in a row are mispronounced (e.g. "tu2 su1 guan2" → 图书馆);
  - **tone feedback** against the accepted candidate, as in practice mode.
- Recognition prefers HSK vocabulary (all levels, with the user's level weighted), but names and brands are still allowed. It never forces HSK words.
- The app decides from the confidence: use the top candidate directly, ask "Did you mean 图书馆?" (showing the top 1–3), or skip tone feedback.

## Model properties
- Designed to run in real time on a laptop CPU; no LLM decides the feedback.
- Trained only on open, commercially licensed data.

# Learning data (HSK 3.0)
- **Words:** 10,969 entries.
  - By level: 1: 506 · 2: 750 · 3: 953 · 4: 972 · 5: 1,059 · 6: 1,123 · 7–9: 5,606.
  - Each entry has: simplified and traditional form, pinyin (tone marks and tone numbers), English meanings, part of speech, radical, frequency rank.
  - Source: complete-hsk-vocabulary, MIT licence.
- **Sentences:** about 59,800 Tatoeba sentences, graded by the HSK level of their vocabulary (CC-BY 2.0 FR).
  - Each sentence comes with canonical, sandhi (surface) and allowed pinyin.
- **Prompt sets:**
  - 152 read-aloud prompts (HSK-graded Tatoeba sentences plus targeted sandhi, 一/不, neutral-tone, erhua and minimal-pair items);
  - 61 targeted drills;
  - 30 optional conversation starters (topic suggestions for free speech; not used by the model).

# Functionalities

## Required
- Expo project with TypeScript and React Navigation, running on Android and iOS.
- Audio recording with real-time access to frames, and microphone permissions on both platforms.
- Local SQLite database of HSK 3.0 material: characters, words and sentences with pinyin, tones and translations.
- Material browser: search by character, pinyin or translation; filter by HSK level.
- Audio streaming over WebSocket while recording, receiving partial and final results.
- Result view:
  - syllables coloured by tone correctness;
  - expected vs recognised tone;
  - an example of correct pronunciation.
- Practice mode: choose an item → record → feedback → next item.
- Free-speech mode: set HSK level → speak → meant sentence + tone feedback.
- Practice history stored locally in SQLite.
- Error and app-lifecycle handling (foreground and background): network loss, reconnecting, …

## Optional
- Visual comparison of reference vs own pronunciation (e.g. pitch contour).
- Statistics of the most frequent tone errors, with charts.
- More advanced test settings.
- HSK database updates.

# Tech stack (TBD)

| Area | Technology |
|---|---|
| App | React Native (Expo), TypeScript |
| Navigation | React Navigation |
| State management | Zustand (?) |
| Audio | react-native-audio-api (16 kHz PCM recording), expo-audio (playback), expo-speech (TTS) |
| Networking | WebSocket (audio streaming), GraphQL (data) |
| Local storage | SQLite (expo-sqlite), expo-file-system |
| UI | FlashList, Reanimated, react-native-skia, expo-haptics |
| Connectivity / app lifecycle | @react-native-community/netinfo, AppState |
| Build | EAS Build |
