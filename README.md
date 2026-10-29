# Plantilla NoExpertise · Tatuajes y barbería

Web cruda en negro, rojo oscuro y hueso para estudios de tatuaje, barberías y piercing, a ancho completo.

- Sectores: tatuajes, barbería, piercing, estudio de tatuaje. Estilo: crudo. Plan mínimo: gratis.
- Secciones: hero, servicios, artistas, proceso, galeria, manifiesto, preguntas, cita, contacto (+ `texto` para apartados nuevos).
- Campos propios: `servicios[]` (nombre, texto, precio, duracion, categoria, destacado), `personas[].estilos` (cadena con comas), `manifiesto.declaracion` y `manifiesto.autor`, `cita.opciones` (zonas del cuerpo con «;»), `boton_formulario` en cita y contacto, `contacto.horario[]` (dia, horas).
- SEO de base incluido (`src/lib/seo.ts`): canónica, og:image, JSON-LD del negocio (`TattooParlor`) y de las preguntas frecuentes, `robots.txt`, `sitemap.xml` y `llms.txt`; `noindex` si `seo.indexable: false`.
- Contenido editable en `site.yaml`; metadatos y guion del asistente en `template.yaml`; reglas para el agente en `CLAUDE.md`; brief de diseño en `DISEÑO.md`; fotos a generar en `fotos.json` (respaldos en `public/placeholders/`).

```
npm ci
npm run dev      # desarrollo
npm run build    # web estática en dist/
```

Basada en [AstroWind](https://github.com/onwidget/astrowind) © onWidget, licencia MIT (`LICENSE-ASTROWIND.md`). Imágenes de relleno (`public/placeholders/`) generadas para esta plantilla, sin licencias de terceros.
