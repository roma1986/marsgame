# Mission Architect («Архітектор місії»)

A browser game for the **2026 NASA Space Apps Challenge**, challenge **Space Mission Design Game**. Team: **[team name]**.

- Play: <https://roma1986.github.io/architect-misii/>
- Guided demo (the game plays two missions by itself, with captions): <https://roma1986.github.io/architect-misii/#demo>
- Code and data: <https://github.com/roma1986/architect-misii>
- Demo slides (7 slides, English): [demo/mission-architect-demo.pdf](demo/mission-architect-demo.pdf)
- References and credits: [REFERENCES.md](REFERENCES.md)

> **Language note.** The game interface is currently in Ukrainian. The glossary below maps every screen to English. An English interface is the next step.

## What it is

The player is the chief engineer of a space mission. They choose a target and a launch date, build a spacecraft from components with real prototypes, go through development and testing, fly the mission making decisions, and finally read **why** the mission succeeded or failed.

The main idea: **there is no perfect design, only trade-offs.** A better instrument adds science, but also mass, power, data and cost.

## How to play

1. **Briefing («Брифінг»).** Pick the target (Moon, Mars, asteroid Bennu, Venus or Europa), the mission class (budget) and the science goal. Pick a launch month: launch windows are computed from real orbital periods, and outside the window the rocket carries less.
2. **Builder («Конструктор»).** Choose launch vehicle, platform (orbiter, lander or rover), instruments, power source and antenna. Four live gauges show budget, mass, power and data. The rocket and a cutaway of its fairing are drawn to scale. Launch is blocked while a gauge is red.
3. **Development («Розробка»).** The spacecraft gets heavier than planned, software and instruments are late, reserve money melts. You may drop an instrument, ask for money or wait for the next window. The project can even be cancelled.
4. **Flight.** Step by step simulation. Decisions: landing site, dust storm (sleep or keep working), data priority, solar conjunction, sample collection, a stuck wheel, a units check.
5. **Summary («Підсумок»).** A score out of 100 on three axes (science, budget efficiency, reliability), whether the threshold and baseline missions were met, up to three reasons with the share of science lost, and a comparison with a real mission.

Bonus: **Mars colony («Колонія на Марсі»)** after a successful landing: design an oxygen plant based on the MOXIE experiment.

Two modes: **Cadet** («Курсант», default) and **Engineer** («Режим інженера» in the top bar: trajectory, ion engine, orbit height, ground-antenna time, planetary protection, formulas under each gauge).

## Interface glossary

| Ukrainian | English | Ukrainian | English |
|---|---|---|---|
| Брифінг | Briefing | Бюджет | Budget |
| Конструктор | Builder | Маса | Mass |
| Розробка | Development | Енергія | Power |
| Політ | Flight | Дані | Data |
| Підсумок | Summary | Зв’язок / Антена | Communications / Antenna |
| Демо | Demo (guided walkthrough) | Ракета-носій | Launch vehicle |
| Про дані | About data | Платформа | Platform |
| Режим інженера | Engineer mode | Наукові прилади | Science instruments |
| Звук | Sound | Джерело енергії | Power source |
| Клас місії | Mission class | Клас ризику | Risk class |
| Наукове завдання | Science goal | Резерв | Reserve |
| Дата запуску | Launch date | Випробування | Testing |
| Старт / Запуск | Launch | Пилова буря | Dust storm |
| Сплячий режим | Sleep (safe) mode | Працювати далі | Keep working |
| Сонячне з’єднання | Solar conjunction | Це сталося насправді | This really happened |
| Базова місія | Baseline mission | Порогова місія | Threshold mission |
| Загальна оцінка | Overall score | Колонія на Марсі | Mars colony |
| Детальніше (magnifier) | Details | Далі | Next |

## Realism and data

- Propellant by the **Tsiolkovsky rocket equation**; solar power and radio data rate fall with the **inverse square of distance**; launch windows and solar conjunction come from real **orbital periods**; launch-vehicle reliability uses **Laplace's rule** on real launch histories.
- Every instrument, rocket and platform has a real prototype and a source link.
- Numbers come in three kinds, and the game says which is which («Про дані» window): **checked against sources** (about 56 values: NASA, SpaceX, Wikipedia), **approximate**, and **game parameters** (science scores, event probabilities, class budgets).
- A balance test plays 10,000 random missions with the same simulation: about 22% reach the baseline mission in class Discovery, 10% in New Frontiers and 3% in Flagship, and the best designs differ, so there is no single winning build.
- Photographs are from the NASA Image and Video Library. See [REFERENCES.md](REFERENCES.md).

## Run locally

```
python -m http.server 8000      # open http://localhost:8000
npm install
npm run verify                  # data, texts, code and demo checks
npm run balance                 # 10,000 random missions
npm run build:single            # one-file version in dist/
```

Plain HTML, CSS and JavaScript, no server and no runtime libraries. New instruments, rockets and events are added as data in `data/*.json`; a new target with its own rules also needs code (for example Venus clouds, Europa radiation and asteroid sampling were added in `js/calc.js` and `js/sim.js`).

## Use of AI

We used an AI assistant, **Claude (Anthropic)**.

- **The idea of the game and the scenario are ours.**
- **The assistant wrote the program code**, drafted most on-screen texts and documents, and helped check data and run automated tests. We directed its work and reviewed the results.
- **The assistant also suggested some mechanics** (for example the development-and-testing stage, risk classes, launch windows, engineer mode). We reviewed them and chose to accept them.
- Code and data files are therefore AI-generated or AI-assisted. This is stated here, in [REFERENCES.md](REFERENCES.md), in the `<meta>` tags of the HTML pages, in `package.json` and in the game's «Про дані» window.
- **Images:** planets, rockets, spacecraft, icons and the mission emblem are vector drawings produced by program code. No image or video generation model was used. Photographs are NASA's. We did not use NASA logos or other NASA branding.

## Limitations and what is not implemented

- Interface is Ukrainian only (English interface planned).
- Team play for up to four players, online multiplayer and a sandbox mode are not implemented.
- Orbits are simplified to circles; real trajectories are not computed. Only two orbit options exist (standard, low), in Engineer mode.
- Mission lifetime and individual subsystems (computer, attitude control) are not player choices.
- Some numbers are estimates, some "This really happened" cards were not checked in detail, and a few NASA photos were chosen poorly (for example Mars and Moon on the briefing screen).
- The leaderboard is stored only in one browser.
- Mobile layout was checked less than desktop.
