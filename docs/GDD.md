# Pipeline Rush — Game Design Document

> Versión 0.1 · 19 oct 2026 · Repo: `ai-kart-racer`
> Kart racer arcade **original**, hecho con agentes de IA y desplegado con prácticas DevOps.

---

## 1. Pitch

Un kart racer arcade donde mascotas originales inspiradas en **conceptos DevOps** compiten por las tuberías de un datacenter. Cada pista es un *pipeline* literal: un sistema de tuberías y alcantarillas por donde fluyen los datos, y donde terminan los deploys fallidos.

## 2. Pilares

1. **Drift + turbo como núcleo.** Derrapar bien es la habilidad principal; todo lo demás es secundario.
2. **Partidas cortas.** Una vuelta de 60-90 s; se juega en el navegador sin instalar nada.
3. **Humor DevOps.** Personajes, pistas y textos llenos de referencias a *conceptos* (deploys, rollbacks, latencia, caché), nunca a marcas.
4. **Hecho con IA, operado con DevOps.** El juego es también una demo de portafolio: CI/CD, IaC, GitOps y observabilidad aplicados.

## 3. Regla de propiedad intelectual

Todo es original. **No** se usan logos, mascotas ni nombres de productos reales (herramientas, empresas o videojuegos). Los personajes representan **conceptos**, no marcas. Assets externos solo con licencia **CC0**, registrados en `CREDITS.md`.

## 4. Ambientación

**El Subsuelo:** la red de tuberías bajo un datacenter gigante. Agua, cables, luces de status y basura digital.

- **Pista 1 — "El Colector"** (v0.1): alcantarilla principal. Curvas amplias para aprender a derrapar, un tramo de tubería cerrada y una rampa de salida.
- Pistas futuras (ideas): Torre de Enfriamiento, Cuarto de Servidores, Cola de Mensajes.

## 5. Personajes

Personajes originales basados en conceptos DevOps. Cada uno tendrá stats distintos a partir del lote 2.

| Personaje | Concepto | Diseño | Estilo de manejo |
|---|---|---|---|
| **Hotfix** ⭐ v0.1 | Arreglo urgente en producción | Salamandra naranja con casco de bombero | Equilibrado, turbo fuerte |
| **Rollback** | Volver a la versión anterior | Armadillo que se enrolla al chocar | Pesado, se recupera rápido de golpes |
| **Latency** | Lentitud de red | Caracol con propulsor trasero | Arranque lento, velocidad máxima alta |
| **Cache** | Guardar para usar rápido | Mapache con mochila llena de cosas | Ventaja con power-ups (lote futuro) |

## 6. Mecánicas (v0.1)

### Manejo
- Acelerar, frenar/reversa y girar.
- Física arcade: agarre alto, sensación de velocidad, sin simulación realista.

### Drift + mini-turbo
- Mantener **drift** en curva carga el turbo en 3 niveles, con colores de *pipeline status*:
  - 🟢 Nivel 1 (≈0.5 s) → turbo corto
  - 🟡 Nivel 2 (≈1.2 s) → turbo medio
  - 🔴 Nivel 3 (≈2.0 s) → turbo largo
- Soltar el drift libera el turbo del nivel alcanzado.
- Chocar contra una pared durante el drift cancela la carga.

### Modo contrarreloj
- 3 vueltas.
- **Checkpoints** invisibles en orden: una vuelta solo cuenta si se pasaron todos, para evitar atajos.
- HUD: vuelta actual, tiempo total, tiempo de vuelta y mejor vuelta.
- **Récord local** guardado en el dispositivo. El leaderboard online llega en F3.

## 7. Controles

| Acción | Teclado | Gamepad |
|---|---|---|
| Acelerar | `W` / `↑` | `RT` / `A` |
| Frenar / reversa | `S` / `↓` | `LT` / `B` |
| Girar | `A` `D` / `←` `→` | Stick izquierdo |
| Drift | `Shift` / `Espacio` | `RB` |
| Pausa | `Esc` | `Start` |

Se definen en el **Input Map** de Godot, nunca con teclas hardcodeadas en el código.

## 8. Cámara

Cámara de persecución en tercera persona, con suavizado (*lerp*). Se abre ligeramente en el turbo para dar sensación de velocidad.

## 9. Dirección de arte

- **Low-poly** colorido, con iluminación simple. Debe correr fluido en WebGL 2.
- Paleta: túneles oscuros (azules y grises) con acentos neón (verde, amarillo y rojo de status).
- **Concept art y texturas:** Gemini (generación de imagen), revisados y curados a mano.
- **Modelos 3D:** assets CC0 low-poly como base, con texturas propias.

## 10. Técnico

| Aspecto | Decisión |
|---|---|
| Engine | Godot 4.7, renderer **Compatibility** (requisito para export web) |
| Lenguaje | GDScript |
| Plataforma v0.1 | Web (HTML5), en desktop |
| Rendimiento objetivo | 60 FPS en navegador desktop |
| Build | Export headless desde CI |
| Deploy | S3 + CloudFront con Terraform (reutiliza el módulo `s3` de F2) |

### Estructura de carpetas

```
ai-kart-racer/
├── docs/          # GDD, ADRs del juego
├── scenes/        # .tscn (kart, pista, UI)
├── scripts/       # .gd
├── assets/
│   ├── models/
│   ├── textures/
│   └── audio/
├── tools/         # agente asset-pipeline (wk7)
└── CREDITS.md     # licencias de assets externos
```

## 11. Flujo de desarrollo con IA

Igual que en el resto del roadmap:
1. **Claude Code** implementa.
2. **Gemini** hace el *cross-model review* del PR.
3. **Santiago** audita, entiende y aprueba.
4. **Claude** documenta.

**Agente propio (wk7):** `asset-pipeline`, que genera texturas o UI con IA, las procesa (tamaño, formato, compresión) y las importa a Godot.

## 12. Fuera de alcance en v0.1

- Rivales controlados por IA
- Power-ups / items
- Multijugador (local u online)
- Más de 1 personaje o 1 pista
- Música y efectos de sonido elaborados (solo placeholders)
- Leaderboard online
- Soporte móvil / táctil

## 13. Roadmap del juego

| Semana | Entregable |
|---|---|
| wk1 | Setup Godot + repo + GDD |
| wk2 | Fundamentos de Godot |
| wk3 | Kart controller + cámara |
| wk4 | Drift + mini-turbo |
| wk5 | Pista greybox "El Colector" + checkpoints + vueltas |
| wk6 | Dirección de arte con IA |
| wk7 | Agente asset-pipeline |
| wk8 | 🎯 **v0.1:** build web jugable + CI + deploy S3 |
| Lote 2+ | Leaderboard FastAPI en K8s (F3), más personajes, pistas, rivales IA, power-ups |

## 14. Criterios de "listo" para v0.1

- [ ] Se puede completar una carrera de 3 vueltas en el navegador.
- [ ] El drift con 3 niveles de turbo funciona y se siente bien.
- [ ] Los checkpoints impiden contar vueltas con atajos.
- [ ] El récord local persiste entre sesiones.
- [ ] 60 FPS estables en un navegador desktop.
- [ ] El pipeline de CI exporta y despliega automáticamente al hacer merge a `master`.
