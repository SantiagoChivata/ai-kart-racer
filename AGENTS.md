# AGENTS.md — Reglas comunes (fuente única de verdad)

## Proyecto
- **Pipeline Rush**: kart racer arcade **original**. Proyecto de estudio personal.
- Engine: **Godot 4.7**, renderer **Compatibility**, lenguaje **GDScript**.
- Fuente de verdad del diseño: `docs/GDD.md`. Si un cambio contradice el GDD, se señala; no se implementa en silencio.
- Alcance v0.1: 1 kart (Hotfix), 1 pista ("El Colector"), contrarreloj con drift + mini-turbo. Nada fuera de ese alcance sin aprobación.

## Propiedad intelectual (no negociable)
- Prohibido usar personajes, mascotas, logos, nombres, pistas, música, sonidos o assets de juegos o marcas de terceros, también "inspirados en" de forma reconocible.
- Solo assets **CC0** o generados para este proyecto. Cada asset externo se registra con fuente y licencia en `assets/CREDITS.md`.

## Estructura (convención, crear a medida que haga falta)
- `scenes/` → `.tscn` · `scripts/` → `.gd` · `assets/` → modelos, texturas, audio · `docs/` → GDD, ADRs, notas.
- Nombres de archivo en `snake_case`.

## Zonas protegidas
- No editar a mano: `.godot/`, `*.import`, `*.uid`. Los genera el editor.
- `project.godot`: solo con justificación explícita en el PR.
- No añadir plugins/addons sin un ADR en `docs/`.

## Estilo GDScript (Godot 4)
- Tipado estático: `var speed: float = 0.0`, `func _ready() -> void:`.
- `snake_case` para variables/funciones, `PascalCase` para `class_name`, señales en pasado (`lap_completed`).
- Sintaxis de Godot 4, nunca de Godot 3 (`@onready`, `@export`, `await`; no `yield`, no `onready var`).
- Física del kart en `_physics_process`, no en `_process`.

## Git
- Un cambio = una rama + PR pequeño. Commits estilo Conventional Commits (`feat:`, `fix:`, `docs:`, `chore:`).
- Nunca commitear secretos, tokens ni rutas personales.

## Idioma
- Documentación en español; términos técnicos en inglés.
