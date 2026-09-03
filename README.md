# Baluarte — Crónicas de la Guardia del Norte

Juego de defensa de torres (tower defense) medieval en un único archivo `index.html`. Sin dependencias, sin servidor: funciona directamente en GitHub Pages.

## Publicar en GitHub Pages

El repositorio ya incluye el workflow `.github/workflows/pages.yml`, que publica la raíz del proyecto en cada push a la rama por defecto.

1. Ve a **Settings → Pages** del repositorio.
2. En *Build and deployment → Source* elige **GitHub Actions**.
3. Haz push a `main` (o lanza el workflow a mano desde la pestaña **Actions → Deploy to GitHub Pages → Run workflow**).
4. En uno o dos minutos el juego estará en `https://alvarodiez20.github.io/baluarte/`.

Alternativa sin Actions: en *Source* elige **Deploy from a branch**, rama `main`, carpeta `/ (root)` y pulsa **Save**. El archivo `.nojekyll` evita que Jekyll procese los archivos.

## Qué incluye

- **Campaña de 10 capítulos** con historia (la traición del Canciller Malaquías y el regreso del liche Vhaldrek), 192 oleadas en total y un jefe al final de cada capítulo.
- **7 torres**: arqueros, catapulta, magos, hielo, ballesta pesada, alquimista y Templo de la Luz. Cada una con 3 niveles y dos **especializaciones** al máximo (14 ramas distintas).
- **3 hechizos**: Lluvia de flechas, Tormenta helada y Meteoro.
- **14 enemigos + 10 jefes** con armadura, resistencia mágica, vuelo, curación, regeneración e invocaciones.
- **Progresión permanente**: estrellas por capítulo, Gloria, 10 mejoras del reino, 17 logros y bestiario.
- **Dificultades** Normal, Difícil y Pesadilla (esta última se desbloquea al terminar la campaña) y modo **Asedio infinito**.
- Guardado automático en el navegador (`localStorage`).

## Controles

`1`–`7` elegir torre · clic para construir (Shift + clic para construir varias) · `Q` `W` `E` hechizos · `Espacio` siguiente oleada (adelantarla da oro extra) · `P` pausa · `Esc` cancelar · `U` mejorar · `S` vender · `T` cambiar objetivo · `+`/`-` velocidad · clic derecho cancelar.

## Modificar el juego

Todo el contenido está en bloques de datos al inicio del `<script>` de `index.html`:

- `ENEMIES`, `TOWERS`, `SPELLS`: estadísticas y textos.
- `LEVELS`: mapas (lista de puntos del camino en casillas de una cuadrícula de 24×15), oleadas, oro inicial, enemigos disponibles, jefe, recompensas e historia.
- `META`, `ACHIEVEMENTS`: mejoras permanentes y logros.

Para añadir un capítulo basta con copiar una entrada de `LEVELS`, cambiar el `id`, el camino y los textos.
