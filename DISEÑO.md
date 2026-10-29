# Tatuajes y barbería: brief de diseño

Plantilla `tatuajes-barberia` creada el 29/10/2026 a partir de `gimnasio-deporte` con `php artisan plantillas:nueva` y
rediseñada entera a ancho completo (tanda «ancho completo»). Este fichero se queda en el repo: es lo que lee quien
(persona o agente) rediseñe la plantilla.

## Brief

- **Para quién**: estudios de tatuaje, barberías, estudios de piercing y locales que mezclan las tres cosas
  (`tatuajes, barberia, piercing, estudio-tatuaje`). Quien entra quiere ver trabajos, saber quién tatúa o corta y en
  qué estilo, cuánto cuesta más o menos, cómo se cura un tatuaje y pedir cita.
- **Qué tiene que conseguir la web**: que pidan cita contando la idea (formulario con servicio, zona del cuerpo,
  tamaño y fecha) o por WhatsApp. Secundario: llamar y ir al estudio.
- **Tono y estilo** (`crudo`): crudo, artesano, con oficio. Sí: el rótulo pintado de una barbería antigua, una lámina
  de «flash» de tatuaje tradicional, el papel de calco y el sello de tinta. No: la caja centrada con tarjetas blancas,
  el verde neón con franjas diagonales y botones inclinados de `gimnasio-deporte`, la letra de cartel condensada y el
  magenta de `musica-espectaculos`, ni la hoja de contactos en monoespaciada de `fotografo`.
- **Paleta de ejemplo**: fondo `#0f0d0c` (negro tinta), texto `#ece3d2` (hueso), primario `#7a1712` (rojo oscuro),
  acento `#c8361f` (rojo vivo). Derivados con `color-mix` en `global.css`: `--rojo-claro` (acento + hueso, el rojo
  que se lee sobre negro), `--negro` (pie), `--resalte` (lo que resalta en cada banda: rojo claro sobre negro, rojo
  oscuro sobre hueso, la letra sobre rojo), `--sobre-acento` y `--sobre-primario` (letra calculada con `oklch`).
  Aguanta otros cuatro colores: las bandas hueso son `texto` sobre `fondo` invertidos.
- **Tipografía** (sistema, sin descargas): titulares en slab serif pesada («Rockwell Extra Bold», «Rockwell», «Roboto
  Slab», «Clarendon», «Bookman Old Style», Georgia) a 800 sin negrita sintética, en caja normal: portada hasta 7 rem
  (2,75 rem en móvil), títulos de sección hasta 5,5 rem. Antetítulos, menú, botones, etiquetas y duraciones en
  system-ui 700 en mayúsculas con interletrado de 0,16-0,26 em. Texto en system-ui.
- **Motivos propios**: grano de papel (SVG `feTurbulence` en línea) en todas las bandas; bordes dentados de sello
  (máscara `conic-gradient`) en lo alto de las bandas rojas, hueso y del pie; estrellas de ocho puntas (✶) como
  separadores y marca de «destacado»; lista de precios con puntos guía y doble filete como un rótulo de barbería;
  números de paso enormes en slab serif translúcida; botones de bloque rojo con doble filete interior (sello);
  retratos en blanco y negro contrastado que se colorean al pasar; velo rojo sobre las fotos de la galería al pasar.
- **Ritmo de bandas** (todas de borde a borde, contenido a `max-width: 90rem`):
  portada partida (negro + foto a sangre, letrero vertical rojo con la localidad, cinta roja dentada con los `items`)
  → servicios (hueso; franja de foto 21:9 a sangre y lista de precios en 3 columnas) → artistas (negro; retratos de
  borde a borde en 4 columnas) → cómo trabajamos (roja dentada; 4 pasos) → trabajos (negro; mosaico de borde a borde
  sin márgenes) → la casa (hueso dentada; cita enorme) → cuidados y preguntas (negro; 50/50 con foto a sangre a la
  izquierda) → pide cita (50/50 roja / negra con formulario) → contacto (hueso dentada; teléfono enorme, tablilla de
  horario y formulario corto) → pie (negro dentado; nombre grande, botón de cita y cuatro columnas).
- **Responsive**: móvil primero. A 375 px todo en una columna con 16 px de margen del texto (fotos y fondos tocan el
  borde): la foto de la portada arriba a todo el ancho, la cinta en tres líneas, los grupos de precios uno debajo de
  otro, artistas y galería a 2 columnas sin márgenes, las bandas partidas apiladas, menú plegable con enlaces de
  48 px y botones de 48 px. A 768, pasos en 2 columnas, galería a 4 y cinta en una fila. A partir de 1024, portada,
  preguntas y cita partidas 50/50 y precios en 3 columnas.

## Apartados

1. `hero`: antetítulo, `titulo`, `texto`, `cta`, `cta_secundario`, `imagen` (1:1) e `items` ({titulo, icono}).
2. `servicios`: `imagen` (21:9), `servicios: [{nombre, texto, precio, duracion, categoria, destacado}]`, `nota`, `cta`.
3. `artistas`: `personas: [{nombre, cargo, estilos, foto, texto}]` (`estilos` con comas).
4. `proceso`: `items: [{titulo, texto, icono}]` (cita, diseño, sesión, cuidados).
5. `galeria`: `galeria` (8 fotos) y `cta`.
6. `manifiesto`: `declaracion` y `autor` (y `titulo` pequeño encima).
7. `preguntas`: `imagen` (3:4) y `preguntas: [{pregunta, respuesta}]` (cuidados y dudas).
8. `cita`: `items: [{titulo, texto}]`, `opciones` (zonas del cuerpo con «;»), `nota`, `boton_formulario`.
9. `contacto`: `horario: [{dia, horas}]` y `boton_formulario`.

## Fotos (`fotos.json`, 11)

Interior del estudio en piedra del casco viejo (portada), encimera de barbería con navajas (franja), antebrazo con
tatuaje tradicional sin cara, máquina de bobinas, láminas de flash sin letras, navaja con toalla caliente, nuca con
degradado de espaldas, joyas de piercing, frascos de tinta sin etiqueta, vista general del estudio y brazo con film
tras la sesión. Sin texto legible, sin logotipos, sin caras.

## Qué no hacer

- Volver a la caja centrada estrecha con tarjetas, al neón y las franjas del gimnasio o a la letra condensada.
- Fotos de caras o de tatuajes con letras legibles.
- Precios o cifras fijos en los componentes: todo sale de `site.yaml`.
