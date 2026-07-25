# Calculadora CPS — versión instalable (PWA)

Esta carpeta contiene la misma calculadora, empaquetada para poder instalarse como una app
en un teléfono, tablet o computador, y para funcionar sin conexión después de la primera vez
que se abre. Para que esto funcione, los archivos deben estar en un sitio con HTTPS — no
sirve abrir `index.html` haciendo doble clic. GitHub Pages cumple ese requisito y es gratis.

## Archivos

- `index.html` — la calculadora (idéntica a la versión de un solo archivo, más las líneas
  necesarias para que se pueda instalar).
- `manifest.json` — le dice al navegador el nombre, ícono y colores de la app instalada.
- `sw.js` — el "service worker": guarda una copia de la app en el dispositivo la primera vez
  que se abre, para que funcione sin internet después.
- `icon-192.png`, `icon-512.png` — íconos de la app.

## Publicar en GitHub Pages

1. En GitHub, crear un repositorio nuevo (puede ser público o privado si tienen GitHub Pro/Team;
   Pages gratis en cuentas personales requiere que el repositorio sea público).
2. Subir estos 5 archivos a la raíz del repositorio (`index.html`, `manifest.json`, `sw.js`,
   `icon-192.png`, `icon-512.png`), manteniendo los nombres exactos.
3. Ir a **Settings → Pages** dentro del repositorio.
4. En "Build and deployment", elegir **Deploy from a branch**, rama `main` (o `master`), carpeta `/ (root)`.
5. Guardar. GitHub tarda uno o dos minutos en publicar el sitio.
6. La URL quedará como: `https://SU-USUARIO.github.io/NOMBRE-DEL-REPOSITORIO/`

## Instalar en un teléfono

- **Android (Chrome):** abrir la URL, tocar el menú (⋮) y elegir "Instalar app" o "Añadir a
  pantalla de inicio".
- **iPhone (Safari):** abrir la URL, tocar el ícono de compartir (□↑) y elegir
  "Añadir a pantalla de inicio". iPhone no muestra un aviso automático como Android — hay que
  hacerlo manualmente la primera vez.
- **Computador (Chrome/Edge):** aparecerá un ícono de instalación (⊕ o similar) en la barra de
  direcciones.

## Actualizar la app más adelante

Cuando cambien `index.html`, hay que subir el archivo actualizado al repositorio y además
cambiar el número de versión en la primera línea de `sw.js` (`CACHE_NAME`, por ejemplo de
`"cosp-fgd-shell-v1"` a `"cosp-fgd-shell-v2"`). Sin ese cambio, alguien que ya instaló la app
puede seguir viendo la versión vieja guardada en su dispositivo, incluso después de que ustedes
suban la nueva.

## Qué es distinto respecto al archivo único (calculadora_cosp_fgd.html)

- **Se instala como app** con ícono propio, en vez de ser un archivo que se abre por correo.
- **Funciona sin internet** después de la primera vez que se abre (gracias a `sw.js`).
- **Requiere estar publicada en un sitio con HTTPS** (GitHub Pages, por ejemplo) — no se puede
  simplemente enviar por correo y abrir con doble clic, como sí funciona con el archivo único.
- El botón "Guardar copia HTML" y "Exportar CSV" siguen funcionando igual que antes.
- Las fuentes de letra (Google Fonts) no se guardan para uso sin conexión; si no hay internet
  la primera vez que se instala, el texto se ve con la fuente del sistema en vez de la fuente
  de diseño — no afecta el funcionamiento, solo la apariencia.
