# AGENTS.md

Clon de Asteroids en HTML5 Canvas 2D puro. Cero dependencias, cero build.

## Comandos

- No hay `package.json`: no existen `npm install/test/build`. No los inventes.
- Correr: abrir `index.html` en el navegador, o `npx serve .` → `http://localhost:3000`.
- Verificación rápida de sintaxis: `node --check game.js` (solo JS viejo, sin imports ni módulos).

## Estructura

- `index.html` — solo contiene el `<canvas id="canvas" width="800" height="600">` y `<script src="game.js">`.
- `game.js` — TODO el juego (423 líneas): clases `Bullet`, `Asteroid`, `Ship`, `Particle` + game loop con `requestAnimationFrame`.
- `README.md` — está desactualizado: menciona power-ups y estrella fugaz que fueron **eliminados** (commit `13e713f`). No implementes características basadas en el README; verifica primero en `game.js`.

## Gotchas que importan

- **Input edge-detect**: `keys{}` para teclas sostenidas y `justPressed{}` con `pressed(code)` que consume el flag (game.js:8-24). Espacio dispara **1 bala por pulsación**. Si agregas disparo en `keydown` sostenido romperás el comportamiento; usa `pressed('Space')` dentro de `update()`.
- **Máquina de estados** en `game.js:239-242` y `game.js:294-308`: `'playing'` | `'dead'` | `'gameover'`. Respeta la separación en `update(dt)`.
- **Canvas fijo**: `W = 800`, `H = 600` (game.js:5-6). No redimensiones dinámicamente sin tocar también la lógica de wrapper (`wrap()`, game.js:27).
- **Idioma**: comentarios, HUD (`SCORE`, `NIVEL`) y README en español. Mantén el código nuevo en español.

## Convenciones de estilo

- JS ES6+ plano, sin framework ni bundler. Clases para entidades, cada una con `update(dt)` y `draw()` propios usando `ctx` global.
- Comentarios de sección con la línea `─` como separador (ej. `// ── Input ──...`).
- Mundo toroidal: toda entidad debe llamar `wrap()` en sus bordes.