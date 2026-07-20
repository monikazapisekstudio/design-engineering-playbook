---
created: 2026-07-20
updated: 2026-07-20
version: 1.0
description: Kanoniczna specyfikacja szablonu FigJam Story Map (LLM-ready). Zbudowana na podstawie boardu product-handoff-lab.
---

# FigJam Story Map Template — LLM-ready (Patton methodology)

Szablon kanwy FigJam zgodny z metodyką Jeffa Pattona i zoptymalizowany pod bezbłędne czytanie przez LLM (REST API JSON + Vision). Zbudowany i przetestowany na realnym boardzie `product-handoff-lab` (Symphonia Score — Design System sprzedażowy).

## Struktura kanwy

```
[STORY_MAP]                                    ← root SECTION (wrapper, wymog)
├── [00_SECTION_AI_Readme]                     ← system prompt + legenda
├── [TEMPLATE_META]                            ← attribution block (author, version, license, repo)
├── [USER_SEGMENT_or_PERSONA]                  ← persona + Name + Description (opcjonalny obraz)
├── [01_SECTION_BACKBONE_Activities]           ← backbone L1
│   └── [ACT_01] Activity  ·  [ACT_02] Activity
├── [02_SECTION_BACKBONE_User_Tasks]           ← backbone L2
│   └── [TASK_01] Task  ·  [TASK_02] Task  ·  [TASK_03] Task
├── [03_SECTION_Release_1] Core Value Proof    ← V1 z pełną taksonomią
├── [04_SECTION_Release_2] Business Goal ...    ← V2 czyste
└── [05_SECTION_Release_3] Business Goal ...    ← V3 czyste
```

## Template Metadata — attribution block `[TEMPLATE_META]`

Wstaw jako osobny Section między `[00_SECTION_AI_Readme]` a `[USER_SEGMENT_or_PERSONA]`. Parser go zignoruje (czyta tylko STICKY/SHAPE_WITH_TEXT/CONNECTOR z tagami `[STORY]`/`[ACT]`/`[TASK]` — ten block to zwykły tekst). Czysty separation of concerns: instrukcja dla agenta w `[00]`, attribution człowieka w `[TEMPLATE_META]`, content mapy w pozostałych sekcjach.

### Kanoniczna treść `[TEMPLATE_META]`

```text
Author: Monika Zapisek
Website: monikazapisek.com
Created: 2026-07-20
Last Updated: 2026-07-20
Version: 1.0
Licence: MIT
Skill: github.com/monikazapisekstudio/design-engineering-playbook/tree/main/skills/figjam-storymap-llm

If you use this template, credit appreciated:
"Based on figjam-storymap-llm by Monika Zapisek"

FigJam and Figma are trademarks of Figma, Inc. This template is
independent and not affiliated with, endorsed by, or sponsored by Figma, Inc.
```

### Co musi zawierać `[TEMPLATE_META]`

| Pole | Wartość | Dlaczego |
|---|---|---|
| Author | Imię i nazwisko | Build-in-public credit, social proof — każdy kto duplikuje template widzi autorat |
| Website | URL autora | Profile visits → followers |
| Created | data ISO 8601 (`YYYY-MM-DD`) | Kiedy template powstał — trackowanie używanych wersji |
| Last Updated | data ISO 8601 (`YYYY-MM-DD`) | Bump przy każdej zmianie — użytkownicy wiedzą czy mają świeżą wersję |
| Version | semver (`1.0`, `1.1`, `2.0`) | Wersjonowanie template'u — ważne gdy template jest forkowany/duplikowany |
| Licence | `MIT` (lub inna) | Wyraźne oświadczenie licencji — użytkownicy wiedzą czy mogą duplikować/modyfikować/sprzedawać |
| Skill | pełny URL do folderu skilla w repo | Otwiera landing page folderu (renderowany README) — kieruje do parsera, pełnej procedury, source code |
| Credit appreciated | miękka prośba o cytowanie | Etyczny ask (MIT nie wymaga), buduje authority loop — każdy screenshot z template = darmowa reklama |
| Trademark disclaimer | FigJam/Figma = Figma, Inc. | Defense-in-depth — nominative fair use jest legalne, disclaimer to safety net |

### Czego NIE wstawiać w `[TEMPLATE_META]`

- ❌ Pełny tekst licencji MIT (21 linii — link do repo wystarczy)
- ❌ E-mail kontaktowy (spam risk — masz Website)
- ❌ `© 2026 Monika Zapisek` — MIT LICENSE już to zawiera, nie dubluj
- ❌ `All rights reserved` — MIT jest permissive, "all rights reserved" przeczy licencji
- ❌ Long description skilla — to jest w README repo, nie na kanwie
- ❌ Follow / X handle — opcjonalnie, tylko jeśli masz aktywne konto i chcesz audience

## Kolorystyka (semantyka + deterministyczne dla Vision LLM)

| Sekcja / element | Kolor HEX | Znaczenie |
|---|---|---|
| `[ACT_*]` Activity | `#FFD9E2` / `rgba(255, 217, 226, 0.77)` | Backbone L1 — główny cel użytkownika |
| `[TASK_*]` Task | `#FFE5D2` | Backbone L2 — krok w procedurze |
| `[STORY] [V1]` | `#E6F6C3` (jasny zielony) | Release 1 — MVP / Core Value |
| `[STORY] [V2]` | `#E5F3FE` (jasny niebieski) | Release 2 — Growth |
| `[STORY] [V3]` | `#F3EEFF` (jasny fioletowy) | Release 3 — Scale / Vision |
| Persona (sticky) | `#B3EFBD`, `#B3F4EF`, `#FFD3A8`, `#D3BDFF` | 4 segmenty: Designer / Developer / End-user / AI-agent |
| Connectors (default) | `#D5C2C5` | Przyczynowo-skutkowe |
| Connectors (block) | czerwony | Blokady (A BLOCKS B) |

## Typografia

- **Title (Story Map):** Inter Bold 96px
- **Section header (Activity / Task / Release):** Inter Bold 96px, kolor sekcji
- **Description text:** Inter Medium 40px, kolor sekcji
- **Sticky text:** Inter Medium 16px

## Taksonomia tagów na kartkach

### Story (V1 — pełna)

```text
[STORY] [V1] [P1] User Story sentence @DEV
AC:
- Acceptance criterion 1
- Acceptance criterion 2
```

### Story (V2 / V3 — czyste)

```text
[STORY] [V2] User Story sentence
AC:
- Acceptance criterion 1
```

**Zero `[P*]`, zero `@Owner` w V2/V3** (Lean UX — planowanie odległych hipotez = Big Upfront Design).

### Activity (backbone L1)

```text
[ACT_01] Activity
```

### Task (backbone L2)

```text
[TASK_01] Task
```

## Layout (osi X i Y)

- **Oś X (chronologia):** lewa → prawa. `[ACT_01]` → `[ACT_02]`, wewnątrz activity `[TASK_01]` → `[TASK_02]` → `[TASK_03]`. Każdy task to osobna kolumna.
- **Oś Y (priorytet / release):** góra → dół. Backbone u góry (Activities, potem Tasks), release slice'y pod spodem (V1, V2, V3).
- **Story w release:** kartka `[STORY]` układa się w pionowym słupku pod taskiem do którego należy (algorytm parsera: `center_x` story musi wpaść w range X taska).
- **Odstępy między kolumnami:** 40–60 px w poziomie — daje algorytmowi margines błędu.
- **NIE nakładaj kolumn:** dopóki kartka z jednej kolumny nie wjedzie do połowy szerokości pod sąsiednie zadanie, parser się nie pomyli.

## Connectors

### Kiedy używać

- **Branching (odgałęzienia):** `[STORY_05] --[IF_FAIL]--> [STORY_05B] Ekran błędu`
- **Cross-release dependencies:** `[STORY_12_V2] --[REQUIRES]--> [STORY_03_V1]`
- **Kryteria akceptacji notatki:** (choć preferowane: AC w tej samej kartce co story)

### Kiedy NIE używać

- **Liniowy przepływ chronologiczny** (krok 1 → krok 2 → krok 3). Chronologia kodowana jest w pozycji X + numeracji `[TASK_*]`. 100 strzałek = spaghetti payload.

## `[00_SECTION_AI_Readme]` — instrukcja dla agenta

Wstaw na początku kanwy (najlepiej `x: 0, y: 0` względem roota) sekcję z instrukcją:

```text
==================================================
SYSTEM INSTRUCTIONS FOR AI AGENT (FIGJAM PARSER)
==================================================
PURPOSE:
Ten plik zawiera Story Map (Jeff Patton methodology) dla produktu [PRODUCT NAME].

CANVAS STRUCTURE:
- Sekcje ułożone pionowo (os Y): [01_BACKBONE_Activities] -> [02_BACKBONE_User_Tasks] -> [03_Release_1] -> [04_Release_2] -> [05_Release_3]
- Chronologia kodowana w osi X (task 01 -> task 02 -> task 03)

COLOR SEMANTICS:
- #FFD9E2 = Activity (backbone L1)
- #FFE5D2 = Task (backbone L2)
- #E6F6C3 = Story V1 (MVP, z [P*] i @Owner)
- #E5F3FE = Story V2 (Growth, czyste)
- #F3EEFF = Story V3 (Scale/Vision, czyste)

CONNECTOR RULES:
- A -> B = relacja przyczynowo-skutkowa
- Czerwona krawędź = blokada (A BLOCKS B)

LEAN UX RULES:
- V1: pełna taksonomia ([P1]/[P2]/[P3], @Owner, AC)
- V2/V3: czyste kartki, zero [P*], zero @Owner

OUTPUT EXPECTED:
Markdown backlog: Release -> Activity -> Task -> User Stories (z AC + Owner)
==================================================
```

## Pre-publish checklist (10 min)

Przed opublikowaniem szablonu jako "LLM-ready FigJam Story Map", sprawdź:

- [ ] **Root `[STORY_MAP]`** owija całą kanwę (zero `unsectioned_nodes` w JSON)
- [ ] **`[00_SECTION_AI_Readme]`** istnieje i zawiera legenda + connector rules + expected output
- [ ] **`[TEMPLATE_META]`** istnieje między `[00]` a `[USER_SEGMENT]` — zawiera Author, Created, Last Updated, Version, Licence, Skill URL, credit appreciated, trademark disclaimer
- [ ] **`[01_SECTION_BACKBONE_Activities]`** zawiera tylko `[ACT_*]`
- [ ] **`[02_SECTION_BACKBONE_User_Tasks]`** zawiera tylko `[TASK_*]`, kolumny mają 40–60 px odstępu
- [ ] **`[03_SECTION_Release_1] Core Value Proof`** — kartki `[STORY] [V1]` z `[P1]/[P2]/[P3]`, `@Owner`, AC inline
- [ ] **`[04_SECTION_Release_2]`** i **`[05_SECTION_Release_3]`** — kartki `[STORY] [V2]/[V3]` czyste (zero `[P*]`, zero `@Owner`)
- [ ] **AC inline** — w tej samej kartce co `[STORY]`, po `AC:`
- [ ] **Connectors** tylko do branching / cross-release dependencies
- [ ] **Wewnętrzne nagłówki tekstowe** w każdej sekcji (defense vs `Copy as PNG` ucina nazwy sekcji)
- [ ] **Brak FigJam Stamps / Badges** jako nośniki informacji (prefiksy tekstowe w kartce zamiast)
- [ ] **`Last Updated`** w `[TEMPLATE_META]` zaktualizowane przed publikacją (data dzisiejsza ISO 8601)

## Test parsera (po wypełnieniu szablonu)

```bash
python scripts/figjam_parser.py --file-key {FILE_KEY} --token $FIGMA_TOKEN > story-map.md
```

Sprawdź:

- Każda `[STORY]` ma przypisany `[TASK]` (lub flaga `UNASSIGNED`)
- AC są w tej samej sekcji co story
- V2/V3 są czyste
- Connectory renderują się jako `A --[label]--> B`

## Adnotacje Patellean (z Patton + Lean UX)

- **Release nazewnictwo:** `Core Value Proof`, `Business Goal or Outcome` — outcome, nie "v2 dla v2". Patton zachęca do podawania krótkiego celu biznesowego obok numeru wersji.
- **Priorytety tylko w V1:** pozycja na osi Y w V1 + `[P1]/[P2]/[P3]` wewnątrz release. V2/V3 to hipotezy.
- **Owner tylko w V1:** przypisanie wykonawców do funkcji odległych = noise.
- **Story Map = perspektywa usera, nie wykonawcy.** Activities/Steps opisują co **użytkownik** robi ("Buy Component Package", "Check External Documentation"), nie co zespół buduje ("Build X", "Create Y").
- **Termin "Task" (nie "Step").** Standard Patton dla backbone L2.