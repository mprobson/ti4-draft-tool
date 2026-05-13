# TI4 Faction Draft Tools

A collection of single-file web applications for drafting factions in Twilight Imperium Fourth Edition with the Prophecy of Kings expansion and Council Keleres.

## Overview

These tools help groups secretly draft factions for TI4 games. Each player receives 1 random faction from the PoK+Keleres pool and 3 random factions from the remaining pool. The tools ensure secrecy by providing individual player views.

## Project Structure

```
.
├── README.md                    # This file
├── index-00.html                # Version 0: Basic draft tool (reference)
├── index-01.html                # Version 1: Secret links with base64 encoding (reference)
├── index-02.html                # Version 2: Seed-based reproducibility + hashes (reference)
├── index.html                   # Latest index version (symlink/copy of index-02)
│
├── mistral-web/
│   ├── standalone-01.html       # Version 0: Basic drafter (reference)
│   ├── standalone-02.html       # Version 1: Enhanced styling (reference)
│   ├── standalone-03.html       # Version 2: Minified code (reference)
│   └── standalone.html          # Latest standalone version
│
└── perplexity-labs/
    ├── ti4-faction-draft-01.html  # Version 0: Basic secret code system (reference)
    ├── ti4-faction-draft-02.html  # Version 1: Added player names (reference)
    ├── ti4-faction-draft-03-offline.html  # Version 2: Offline hash-based links (reference)
    └── ti4-faction-draft.html     # Latest perplexity-labs version
```

## Versions

### Index Series

Three progressive versions of the main draft tool:

| Version | File | Description |
|---------|------|-------------|
| 00 | `index-00.html` | Initial basic faction draft tool |
| 01 | `index-01.html` | Added secret player links with base64-encoded faction data |
| 02 | `index-02.html` | Added seed-based reproducibility and hash verification for player isolation |

**Current:** `index.html` (based on index-02)

### Standalone Series

Alternative implementation with different UI approach:

| Version | File | Description |
|---------|------|-------------|
| 01 | `standalone-01.html` | Basic faction drafter with shared results, no player isolation, basic CSS |
| 02 | `standalone-02.html` | Enhanced UI styling with improved spacing, shadows, backdrop-filter, transitions |
| 03 | `standalone-03.html` | Production minification - traditional syntax, string concatenation, condensed CSS |

**Current:** `mistral-web/standalone.html` (based on standalone-03)

### Perplexity-Labs Series

Minimalist offline-capable version:

| Version | File | Description |
|---------|------|-------------|
| 01 | `ti4-faction-draft-01.html` | Basic secret code system with player count and shared draft ID |
| 02 | `ti4-faction-draft-02.html` | Added player names input for personalized assignments and minified CSS |
| 03 | `ti4-faction-draft-03-offline.html` | Offline version with URL hash-based secret links for individual player views |

**Current:** `perplexity-labs/ti4-faction-draft.html` (based on ti4-faction-draft-03)

## Usage

### Index Version (Recommended)

1. Open `index.html` in a web browser
2. Select the number of players (3-8)
3. Optionally enter a seed for reproducible drafts (or click "Random")
4. Enter player names
5. Click "Create Secret Draft Links"
6. Copy and share each player's unique URL privately
7. Each player opens their URL to see only their 4 factions

**Features:**
- Base64-encoded faction data in URLs (obscured from casual viewing)
- Seed-based reproducibility for consistent drafts across sessions
- Hash verification to prevent players from viewing each other's factions
- Color-coded faction cards by expansion

### Standalone Version

1. Open `mistral-web/standalone.html` in a web browser
2. Enter number of players
3. Enter player names (one per line)
4. Enter a secret code (shared across all players)
5. Enter or customize the faction list
6. Click "Generate draft"
7. Click "Reveal / hide" to toggle faction visibility
8. Click "Copy visible text" to copy the current view

**Features:**
- Shared secret code for consistent drafts
- Toggle reveal/hide for all factions
- Copy functionality for sharing
- Draft pool display

### Perplexity-Labs Version

1. Open `perplexity-labs/ti4-faction-draft.html` in a web browser
2. Enter number of players
3. Enter your name (host)
4. Enter player names (one per line)
5. Enter a secret seed (shared across all players)
6. Click "Generate draft"
7. Click "Copy my secret link" to get a per-player URL with hash fragment
8. Each player opens their unique URL to see only their hand

**Features:**
- Completely offline - uses URL hash fragments
- Per-player secret links (`#player=N`)
- Individual player views
- All players see the same draft from the shared seed
- Draft pool display

## Faction Pools

All versions use the official Twilight Imperium Fourth Edition factions:

**Base Game (17 factions):**
- The Arborec
- The Barony of Letnev
- The Clan of Saar
- The Embers of Muaat
- The Emirates of Hacan
- The Federation of Sol
- The Ghosts of Creuss
- The L1Z1X Mindnet
- The Mentak Coalition
- The Naalu Collective
- The Nekro Virus
- Sardakk N'orr
- The Universities of Jol-Nar
- The Winnu
- The Xxcha Kingdom
- The Yin Brotherhood
- The Yssaril Tribes

**Prophecy of Kings (7 factions):**
- The Argent Flight
- The Empyrean
- The Mahact Gene-Sorcerers
- The Naaz-Rokha Alliance
- The Nomad
- The Titans of Ul
- The Vuil'Raith Cabal

**Codex III (1 faction):**
- The Council Keleres

## Draft Logic

Each player receives:
- 1 random faction from the PoK + Keleres pool (8 total)
- 3 random factions from the remaining pool (base factions + any undealt PoK/Keleres)

The draft ensures:
- Each player gets exactly 4 factions
- No faction is dealt to more than one player
- PoK/Keleres factions are prioritized for the first pick

## Technical Details

### Index Version
- Uses seeded Fisher-Yates shuffle for reproducible randomness
- Base64 encoding for URL obscuration
- Hash-based player verification to prevent cross-player viewing
- Supports 3-8 players (limited by PoK+Keleres pool size)

### Standalone Version
- Uses `mulberry32` PRNG with seed for deterministic shuffling
- Shared draft ID stored in localStorage
- Simple reveal/hide toggle mechanism

### Perplexity-Labs Version
- Uses URL hash fragments for offline state persistence
- `mulberry32` PRNG with seed
- Per-player hash links for individual views
- Works entirely client-side with no server

## Development

### Version History

See `git log` for detailed commit history of each series.

#### Index Series Commits
```
5fc9b5c index-00: Initial version - basic faction draft tool
ec1606f index-01: Add secret player links with base64-encoded faction data
88e1203 index-02: Add seed-based reproducibility and hash verification
```

#### Standalone Series Commits
```
b942477 standalone-01: Initial version - basic faction drafter with shared results display, no player isolation, and basic CSS styling
bdf3f4a standalone-02: Enhanced UI styling - improved spacing, shadows, backdrop-filter blur, smoother transitions, and refined button hover effects
56f82e0 standalone-03: Production minification - converted arrow functions to traditional syntax, replaced template literals with string concatenation, and condensed CSS for deployment
```

#### Perplexity-Labs Series Commits
```
0ba65e6 ti4-faction-draft-01: Initial version - basic secret code system with player count and shared draft ID
b1a7d69 ti4-faction-draft-02: Added player names input for personalized faction assignments and minified CSS
3a4d176 ti4-faction-draft-03: Offline version with URL hash-based secret links for individual player views
```

## Getting Started

Simply open any of the `.html` files in a web browser. No server required.

For the best experience with the most features, use:
- `index.html` - Full-featured with seed reproducibility and hash verification

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is open source and available under the [BSD 2-Clause License](LICENSE).

## Acknowledgments

- Twilight Imperium Fourth Edition by Fantasy Flight Games
- Faction data sourced from the [TI4 Wiki](https://twilight-imperium.fandom.com/wiki/Factions)
- Inspired by the need for fair and secret faction drafting in remote gaming sessions
