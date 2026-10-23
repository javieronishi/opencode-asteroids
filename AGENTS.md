# Repository guide

## Run and verify

- This is a dependency-free HTML5 Canvas game: open `index.html` directly, or run `npx serve .` and use `http://localhost:3000`.
- There is no configured test, lint, build, or typecheck suite. For a focused JavaScript syntax check, run `node --check game.js`; manually exercise gameplay changes in a browser.

## Structure and gameplay flow

- `index.html` is the sole page and loads `game.js` directly; do not assume a bundler, module system, or package manifest.
- `game.js` contains all game state, entities, update/collision logic, rendering, and the `requestAnimationFrame` loop. Keep gameplay changes self-contained there unless the page shell itself must change.
- Canvas coordinates are fixed at `800 × 600` (`W`/`H`), and movement wraps with `wrap(...)`; new moving entities should follow that convention when appropriate.
- Entities use `dead` flags and are removed by array filtering in `update()`. Ensure time-limited entities are filtered in both normal play and the `dead`-state update path when they continue updating there.
