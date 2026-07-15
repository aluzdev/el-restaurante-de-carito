# Design — Taquizas Don Neto

Concepto: **«La taquiza es de noche»**. El sitio vive en la escena real del producto: la fiesta de noche, la plancha bajo focos, la comida brillando contra la oscuridad. Drenched: la superficie ES el color.

## Color (OKLCH, definidos en `src/pages/index.astro`)

| Token | Valor | Uso |
|---|---|---|
| `--noche` | `oklch(0.15 0.03 295)` | Fondo del sitio (violeta-noche) |
| `--noche-2` | `oklch(0.19 0.035 295)` | Sección guisados |
| `--noche-3` | `oklch(0.24 0.04 295)` | Borde del footer |
| `--linea` | `oklch(0.34 0.05 295)` | Reglas del menú |
| `--tinta` | `oklch(0.965 0.008 295)` | Texto principal |
| `--tinta-2` | `oklch(0.82 0.03 295)` | Texto secundario |
| `--jacaranda` | `oklch(0.76 0.11 295)` | Palomitas de la lista incluye |
| `--rosa` | `oklch(0.55 0.23 356)` | Rosa mexicano: sello de precio, números de paso, sección de pago. Tomado de la tarjeta de cobro de la dueña. Texto blanco encima (≥4.5:1). |
| `--rosa-claro` | `oklch(0.81 0.13 356)` | Acentos de texto sobre noche: precio, links, kicker del hero |
| `--verde-wa` | `oklch(0.53 0.15 152)` | SOLO botones de WhatsApp (reconocimiento). Hover: `--verde-wa-2` |

Regla: el verde es exclusivo de WhatsApp. El rosa es la marca. Nada de verde-blanco-rojo ni pergamino beige.

## Tipografía

- **Rótulo (display):** Alfa Slab One — evoca rotulación de mercado. Peso único 400, letter-spacing ≥ 0. H1 hero: `clamp(3.4rem, 12vw, 6rem)`.
- **Texto:** Archivo Variable (Omnibus-Type). Cuerpo 1.0625rem / 1.65.
- Ambas se sirven con `@fontsource` (self-hosted, sin Google Fonts CDN).

## Imágenes (Unsplash, IDs verificados)

- Hero: `photo-1596995804697-27d11d43652e` — trompo al pastor de noche.
- Paquete: `photo-1552332386-f8dd00dc2f85` — tacos de suadero con verdura.
- Pasos: `photo-1591735200387-c29c7d0ec3d3` — mesa con salsas y Sidral Mundet.

## Motion

- Entrada del hero: stagger `sube` 0.9s `cubic-bezier(0.22,1,0.36,1)` + zoom-out lento de la foto.
- Reveals por sección: `.revela` → `.visto` vía IntersectionObserver. **Visibles por defecto sin JS** (gate con `html.js`).
- Guisados: stagger por `transition-delay` en la lista.
- Todo desactivado bajo `prefers-reduced-motion`.

## Componentes / patrones

- `.btn-wa` / `.btn-wa-grande`: pastilla verde WhatsApp, icono SVG inline.
- `.fab-wa`: botón flotante, oculto mientras el hero está en pantalla (con JS).
- `.hero-precio`: sello rosa rotado −1.5° (voz de rótulo).
- `.pago-tarjeta`: panel oscuro translúcido sobre el baño rosa; botón copiar con feedback «¡Copiado! ✓».
- Radios: 14–16px en tarjetas/fotos, pastilla en botones. Sombras cortas (≤18px blur).

## Reglas duras

- Español mexicano únicamente. Sin anglicismos en UI.
- El número de tarjeta se muestra completo por decisión de la dueña (depósito-solo).
- Móvil primero (390px); breakpoints 640/800/900.
- z-index: solo `--z-fab: 40`.
