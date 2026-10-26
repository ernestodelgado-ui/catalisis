# Catálisis 3D · Bioferia

Versión 3D: el ser y sus elementos tienen volumen y se pueden girar con el dedo. Si el celular va lento, baja la calidad sola o vuelve a 2D.

Prototipo interactivo de la marca Bioferia. Cada persona recibe una semilla, suma elementos de Aire, Tierra, Agua, Fuego y Corazón, y se lleva un ser único (postal PNG de 1080×1350).

Es una sola página estática: no necesita servidor ni base de datos.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | Toda la app (código, estilos y el mapa de la feria embebido) |
| `manifest.webmanifest` | Permite instalarla como app en el celular |
| `sw.js` | Hace que abra sin conexión; las actualizaciones llegan solas |
| `favicon.ico`, `favicon.svg`, `favicon-32.png` | Ícono de la pestaña del navegador (las dos hojas rosas, fondo transparente) |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png`, `apple-touch-icon.png` | Íconos de la app |
| `.nojekyll` | Le dice a GitHub que sirva los archivos tal cual |

## Subirla a GitHub Pages

1. En GitHub: **New repository**, con un nombre como `bioferia-catalisis` (público).
2. **Add file → Upload files** y arrastrá **todo el contenido de esta carpeta**, incluido `.nojekyll`. Confirmá con **Commit changes**.
3. En el repositorio: **Settings → Pages**. En *Build and deployment* elegí **Deploy from a branch**, rama `main` y carpeta `/ (root)`. Guardá.
4. A los 1 o 2 minutos aparece la dirección: `https://TU-USUARIO.github.io/bioferia-catalisis/`.

Con Git en la compu es lo mismo:

```bash
git init
git add .
git commit -m "Catálisis Bioferia"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/bioferia-catalisis.git
git push -u origin main
```

## Subirla a Vercel

La carpeta ya está lista para Vercel, sin configuración:

1. En vercel.com: **Add New → Project** e importá el repositorio de GitHub.
2. En *Framework Preset* dejá **Other**. No hace falta comando de build ni carpeta de salida.
3. **Deploy**. La dirección queda como `https://NOMBRE.vercel.app/`.

El favicon se carga solo: Vercel sirve `/favicon.ico` desde la raíz, y `index.html` también apunta al SVG y al PNG. Los QR funcionan igual, con el ancla al final (`…vercel.app/#agua`).

## Códigos QR de la feria

Cada QR abre la app directo en un elemento. Agregá el ancla al final de la dirección:

- `…/bioferia-catalisis/#aire`
- `…/bioferia-catalisis/#tierra`
- `…/bioferia-catalisis/#agua`
- `…/bioferia-catalisis/#fuego`
- `…/bioferia-catalisis/#corazon`

La dirección sin ancla empieza por la bienvenida.

## Cómo actualizarla

Reemplazá `index.html` en el repositorio (**Add file → Upload files**, mismo nombre) y confirmá. En un minuto está publicada. Quien ya la tenga abierta o instalada ve la versión nueva al volver a abrirla con conexión.

## Qué se puede ajustar, y dónde (dentro de `index.html`)

- **Combinaciones del superpoder:** buscá `const POWERS=`. Cada entrada es `'símbolo+número':['Texto','efecto']`. Los efectos disponibles son `spin`, `shrink`, `flash`, `pulse` y `confetti`. Los símbolos están en `const SYMS=`.
- **Zonas del mapa:** buscá `const ZONES=`. Cada zona tiene su catalizador (`c`) y su posición `x`, `y` en el plano de 1920×1080.
- **Frases:** el texto de la bienvenida está en `function renderWelcome`, y el de felicitaciones en `function openCongrats`.
- **Año de la postal:** buscá `BUENOS AIRES · 2027`.

## Refugio (apartado de sonido)

Se desbloquea al llenar la barra (etapa final) y usar un superpoder: cuando termina el efecto aparece "Desbloqueaste Refugio, un momento para conectar con vos". Al tocar **Ingresar** empieza el sonido; el ser flota en calma, con fondo de auroras, y toma un color etéreo. Al tocar **Salir** recupera su color.

- Hay un sonido sintetizado por cada subelemento (25 en total, en `RF_SND`). Cada ser suena según los elementos que eligió, y los repetidos suenan más fuerte.
- Para ajustar un sonido, buscá `const RF_SND=` en `index.html`: cada entrada tiene sus volúmenes. El volumen general está en `rfBuild` (`const level=`).
- **iPhone:** el interruptor de silencio apaga el audio de las webs. La app activa la sesión de audio "playback" y reproduce un audio mudo en bucle para que suene igual; si el teléfono lo bloquea, el botón dice "Tocá para activar el sonido".
- El sonido solo arranca tras un toque (regla de los navegadores) y se pausa si se cierra la pantalla o se cambia de app.

## Escuchar a otros seres (mapa)

En el mapa, al tocar un ser se abre su ficha con **Así fue hecho** (su recorrido de elementos) y el botón **♫ Escuchar a este ser**. Suena su paisaje sonoro, armado con los sonidos de los elementos que lo componen. Cada ser suena siempre igual (la semilla del ser fija el azar y la tonalidad). Al tocar otro ser mientras suena, cambia el sonido; al tocar un lugar vacío, la música sigue; al cerrar el mapa, se corta.

## Pendientes conocidos

- Las hojas del logo están trazadas a ojo sobre la imagen. Conviene reemplazarlas por el SVG oficial (`LEAF_PATHS` y `LEAF_D`).
- Las tipografías de cada elemento son aproximaciones libres de Google Fonts. Hay que reemplazarlas por las reales de la marca.
- Los seres del mapa son de muestra. Para mostrar los reales hace falta un servicio que los guarde (por ejemplo, Firebase o Supabase).
- Las combinaciones del superpoder son provisorias.
- Los volúmenes de Refugio se ajustaron por medición, no de oído: conviene afinarlos escuchando con auriculares.

## Probarla en local

Abrí una terminal en esta carpeta y corré `npx serve` (o `python -m http.server`). Después entrá a la dirección que muestre. Abrir `index.html` con doble clic también funciona, pero ahí no se registra el modo sin conexión.


