# Baluarte — Crónicas de la Guardia del Norte

[![Deploy to GitHub Pages](https://github.com/alvarodiez20/baluarte/actions/workflows/pages.yml/badge.svg)](https://github.com/alvarodiez20/baluarte/actions/workflows/pages.yml)

Juego de defensa de torres medieval con campaña, progresión permanente y modo infinito.
Todo el juego vive en un único `index.html`: sin dependencias, sin build, sin servidor.

**▶ Jugar: https://alvarodiez20.github.io/baluarte/**

---

## Contenido

- [Características](#características)
- [Cómo jugar](#cómo-jugar)
- [Controles](#controles)
- [Torres y hechizos](#torres-y-hechizos)
- [Ejecutar en local](#ejecutar-en-local)
- [Despliegue](#despliegue)
- [Estructura del proyecto](#estructura-del-proyecto)
- [Modificar el juego](#modificar-el-juego)
- [Compatibilidad](#compatibilidad)

## Características

| | |
|---|---|
| **Campaña** | 10 capítulos con historia — la traición del Canciller Malaquías y el regreso del liche Vhaldrek — con 192 oleadas y un jefe al final de cada capítulo |
| **Torres** | 7 torres, 3 niveles cada una y 2 especializaciones al máximo: 14 ramas de mejora distintas |
| **Enemigos** | 24 unidades entre 14 enemigos y 10 jefes, con armadura, resistencia mágica, vuelo, curación, regeneración e invocaciones |
| **Hechizos** | 3 hechizos con enfriamiento propio |
| **Progresión** | Estrellas por capítulo, moneda de Gloria, 10 mejoras permanentes del reino, 17 logros y bestiario |
| **Dificultades** | Normal, Difícil y Pesadilla (se desbloquea al terminar la campaña) |
| **Asedio infinito** | Modo sin final con oleadas escaladas, también desbloqueable |
| **Guardado** | Automático en `localStorage`, sin cuentas ni servidor |

## Cómo jugar

Los enemigos recorren el camino desde la entrada hasta tu baluarte. Cada uno que llegue te
cuesta una vida; si se agotan, el capítulo termina. Construyes torres sobre el terreno libre
para detenerlos, y el oro que sueltan financia más torres y mejoras.

Adelantar una oleada con `Espacio` antes de que salga sola concede oro extra, así que el ritmo
lo marcas tú: consolidar defensas o arriesgar por economía.

## Controles

| Tecla | Acción |
|---|---|
| `1` – `7` | Seleccionar torre |
| Clic | Construir (mantén `Shift` para construir varias seguidas) |
| `Q` `W` `E` | Lanzar hechizo |
| `Espacio` | Siguiente oleada (adelantarla da oro extra) |
| `U` | Mejorar la torre seleccionada |
| `S` | Vender la torre seleccionada |
| `T` | Cambiar el criterio de objetivo |
| `+` / `-` | Velocidad del juego |
| `P` | Pausa |
| `Esc` / clic derecho | Cancelar selección |

## Torres y hechizos

| Torre | Coste |
|---|---|
| Torre de arqueros | 70 |
| Torre de hielo | 90 |
| Torre de magos | 110 |
| Catapulta | 120 |
| Alquimista | 130 |
| Ballesta pesada | 150 |
| Templo de la Luz | 160 |

Hechizos: **Lluvia de flechas**, **Tormenta helada** y **Meteoro**.

## Ejecutar en local

Basta con abrir `index.html` en el navegador. Si prefieres servirlo por HTTP:

```bash
git clone https://github.com/alvarodiez20/baluarte.git
cd baluarte
python3 -m http.server 8000
# abre http://localhost:8000
```

## Despliegue

El repositorio se publica en GitHub Pages mediante
[`.github/workflows/pages.yml`](.github/workflows/pages.yml), que sube la raíz del proyecto
como artefacto y la despliega con `actions/deploy-pages`. Cada push a la rama por defecto
lanza un despliegue nuevo; también puede ejecutarse a mano desde
**Actions → Deploy to GitHub Pages → Run workflow**.

Para replicarlo en tu propia copia hay que activar Pages una sola vez en
**Settings → Pages → Source: GitHub Actions** (crear el sitio requiere permisos de
administración del repositorio, así que el propio workflow no puede hacerlo).

El archivo `.nojekyll` evita que GitHub procese los archivos con Jekyll.

## Estructura del proyecto

```
.
├── index.html                    # el juego completo: HTML, CSS y JS
├── .github/workflows/pages.yml   # despliegue a GitHub Pages
├── .nojekyll                     # sirve los archivos sin procesar
└── README.md
```

## Modificar el juego

Todo el contenido está en bloques de datos al inicio del `<script>` de `index.html`:

| Bloque | Contiene |
|---|---|
| `ENEMIES` | Estadísticas y textos de enemigos y jefes |
| `TOWERS` | Torres, niveles, costes y especializaciones |
| `SPELLS` | Hechizos, daño y enfriamientos |
| `LEVELS` | Mapas (puntos del camino sobre una cuadrícula de 24×15), oleadas, oro inicial, enemigos disponibles, jefe, recompensas e historia |
| `META` | Mejoras permanentes compradas con Gloria |
| `ACHIEVEMENTS` | Logros y la Gloria que otorgan |

Para añadir un capítulo, copia una entrada de `LEVELS` y cambia el `id`, el camino y los
textos. La partida guardada vive bajo la clave `baluarte_save_v1` de `localStorage`; si
cambias la estructura de datos, súbele la versión para no leer partidas incompatibles.

## Compatibilidad

Navegadores de escritorio modernos (Chrome, Firefox, Edge, Safari). La partida se escala
para caber siempre en la ventana, sin recortes ni scroll: en pantallas grandes se amplía
hasta 2×, y en ventanas estrechas —media pantalla, por ejemplo— el panel lateral pasa
debajo del tablero para aprovechar el alto. El control es de teclado y ratón, así que no
está adaptado a móvil.
