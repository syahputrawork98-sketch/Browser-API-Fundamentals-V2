# Browser API Fundamentals V2

This repository is an architectural reference of the Web Platform and Browser APIs.

It is not a JavaScript tutorial.
It is not a framework guide.

It is a structured, spec-aligned, runtime-aware documentation of how the Web Platform works.

---

## Philosophy

ECMAScript (Language)
↓
JavaScript Engine
↓
Web Platform (HTML, DOM, Fetch, Streams, etc.)
↓
Browser Implementation (Blink, WebKit, Gecko)

This repository focuses on the Web Platform layer.

---

## Structure

The content is divided into Levels:

- L0 — Platform Map
- L1 — Runtime Model
- L2 — Core APIs
- L3 — Performance & Security
- L4 — Advanced
- L5 — Watchlist / Experimental

See `/curriculum/LEVELS.md` for details.

---

## Goal

To understand:

- How scheduling works
- When rendering happens
- How networking is processed
- How security boundaries restrict capabilities
- How concurrency is modeled
- How memory is retained or released
