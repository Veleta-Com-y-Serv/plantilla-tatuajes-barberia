# Plantilla «Tatuajes y barbería» (NoExpertise)

Web estática Astro 5 + Tailwind 4, derivada de AstroWind (MIT, ver `LICENSE-ASTROWIND.md`). Estilo: **crudo**
(negro tinta, rojo oscuro y hueso; grano de papel en las bandas, bordes dentados de sello entre bandas, titulares en
slab serif pesada del sistema y etiquetas en mayúsculas muy espaciadas). Todo a ancho completo: cada sección es una
banda de borde a borde. Todo en castellano de España, frases cortas, sin jerga. El brief de diseño está en `DISEÑO.md`.

## Dónde está cada cosa
- **Textos, contacto, menú, SEO y secciones**: `site.yaml` (raíz). Es la única fuente de contenido. `src/data/site.ts` lo carga y lo tipa; no pongas textos fijos en los componentes.
- **Colores**: `site.yaml → colores` (primario, acento, fondo, texto). `src/layouts/Base.astro` los convierte en variables CSS (`--c-primario`…) y Tailwind los expone como `bg-primario`, `text-acento`…
  - `fondo` = negro tinta de las bandas oscuras; `texto` = hueso. Las bandas claras («hueso») son esos dos invertidos: si el cliente pide fondo claro, cambia `fondo` y `texto` y todo se invierte sin romperse.
  - `primario` = rojo oscuro de las bandas de color (cinta de la portada, «Cómo trabajamos», mitad izquierda de «Pide cita», letrero vertical de la portada). La letra encima se calcula sola (`--sobre-primario`).
  - `acento` = rojo vivo de botones, rayas de antetítulos y estrellas. La letra encima se calcula sola (`--sobre-acento`); sobre negro se usa una mezcla más clara (`--rojo-claro`) para que se lea.
- **Tipografías y aspecto general**: `src/styles/global.css` (`--fuente-titulos`: "Rockwell Extra Bold", "Rockwell", "Roboto Slab"… sin negrita sintética; bandas `.banda-tinta`, `.banda-hueso`, `.banda-roja`, `.banda-negra`; `.grano` (textura); `.dentado` (dientes de sello arriba de la banda); `.antetitulo`; botones `.btn` (bloque con doble filete) y `.btn-sec`; cabecera fija `.cabecera--tinta` con alto `--alto-cabecera`; pie `.pie--tinta`). Fuentes del sistema: no añadas fuentes externas.
- **Imágenes**: en `public/`. Las fotos van en `public/fotos/` (lista y descripción en `fotos.json`); cada una tiene su respaldo `public/placeholders/<mismo nombre>.svg`, que `Imagen.astro` enseña si la foto falta. En `site.yaml` se referencian con ruta absoluta (`/fotos/hero.jpg`). Fotos de personas: `/placeholders/persona.svg` (no se generan caras).
- **Logo**: `site.yaml → logo` (ruta en `public/`); vacío = inicial en un sello rojo + nombre.
- **Pie «Web creada con NoExpertise»**: `site.yaml → marca_pie`. El pie repite contacto, horario (de `secciones.contacto.horario` o `contacto.horario`), menú, redes y el botón de la cabecera.

## Secciones
Cada sección es un componente que solo se pinta si `site.yaml → secciones.<id>.activa` es `true`. Se pintan en el orden en que aparecen en `site.yaml`.
- `hero` → `hero.astro`: portada partida a sangre (texto sobre negro a la izquierda, `imagen` hasta el borde derecho con la localidad en vertical), `titulo` enorme (mejor 3-6 palabras), `texto`, `cta`, `cta_secundario` e `items: [{titulo, icono}]` en una cinta roja de borde a borde. Sin foto, el texto ocupa todo el ancho.
- `servicios` → `servicios.astro`: banda hueso con franja de foto a sangre arriba (`imagen`, opcional) y la lista de precios `servicios: [{nombre, texto, precio, duracion, categoria, destacado}]`, agrupada por `categoria` en columnas (hasta 3). `precio` siempre texto (`"desde 60 €"`, `"Consultar"`); vacío = no se pinta. `destacado: true` = estrella roja. `nota` y `cta` opcionales. No inventes precios.
- `artistas` → `artistas.astro`: retratos de borde a borde sin márgenes (hasta 4 columnas): `personas: [{nombre, cargo, estilos, foto, texto}]`; `estilos` es **una cadena** con comas («Blackwork, línea fina»).
- `proceso` → `proceso.astro`: banda roja con los pasos `items: [{titulo, texto, icono}]` numerados (hasta 4 columnas).
- `galeria` → `galeria.astro`: `galeria: [ruta…]` en mosaico de borde a borde (la 1.ª grande; las últimas se ensanchan para cerrar filas) + `cta` opcional (p. ej. a Instagram).
- `manifiesto` → `manifiesto.astro`: banda hueso con la frase de la casa (`declaracion`) en grande y su firma (`autor`). Sin `declaracion`, pinta `titulo` y `texto`.
- `preguntas` → `preguntas.astro`: cuidados y preguntas frecuentes, partida 50/50 con `imagen` a sangre a la izquierda y acordeón `details/summary` (`preguntas: [{pregunta, respuesta}]`); sin preguntas no se pinta.
- `cita` → `cita.astro`: partida 50/50: rojo con titular, `items: [{titulo, texto}]` (qué contar), botón de WhatsApp (sale solo de `contacto.whatsapp`), `cta` opcional y `nota`; negro con el formulario de cita (servicio, zona del cuerpo de `opciones` —**cadena con «;»**—, tamaño, fecha preferida e idea). `boton_formulario` opcional.
- `contacto` → `contacto.astro`: teléfono enorme y datos de `contacto`, tablilla de horario (`horario: [{dia, horas}]`, o `contacto.horario` si no hay lista) y formulario corto (nombre, teléfono, email, servicio y mensaje). `boton_formulario` opcional.
- `texto` → `texto.astro`: apartado genérico (párrafos, `imagen` a sangre 50/50, `items`, `cta`). Para apartados nuevos: `tipo: texto`.

## Reglas para órdenes
1. **Activar o quitar una sección**: cambia `activa: true|false` en `site.yaml`. No borres componentes.
2. **Reordenar secciones**: mueve el bloque dentro de `secciones:` en `site.yaml`. Conviene alternar bandas oscuras, rojas y hueso.
3. **Cambiar textos, teléfonos, horarios, fotos**: solo en `site.yaml`. Si un texto contiene comas o dos puntos dentro de `{ … }`, ponlo entre comillas (las horas, siempre: `horas: "10:00 a 15:00"`).
4. **Listas planas**: nunca una lista dentro de un elemento de lista (los servicios son una lista con su `categoria`, no categorías con servicios dentro; los estilos de un artista y las zonas del cuerpo son cadenas). Precios siempre como texto entre comillas. Máximo 24 elementos por lista.
5. **Página nueva**: crea `src/pages/<slug>.astro` usando `import Base from '../layouts/Base.astro'` y `<Base titulo="…" descripcion="…">…</Base>`; enlázala en `site.yaml → menu` (`{ texto: …, url: "/<slug>" }`). Ejemplo: `src/pages/aviso-legal.astro`.
6. **Sección nueva**: mejor un apartado con `tipo:` (`tipo: texto`, `tipo: servicios`, `tipo: galeria`…) y su propio id. Si hace falta un diseño nuevo, crea `src/components/secciones/<id>.astro` con `seccion(Astro.props.id)` y una banda de borde a borde (`banda-*`, `grano`, `dentado`). `src/pages/index.astro` la recoge sola: no lo toques.
7. **No tocar** `src/layouts/Base.astro`, `src/pages/index.astro`, `tailwind.config.mjs` ni `src/styles/comun.css` salvo orden explícita de diseño. Los ids `hero` y `contacto` son obligatorios. Tampoco `src/lib/seo.ts` ni `src/pages/robots.txt.ts`, `sitemap.xml.ts` y `llms.txt.ts`: son el SEO de base (canónica, og:image, `noindex` si `seo.indexable: false`, JSON-LD del negocio —`TattooParlor`— y de las preguntas, robots, sitemap y llms.txt), salen solos de `site.yaml` y el fichero es el mismo en todas las plantillas. `seo.url` y `seo.indexable` los pone la plataforma: no los cambies.
8. Mantén: `lang="es-ES"`, imágenes con `Imagen.astro` (carga diferida y respaldo), sin JavaScript nuevo salvo necesidad real, 16 px de margen lateral del texto (`.contenedor`; fotos y fondos tocan el borde), sin scroll horizontal en móvil, botones de 44 px de alto como mínimo. Imágenes de contenido con `alt` sacado del contenido (`altHero`, `altFicha`, `altGaleria`, `altSeccion` de `src/lib/seo.ts`, o el `nombre` de la persona); las decorativas, `alt=""` (Imagen.astro les pone `aria-hidden`).
9. El formulario no tiene servidor: abre el correo (`mailto`) con el email de `site.yaml`. Para envío real, cambia `action` en `src/components/ui/FormularioContacto.astro`.
10. Iconos disponibles: ver `src/components/ui/Icono.astro` (del sector: `navaja, tijeras, maquina, aro, aguja, lapiz, escudo, gota, mensaje, reloj`…).

## Construir
```
npm ci && npm run build      # resultado en dist/
npx astro preview            # ver dist/ en http://localhost:4321
```
Antes de dar una orden por buena: `npm run build` sin errores.
