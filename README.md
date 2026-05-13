# TI4 Faction Draft Tools

A collection of single-file web applications for drafting factions in Twilight Imperium Fourth Edition with the Prophecy of Kings expansion and Council Keleres.

## Overview

These tools help groups secretly draft factions for TI4 games. Each player receives 1 random faction from the PoK+Keleres pool and 3 random factions from the remaining pool. The tools ensure secrecy by providing individual player views.

## Project Structure

```
.
├── README.md                    # This file
├── index.html                   # Latest index version
│
├── mistral-web/
│   └── standalone.html          # Latest standalone version
│
└── perplexity-labs/
    └── ti4-faction-draft.html     # Latest perplexity-labs version
```

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

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is open source and available under the [BSD 2-Clause License](LICENSE).

## Acknowledgments

- Twilight Imperium Fourth Edition by Fantasy Flight Games
- Faction data sourced from the [TI4 Wiki](https://twilight-imperium.fandom.com/wiki/Factions)
