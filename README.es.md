# Calculadora CPS (PWA)

*English: [README.md](README.md)*

Herramienta para calcular el Costo de Producción Sostenible del café durante los grupos
focales (FGD). Se instala como app en un teléfono, tablet o computador y funciona sin conexión
después de la primera vez que se abre.

La interfaz está disponible en inglés, español y portugués, y se cambia en cualquier momento
desde el encabezado.

Los archivos deben estar publicados en un sitio con HTTPS. No sirve abrir `index.html` haciendo
doble clic: sin HTTPS el navegador no instala la app ni guarda la copia para uso sin conexión.
GitHub Pages cumple ese requisito y es gratis.

## Archivos

Los cinco archivos que la app necesita para funcionar:

- `index.html` es la calculadora completa: interfaz, traducciones, cálculos y guardado.
- `manifest.json` le indica al navegador el nombre, ícono y colores de la app instalada.
- `sw.js` es el service worker. Guarda una copia de la app en el dispositivo la primera vez que
  se abre, para que funcione sin internet después.
- `icon-192.png` e `icon-512.png` son los íconos de la app.

Esos cinco van juntos en la raíz del repositorio, con esos nombres exactos.

Junto a ellos están `README.md` y `README.es.md`, la misma documentación en inglés y español.
Sirven para quien mantiene o publica la herramienta. La app nunca los lee, así que se pueden
editar o quitar sin afectar nada. Conviene actualizar los dos cuando cambie uno.

## Publicar en GitHub Pages

1. Crear un repositorio nuevo en GitHub. Pages gratis en una cuenta personal requiere que el
   repositorio sea público.
2. Subir los cinco archivos de la app a la raíz del repositorio, manteniendo los nombres
   exactos. Los README también pueden subirse; la app los ignora.
3. Ir a **Settings**, luego **Pages**.
4. En "Build and deployment", elegir **Deploy from a branch**, rama `main` (o `master`),
   carpeta `/ (root)`.
5. Guardar. GitHub tarda uno o dos minutos en publicar el sitio.
6. La URL quedará como `https://SU-USUARIO.github.io/NOMBRE-DEL-REPOSITORIO/`

## Instalar en un dispositivo

**Android (Chrome):** abrir la URL, tocar el menú y elegir "Instalar app" o "Añadir a pantalla
de inicio".

**iPhone o iPad (Safari):** abrir la URL en Safari, tocar el ícono de compartir y elegir
"Añadir a pantalla de inicio". iPhone no muestra un aviso automático como Android, así que hay
que hacerlo manualmente la primera vez. Usar Safari, no Chrome ni Edge en iOS.

**Computador (Chrome o Edge):** aparece un ícono de instalación en la barra de direcciones.

## Cómo se usa

### Pantalla de inicio: dos pestañas

**Mis FGD** muestra la lista de FGD guardados en ese dispositivo. **Comparar FGD** los pone
todos lado a lado.

Cada FGD se guarda por separado, así que un facilitador puede hacer varios grupos focales
seguidos sin perder ni mezclar los datos.

- **+ Nuevo FGD** empieza uno nuevo sin tocar los anteriores.
- **Abrir** retoma un FGD ya empezado.
- Cada tarjeta de la lista muestra el nombre, la cooperativa, el CPS total y la fecha del
  último cambio, y tiene sus propios botones de JSON, CSV y borrar.
- **Mis FGD** en la barra superior regresa a esta pantalla desde cualquier lugar.

Un dispositivo aguanta sin problema del orden de 100 FGD. El límite real es el espacio de
almacenamiento del navegador, no un número fijo.

### Buscar en la lista

Arriba de la lista hay un buscador, que aparece en cuanto haya al menos un FGD guardado. Busca
al mismo tiempo en el nombre del FGD, el nombre de la cooperativa y el FLO-ID, así que
cualquiera de los tres sirve para encontrar un registro.

No distingue mayúsculas ni acentos, en los dos sentidos: escribir "cafe" encuentra "Sol y
Café", y escribir "café" también. Varias palabras funcionan como Y, no como O, así que
"bagua 02" reduce al único FGD que contiene las dos, en vez de ampliar a todos los que
contienen alguna.

Mientras hay una búsqueda activa, el contador dice "Mostrando 2 de 10 FGD" y aparece un botón
para limpiarla. La búsqueda solo afecta la lista: nunca cambia la pestaña de comparación, y se
borra sola después de cargar un archivo o de borrar datos, para que unos FGD recién cargados
nunca parezcan perdidos.

### Comparar FGD

La comparación vive en la pantalla de inicio y no dentro de un FGD, porque describe todo el
dispositivo.

**Filtros.** Arriba de la tabla hay tres filtros: presentación, moneda y unidad de área. El
promedio se recalcula sobre lo que quede visible, y su etiqueta indica cuántos FGD entraron,
por ejemplo "Promedio (8)".

**Promedios que se dejan en blanco.** Un kilo de cereza y un kilo de pergamino seco no son lo
mismo, así que promediar rendimiento o precio por kg entre presentaciones distintas da un
número sin sentido. Cuando los FGD visibles no comparten presentación, esos dos promedios salen
como raya y aparece un aviso explicando por qué. Lo mismo pasa con los promedios de dinero
(jornal, CPS total, precios) cuando se mezclan monedas o unidades de área. Los valores de cada
fila siguen visibles, porque cada uno por separado sí es válido.

El **precio por kg GBE** es la única columna de precio comparable entre presentaciones
distintas. Para eso existe.

### Dentro de un FGD: dos pestañas

1. **Actividades de la finca**: qué actividades se hacen, qué presentación de café se vende y
   el rendimiento. Determina qué preguntas de costo aparecen después.
2. **Cuestionario de costos**: solo las categorías que corresponden a lo marcado en la
   pestaña 1. Cada categoría se puede llenar en modo global o actividad por actividad.

### Unidad de área

La herramienta nunca convierte entre unidades. Todo se captura en la unidad que se elija, y el
precio por kg sale de dividir el costo por unidad entre el rendimiento por unidad, así que el
cálculo es correcto en cualquier unidad mientras las dos cifras estén en la misma.

Las etiquetas siguen la unidad elegida. Si se elige Manzana, el campo de rendimiento pide kg/mz
y el cuestionario dice mz, no ha. Si se elige **Otra**, aparece un campo para escribir el
nombre local de la unidad, por ejemplo cuerda o tarea, y todas las etiquetas lo usan.

### Guardado

Todo lo que se escribe queda guardado en el dispositivo automáticamente, dentro del FGD
abierto. No hace falta apretar nada. Nada sale del dispositivo hasta que se exporta.

Si el navegador bloquea el guardado, por ejemplo en navegación privada o cuando el
almacenamiento está lleno, el indicador de la barra superior lo avisa. En ese caso hay que
exportar los datos antes de cerrar.

## Sacar los datos

Los botones de archivo están en la barra superior y se ven desde cualquier pestaña.

- **Guardar este FGD (JSON)** exporta el FGD abierto con todo su detalle línea por línea. Sirve
  para enviar un FGD por correo a quien consolida, o para pasarlo a otro dispositivo.
- **Exportar este FGD (CSV)** exporta el FGD abierto como una sola fila.
- **Exportar todos (CSV)** genera un archivo con una fila por FGD y una columna `fgd_id` que
  identifica cada uno. Es el archivo pensado para pegar directo en una hoja maestra.
- **Respaldar todos (JSON)** es un respaldo completo de todos los FGD del dispositivo.
- **Cargar JSON** acepta tanto un FGD suelto como un respaldo completo.
- **Borrar todos los datos** borra todos los FGD del dispositivo, con confirmación previa.

### Nota sobre cargar JSON

Cargar agrega FGD a la lista. Nunca borra nada de lo que ya está en el dispositivo.

Cargar dos veces el mismo archivo crea una segunda copia de cada FGD en vez de actualizar el
original, así que la lista mostrará duplicados. Hay que borrar las copias sobrantes a mano, o
borrar todos los datos primero y luego cargar el respaldo. Conviene tenerlo presente al mover
datos entre dispositivos.

### Columnas del CSV

Los nombres de columna del CSV usan identificadores fijos en inglés, como `fertilization_total`
y `total_cps_per_area_unit`, y no las etiquetas traducidas. Así los archivos de facilitadores
que trabajan en distinto idioma de interfaz se alinean en la misma hoja maestra. El CSV de un
solo FGD y el de todos tienen exactamente las mismas columnas.

Ninguna columna asume hectáreas. Los rendimientos salen como
`yield_kg_per_area_unit_in_type` y `yield_kg_gbe_per_area_unit`, y la unidad de cada FGD viene
en `area_unit`, más `area_unit_custom_name` cuando ese FGD usa una unidad propia. Hay que
revisar esas columnas antes de sumar o promediar entre FGD en la hoja maestra.

## Actualizar la app más adelante

Cuando cambie `index.html`, hay que subir el archivo nuevo **y** cambiar el número de versión
en `CACHE_NAME`, al inicio de `sw.js`, actualmente `"cosp-fgd-shell-v7.1"`. Sin ese cambio,
quien ya instaló la app puede seguir viendo la versión vieja guardada en su dispositivo.

Los datos ya capturados no se pierden al actualizar la app. Viven en el almacenamiento del
navegador, aparte de los archivos de la app.

## Límites conocidos

- **El español y el portugués son primeras traducciones automáticas.** El inglés es la versión
  de referencia. Conviene que un hablante nativo revise las otras dos antes de usarlas en
  campo.
- **Las fuentes de letra (Google Fonts) no se guardan para uso sin conexión.** Si no hay
  internet la primera vez, el texto se ve con la fuente del sistema. Afecta solo la apariencia,
  no el funcionamiento.
- **Los datos viven solo en ese dispositivo.** No hay servidor ni sincronización. Si se borran
  los datos del navegador o se desinstala la app sin exportar, los FGD se pierden. Conviene
  hacer un respaldo JSON al terminar cada jornada de campo.
- **Las confirmaciones de borrado son un cuadro dentro de la página** y no el aviso del
  sistema, porque ese aviso no funciona bien en navegadores iOS distintos de Safari.
- **La categoría Administración y Servicios de la Finca oculta sus componentes de Insumos y
  Mano de obra contratada**, porque no aplican ahí. Esos dos campos quedan vacíos por diseño.
  Un valor metido ahí a la fuerza mediante un archivo cargado contaría en el CPS total sin
  aparecer en ninguna pantalla.
