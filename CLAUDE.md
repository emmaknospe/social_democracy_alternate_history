# Social Democracy: Star Wars Mod - Development Guide

## Project Overview
This is a Star Wars-themed modification of "Social Democracy: An Alternate History" - a text-based political simulation game originally set in Weimar Germany. The mod adapts the gameplay to the Star Wars universe, set before the Phantom Menace (around 37 BBY / 7940 C.R.C.).

## Technology Stack
- **Game Engine**: DendryNexus (custom interactive fiction framework)
- **File Format**: `.dry` files (DendryNexus scene format)
- **Frontend**: HTML/CSS/JavaScript with jQuery v1.11.1 and d3.js v7
- **Build System**: Node.js with DendryNexus CLI

## Project Structure
```
social_democracy_alternate_history/
├── source/                    # Game source files
│   ├── info.dry              # Game metadata
│   ├── qdisplays/            # UI display components
│   └── scenes/               # Game scenes and logic
│       ├── advisors/         # Character advisor scenes
│       ├── events/           # Historical events (years 1929-1934)
│       ├── government_affairs/ # Government policy scenes
│       ├── party_affairs/    # Party management scenes
│       ├── main.scene.dry    # Main game loop
│       └── root.scene.dry    # Entry point
├── out/html/                 # Compiled game output
└── package.json              # Node.js configuration
```

## Build Commands
- **Build Game**: `npm run dendrynexus make-html`
- **Install Dependencies**: `npm install`
- **Update DendryNexus**: `npm install --upgrade https://github.com/aucchen/dendrynexus`

## Game Mechanics
- **Time System**: BBY (Before Battle of Yavin) dating, converted to C.R.C. (Coruscant Reckoning Calendar)
  - Current setting: 37 BBY = 7940 C.R.C.
  - Display formula: `7977 - BBY = C.R.C. year`
- **Quarters**: 4 per year (.000, .250, .500, .750)
- **Resources**: Party resource management system
- **Factions**: Internal party faction dynamics
- **Advisors**: Character-based action system with cooldowns

## Key Files to Understand
1. `source/scenes/root.scene.dry` - Game initialization and main menu
2. `source/scenes/main.scene.dry` - Core game loop and hand management
3. `source/scenes/status.scene.dry` - Game state display
4. `source/scenes/events/` - Major story events (need Star Wars conversion)
5. `source/scenes/advisors/` - Character interactions (need Star Wars characters)

## Modding Notes
- The game is already partially converted to Star Wars setting
- Title changed to "Phantom Menace: An Alternate History"
- Time system converted to BBY/C.R.C. dating
- Chancellor Valorum referenced in main.scene.dry
- Original Weimar Germany events (1929-1934) need full Star Wars conversion
- Historical characters in advisors/ need replacement with Star Wars characters

## Development Workflow
1. Edit `.dry` files in source/scenes/
2. Run `npm run dendrynexus make-html` to compile
3. Test in out/html/index.html
4. Check game logic with JavaScript console
5. Verify scene transitions and variable states

## File Format (.dry)
- `title:` - Scene title
- `on-arrival:` - JavaScript code executed when scene loads  
- `view-if:` - Conditions for scene visibility
- `go-to:` - Scene navigation
- `@label` - Scene sections/choices
- `- @choice` - Player choice options
- `[? condition : text ?]` - Conditional text display
- `[+ variable +]` - Variable display

## Variables & State
Key game state variables are stored in Q object:
- Q.year_bby, Q.quarter - Current time
- Q.resources - Party resources
- Q.dissent - Internal party conflict
- Q.yellows_* - Party position variables
- Q.advisor_action_timer - Advisor cooldowns
- Q.separatism - Separatist sentiment (unlocks Loyalist coalition)
- Q.in_*_coalition - Coalition membership flags

## Coalition System
Possible government coalitions:
- **Reform Coalition** (current): Yellows + Nobles + Core Coalition
- **Rim Alliance**: Yellows + Rights and Liberties
- **Defense Coalition**: Core Coalition + Yellows + Militarists
- **Loyalist Coalition**: Core Coalition + Nobles + Yellows + Militarists (requires high separatism)
- **Rim Guardians**: Yellows + Rights and Liberties + Militarists