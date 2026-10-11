# የተረሱ ጀግኖች እና ታሪኮች (Forgotten Heroes and Stories)

An interactive Ethiopian and Sidama cultural heritage Android application built with Kotlin and Jetpack Compose, translating the provided Flutter heritage experience into a native Material 3 Android app enriched with an interactive audio narrator, ambient heritage soundscapes, historical timelines, geographic coordinates, and cultural quizzes.

### User Review & Critical Decisions

> [!IMPORTANT]
> The following product and design choices have been confirmed from your answers and are incorporated into this plan:

- **Confirmed Decision 1 — Interactive Audio Player & Soundscapes**: Instead of a placeholder Snackbar, clicking **«ታሪኩን በድምፅ አዳምጥ»** opens an interactive audio player featuring synthesized traditional Ethiopian heritage soundscapes (such as gentle Masinko/Krar pentatonic melodies and ambient Highland breeze), real-time playback controls (play/pause, seek bar, speed toggle, ambient volume), and a synchronized sentence-by-sentence Amharic narrator transcript with Android Text-to-Speech integration.
- **Confirmed Decision 2 — Historical Timelines, Map Coordinates & Cultural Quizzes**: Each of the three flagship stories (**ለኩ (ለኮ) ከተማ**, **አትሌት ቤለይነህ ዲንሳሞ**, and **ሞቲቴ ፉራ (ንግሥት ፉራ)**) includes an interactive chronological timeline, exact geographic coordinates & regional facts (e.g., Loka Abaya / Leku, Diramo Anferara, Rotterdam, Sidama landmarks), and an interactive Amharic cultural quiz with score tracking.
- **Confirmed Decision 3 — Classic Clean Material 3 Amber & White Visual Style**: Faithful to your original Flutter design (`Colors.amber[800]` top app bar, `Colors.amber[100]` category chips, `Colors.amber[900]` primary action buttons, clean white elevated cards with rounded corners), refined for Jetpack Compose Material 3.

---

### 1. Overview & Core Concept

- **What It Does**: Preserves and showcases overlooked Ethiopian and Sidama historical figures and landmarks in Amharic through rich story cards, detailed historical narratives, interactive timelines, geographic context cards, synchronized audio storytelling with ambient heritage soundscapes, and self-paced cultural knowledge quizzes.
- **Target Audience / Persona**: Amharic readers, students, historians, and cultural enthusiasts exploring the history of Leku (Leko) ancient town, World Marathon record-holder Belayneh Dinsamo from Diramo Anferara, and the legendary Sidama Queen Motite Fura.
- **Key Value**: Transforms a static reading list into an engaging, multi-sensory heritage learning experience while maintaining the clean, familiar Material 3 Amber & White aesthetic of the original design.

---

### 2. User Experience & Visual Design

- **Key User Flows**:
  1. **Home Screen (`የቤት ገጽ`)**: Displays the centered Amber 800 TopAppBar (`የተረሱ ጀግኖች እና ታሪኮች`), a quick category filter bar (`ሁሉም`, `ታሪካዊ ቦታ`, `አትሌት`, `ታሪካዊ መሪ`), a global Cultural Quiz challenge banner, and the vertical list of elevated story cards featuring 180dp top-cropped imagery, bold titles, Amber 100 category chips, and subtitles.
  2. **Story Detail Screen (`የዝርዝር ማሳያ ገጽ`)**: Displays the 250dp hero image, full Amharic title, subtitle, and complete multi-paragraph narrative, followed by interactive tabs/sections for:
     - **ታሪካዊ የጊዜ መስመር (Historical Timeline)**: Expandable chronological milestones for the selected story.
     - **መልክዓ ምድራዊ መረጃ (Map Coordinates & Landmarks)**: Interactive coordinate card showing latitude/longitude, altitude, distance from Addis Ababa/Hawassa, and cultural landmarks (e.g., Anga & Lela memorials for Queen Fura) with an interactive "Open in Maps" action and visual regional locator.
     - **እውቀትዎን ይፈትሹ (Story Quiz & Did You Know Facts)**: Interactive multiple-choice questions in Amharic with immediate feedback and explanations.
  3. **Interactive Audio & Soundscape Player (`ታሪኩን በድምፅ አዳምጥ`)**: Tapping the Amber 900 button launches a dedicated interactive audio player sheet/panel that plays procedural pentatonic Ethiopian ambient soundscapes (`AudioTrack` synthesizer + Android TTS narration), highlights the active Amharic paragraph in real time, and lets the user scrub through sections or toggle ambient sound layers.

- **Visual Identity & Theme**:
  - *Aesthetic Direction*: Classic, clean Material 3 editorial presentation matching the Flutter structure with crisp card elevation, generous reading line-height (`1.6x`), and clear visual hierarchy.
  - *Color Palette & Mood*:
    - Primary App Bar: `#FF8F00` (`Colors.amber[800]`) with `#FFFFFF` foreground text.
    - Primary Action Button: `#FF6F00` (`Colors.amber[900]`) with `#FFFFFF` text/icons.
    - Category Chip & Highlight Surface: `#FFECB3` (`Colors.amber[100]`) with deep amber-brown text (`#3E2723`).
    - Background & Cards: Clean `#FAFAFA` scaffold background with `#FFFFFF` elevated cards (`12.dp` corner radius).
  - *Typography & Hierarchy*: Clean, highly legible Amharic (Ethiopic script) typography using `Noto Sans Ethiopic` / `Noto Serif Ethiopic` paired with clear numeric badges for dates, coordinates, and marathon records (`2:06:50`).
  - *Component Styling & Layout*: Responsive Material 3 `Scaffold`, `Card` with `RoundedCornerShape(12.dp)`, `AssistChip`/`SuggestionChip`, interactive timeline nodes, and a custom waveform visualizer in the audio player.

- **Interactive Feedback & Motion**: Smooth shared-feel transitions between Home and Detail views, animated waveform bars when the heritage audio player is active, spring animations when expanding timeline milestones, and celebratory feedback when answering cultural quiz questions.

---

### 3. Key Product Decisions & Trade-Offs

- **Decision 1 — Self-Contained Synthesized Heritage Audio + Synchronized Transcript**:
  - *Chosen Approach*: Combine Android's native `AudioTrack` real-time pentatonic soundscape generator (producing warm Ethiopian Tizita/Bati scale plucks and ambient drone) with Android `TextToSpeech` and a synchronized visual transcript timer.
  - *Why*: Guarantees 100% offline reliability with zero broken external MP3 links while giving users real audible Ethiopian musical atmosphere and synchronized sentence highlighting even on devices without an Amharic TTS voice installed.
  - *Alternatives Considered*: Streaming external audio URLs (prone to 404s or network delays) or keeping the static Snackbar placeholder.

- **Decision 2 — High-Reliability Visual Assets with Offline Fallback**:
  - *Chosen Approach*: Load the exact Unsplash URLs via Coil (`AsyncImage`) while bundling bespoke high-resolution local drawable illustrations for Leku City, Athlete Belayneh Dinsamo, and Queen Motite Fura as instant placeholders and offline fallbacks.
  - *Why*: Ensures images always appear immediately and crisply even if network connectivity fluctuates in the emulator.

---

### 4. Technical Architecture & Data Strategy *(Technical Reference)*

- **Architecture & Component Diagram**:
```
┌─────────────────────────────────────────────────────────────────────────┐
│                       MainActivity & HeritageApp                        │
│              (Material 3 Amber Theme + Navigation State)                │
└───────────────────────────────────┬─────────────────────────────────────┘
                                    │
                  ┌─────────────────┴─────────────────┐
                  ▼                                   ▼
┌───────────────────────────────────┐ ┌───────────────────────────────────┐
│            HomeScreen             │ │           DetailScreen            │
│ ┌───────────────────────────────┐ │ │ ┌───────────────────────────────┐ │
│ │  Category Filter & Search Bar │ │ │ │ Hero Banner + Full Narrative  │ │
│ └───────────────────────────────┘ │ │ └───────────────────────────────┘ │
│ ┌───────────────────────────────┐ │ │ ┌───────────────────────────────┐ │
│ │   Heritage Story Cards List   │ │ │ │ Interactive Historical        │ │
│ │  (Leku, Belayneh, Queen Fura) │ │ │ │ Timeline & Map Coordinates    │ │
│ └───────────────────────────────┘ │ │ └───────────────────────────────┘ │
│ ┌───────────────────────────────┐ │ │ ┌───────────────────────────────┐ │
│ │  Cultural Quiz Challenge Card │ │ │ │ Audio Player & Transcript     │ │
│ └───────────────────────────────┘ │ │ │ + Story Knowledge Quiz        │ │
└───────────────────────────────────┘ │ └───────────────────────────────┘ │
                                      └─────────────────┬─────────────────┘
                                                        │
                                                        ▼
                                      ┌───────────────────────────────────┐
                                      │   HeritageAudioEngine (Service)   │
                                      │ (Pentatonic Soundscape Synth +    │
                                      │  Synchronized Narrator Tracker)   │
                                      └───────────────────────────────────┘
```

- **Data Model & State**:
  - `HeritageItem`: Contains `id`, `type` (`city`, `athlete`, `queen`), `title`, `subtitle`, `category`, `imageUrl`, `localDrawableRes`, `fullDescription`, `paragraphs` (for synchronized transcript highlighting), `timelineEvents` (year/era, title, detail), `coordinates` (lat, lng, regionName, elevation, distanceInfo, landmarks), and `quizQuestions` (question, options, correctIndex, explanation).
  - `HeritageUiState`: Managed by `HeritageViewModel` using `StateFlow`, tracking the selected story, active category filter, audio playback state (`isPlaying`, `currentParagraphIndex`, `progress`, `ambientSoundEnabled`, `playbackSpeed`), and quiz progress/scores per story.

- **Interactive Component & State Mapping**:
  - **Story Card Tap**: Updates `selectedItem` in `HeritageViewModel` and navigates to `DetailScreen` with full Android system `BackHandler` support.
  - **«ታሪኩን በድምፅ አዳምጥ» Button**: Opens the interactive audio player, starts `HeritageAudioEngine` (synthesizing gentle Ethiopian pentatonic notes and stepping through transcript segments), and allows play/pause, scrubbing, ambient soundscape mode switching (`ክራር / Krar`, `ዋሽንት / Washint`, `ጸጥታ / Voice Only`), and speed adjustment.
  - **Timeline & Coordinate Cards**: Tapping timeline nodes expands historical context; tapping the coordinate card opens an interactive regional map view or launches an external geo intent (`geo:lat,lng`).
  - **Cultural Quiz Component**: Selecting an option validates the answer, highlights correct/incorrect choices in green/amber-red, displays historical explanations in Amharic, and increments the user's cultural mastery score.
