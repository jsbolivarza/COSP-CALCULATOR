# Calculadora CPS — app instalable (PWA)

Herramienta para calcular el Costo de Producción Sostenible del café durante los grupos
focales (FGD). Se instala como app en un teléfono, tablet o computador y funciona sin
conexión después de la primera vez que se abre.

Los archivos deben estar publicados en un sitio con HTTPS. No sirve abrir `index.html`
haciendo doble clic: sin HTTPS el navegador no instala la app ni guarda la copia para uso
sin conexión. GitHub Pages cumple ese requisito y es gratis.

## Archivos

- `index.html` — la calculadora completa (interfaz, traducciones, cálculos, guardado).
- `manifest.json` — nombre, ícono y colores de la app instalada.
- `sw.js` — el "service worker": guarda una copia de la app en el dispositivo la primera vez
  que se abre, para que funcione sin internet después.
- `icon-192.png`, `icon-512.png` — íconos de la app.

Los cinco archivos van juntos en la raíz del repositorio, con esos nombres exactos.

## Publicar en GitHub Pages

1. En GitHub, crear un repositorio nuevo (Pages gratis en cuentas personales requiere que el
   repositorio sea público).
2. Subir los 5 archivos a la raíz del repositorio, manteniendo los nombres exactos.
3. Ir a **Settings → Pages**.
4. En "Build and deployment", elegir **Deploy from a branch**, rama `main` (o `master`),
   carpeta `/ (root)`.
5. Guardar. GitHub tarda uno o dos minutos en publicar el sitio.
6. La URL quedará como: `https://SU-USUARIO.github.io/NOMBRE-DEL-REPOSITORIO/`

## Instalar en un dispositivo

- **Android (Chrome):** abrir la URL, tocar el menú (⋮) y elegir "Instalar app" o "Añadir a
  pantalla de inicio".
- **iPhone / iPad (Safari):** abrir la URL en Safari, tocar el ícono de compartir (□↑) y elegir
  "Añadir a pantalla de inicio". iPhone no muestra un aviso automático como Android; hay que
  hacerlo manualmente la primera vez. Usar Safari, no Chrome ni Edge en iOS.
- **Computador (Chrome/Edge):** aparecerá un ícono de instalación en la barra de direcciones.

## Cómo se usa

### Varios FGD en un mismo dispositivo

Al abrir la app aparece la lista de FGD guardados en ese dispositivo. Cada FGD se guarda por
separado, así que un facilitador puede hacer varios grupos focales seguidos sin perder ni
mezclar los datos.

- **+ Nuevo FGD** empieza uno nuevo, sin tocar los anteriores.
- **Abrir** retoma un FGD ya empezado.
- Cada tarjeta de la lista muestra el nombre, la cooperativa, el CPS total y la fecha del
  último cambio, y tiene sus propios botones de JSON, CSV y borrar.
- **Mis FGD** vuelve a esa lista desde cualquier pestaña.

Un dispositivo aguanta sin problema del orden de 100 FGD. El límite real es el espacio de
almacenamiento del navegador, no un número fijo.

### Las tres pestañas

1. **Actividades de la finca** — qué actividades se hacen, qué presentación de café se vende y
   el rendimiento. Determina qué preguntas de costo aparecen después.
2. **Cuestionario de costos** — solo las categorías que corresponden a lo marcado en la
   pestaña 1. Cada categoría se puede llenar en modo global o actividad por actividad.
3. **Comparar FGD** — todos los FGD del dispositivo lado a lado, con una fila de promedio.
   Si los FGD no usan la misma moneda o unidad de área, aparece un aviso: el promedio mezcla
   unidades y no debe reportarse tal cual.

### Guardado

Todo lo que se escribe queda guardado en el dispositivo automáticamente, dentro del FGD
abierto. No hace falta apretar nada. Nada sale del dispositivo hasta que se exporta.

Si el navegador bloquea el guardado (navegación privada, almacenamiento lleno), el indicador
de arriba a la derecha lo avisa. En ese caso hay que exportar los datos antes de cerrar.

## Sacar los datos

Los botones de archivo están en la barra de arriba y se ven desde cualquier pestaña.

- **Guardar este FGD (JSON)** — el FGD abierto, con todo el detalle línea por línea. Sirve
  para enviarlo por correo a quien consolida, o para pasarlo a otro dispositivo.
- **Exportar este FGD (CSV)** — el FGD abierto como una sola fila.
- **Exportar todos (CSV)** — un archivo con una fila por FGD y una columna `fgd_id` que
  identifica cada uno. Es el archivo pensado para pegar directo en una hoja maestra.
- **Respaldar todos (JSON)** — respaldo completo de todos los FGD del dispositivo.
- **Cargar JSON** — acepta tanto un FGD suelto como un respaldo completo. Los FGD se agregan
  a la lista; no borra nada de lo que ya está en el dispositivo. Si un FGD que se carga tiene
  el mismo identificador que uno que ya está guardado, se actualiza ese en vez de duplicarse.
- **Borrar todos los datos** — borra todos los FGD del dispositivo. Pide confirmación.

Los nombres de columna del CSV usan identificadores fijos en inglés (`fertilization_total`,
`total_cps_per_area_unit`, etc.), no las etiquetas traducidas. Así los archivos de
facilitadores que trabajan en distinto idioma se alinean en la misma hoja maestra. El CSV de
un solo FGD y el de todos tienen exactamente las mismas columnas.

## Actualizar la app más adelante

Cuando cambien `index.html`, hay que subir el archivo actualizado **y** cambiar el número de
versión de `CACHE_NAME` en la primera línea útil de `sw.js` (por ejemplo de
`"cosp-fgd-shell-v5"` a `"cosp-fgd-shell-v6"`). Sin ese cambio, quien ya instaló la app puede
seguir viendo la versión vieja guardada en su dispositivo.

Los datos ya capturados no se pierden al actualizar: quedan en el almacenamiento del
navegador, aparte de los archivos de la app.

## Límites conocidos

- **Español y portugués son primeras traducciones automáticas.** El inglés es la versión de
  referencia; conviene que un hablante nativo revise las otras dos antes de usarlas en campo.
- **Las fuentes de letra (Google Fonts) no se guardan para uso sin conexión.** Si no hay
  internet la primera vez, el texto se ve con la fuente del sistema. No afecta el
  funcionamiento, solo la apariencia.
- **Los datos viven solo en ese dispositivo.** No hay servidor ni sincronización. Si se borran
  los datos del navegador o se desinstala la app sin exportar, los FGD se pierden. Conviene
  hacer un respaldo JSON al terminar cada jornada de campo.
- **Los confirmaciones de borrado son un cuadro dentro de la página**, no el aviso del sistema,
  porque ese aviso no funciona bien en navegadores iOS distintos de Safari.
