# Agent guide

This repository contains **The Halls of 7800**, a Java 17, turn-based dungeon game. Use this guide for changes anywhere in the repository. Read `README.md` for setup and architecture, `HOW_TO_PLAY.md` for game behavior, and `FEATURES.md` and `BUGS.md` for the current feature and issue lists.

## Project map

- `src/main/java/edu/towson/cosc442/halls7800/engine`: game session, commands, rules, turns, and events. `GameSession.submit(Command)` is the entry point for player actions.
- `world` and `gen`: map state, visibility, pathfinding, and floor generation.
- `entity`, `combat`, and `effect`: creatures, attacks, and status effects.
- `item`, `quest`, and `progression`: inventory, quests, scoring, and achievements.
- `persist` and `util`: saves, replays, seeded random streams, and supporting utilities.
- `ui` and `app`: JavaFX presentation and application launchers. Keep game rules independent of JavaFX; UI code should read game state and submit commands.
- `src/test/java`: JUnit 5 tests, organized by the same packages as production code. `docs/` is generated Javadoc; `target/` is generated build output.

## Build and verification

Use the Maven Wrapper and JDK 17 or newer. On Windows PowerShell, replace `./mvnw` below with `.\mvnw.cmd`.

```sh
./mvnw test                         # full unit suite and JaCoCo report
./mvnw test -Dtest=ClassName#method # focused test
./mvnw javafx:run                   # launch the game
./mvnw javafx:run -Dseed=42         # launch a reproducible dungeon
```

CI runs `./mvnw -B clean test` on pushes and pull requests. Run focused tests while developing and the full suite before finishing code changes. The build also supports PIT mutation testing and SpotBugs; see `README.md` for those optional commands.

## Change guidelines

- Preserve deterministic runs: the same seed, difficulty, and command sequence must produce the same results. Use the existing `Rng`, `RandomStream`, and `SeedDeriver` patterns for randomness; avoid unseeded random sources in game logic.
- Keep combat and other rules in the model packages. If changing attack behavior, inspect `CombatResolver`, `Combat`, `AttackProfile`, and related tests together.
- Add or update JUnit tests for changed rules and edge cases. Use `ScriptedRng` when a test needs exact random outcomes.
- Follow nearby Java style and package structure. Public APIs generally have Javadoc; document new or changed public behavior.
- Treat replay and save compatibility as part of gameplay changes. Check `persist` and replay tests when changing commands, run records, or state transitions.
- Do not edit generated `target/` output. Regenerate `docs/` only when the task calls for updating API documentation.
