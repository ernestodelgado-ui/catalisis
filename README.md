# Catálisis · Bioferia

Prototipo interactivo de la marca Bioferia. Cada persona recibe una semilla, suma elementos de Aire, Tierra, Agua, Fuego y Corazón, y se lleva un ser único (postal PNG de 1080×1350).

Es una sola página estática: no necesita servidor ni base de datos.

## Archivos

| Archivo | Para qué sirve |
|---|---|
| `index.html` | Toda la app (código, estilos y el mapa de la feria embebido) |
| `manifest.webmanifest` | Permite instalarla como app en el celular |
| `sw.js` | Hace que abra sin conexión; las actualizaciones llegan solas |
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

## Pendientes conocidos

- Las hojas del logo están trazadas a ojo sobre la imagen. Conviene reemplazarlas por el SVG oficial (`LEAF_PATHS` y `LEAF_D`).
- Las tipografías de cada elemento son aproximaciones libres de Google Fonts. Hay que reemplazarlas por las reales de la marca.
- Los seres del mapa son de muestra. Para mostrar los reales hace falta un servicio que los guarde (por ejemplo, Firebase o Supabase).
- Las combinaciones del superpoder son provisorias.

## Probarla en local

Abrí una terminal en esta carpeta y corré `npx serve` (o `python -m http.server`). Después entrá a la dirección que muestre. Abrir `index.html` con doble clic también funciona, pero ahí no se registra el modo sin conexión.
