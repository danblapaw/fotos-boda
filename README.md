# Fotos de la boda

Web de una sola página para que los invitados hagan fotos con su móvil, las suban a una nube compartida y descarguen las que quieran.

- **Hacer una foto** → abre la cámara del móvil → *Subir a la nube* o *Descartar*.
- **Ver todas las fotos** → galería con todas las fotos subidas.
- Las fotos que subes tú aparecen marcadas como **Tuya** y puedes **borrarlas durante los 10 minutos** siguientes a subirlas (límite de Cloudinary sin servidor). Pasado ese plazo, solo los novios pueden borrarlas desde la Media Library.
- Cada foto tiene botón de **descarga** (en iPhone abre la hoja de compartir → "Guardar imagen"; en Android se descarga directamente).

No necesita servidor: la web vive en GitHub Pages y las fotos en Cloudinary (plan gratuito).

---

## 1. Configurar la nube (Cloudinary) — 5 minutos

1. Crea una cuenta gratuita en https://cloudinary.com
2. En el **Dashboard** copia tu **Cloud name**.
3. **Settings → Upload → Upload presets → Add upload preset**
   - Signing mode: **Unsigned**
   - Preset name: `boda_unsigned`
   - Folder: `boda` (opcional, para tenerlas ordenadas)
   - Pestaña **Advanced** del preset: activa **"Return delete token"** (necesario para que cada invitado pueda borrar sus propias fotos).
   - Guarda.
4. **Settings → Security → Restricted media types**: **desmarca "Resource list"** y guarda.
   (Sin esto la galería no puede listar las fotos.)

## 2. Poner tus datos en la web

Abre `index.html` y edita el bloque `CONFIG` del principio del script:

```js
const CONFIG = {
  cloudName:    "ioxxv1uq",
  uploadPreset: "boda_unsigned",
  tag:          "boda",
  titulo:       "Nuestra Boda",
  subtitulo:    "Haz fotos y compártelas con todos"
};
```

## 3. Publicarla en GitHub Pages

1. Crea un repositorio nuevo en GitHub (público), por ejemplo `fotos-boda`.
2. Sube `index.html` (y este README) a la rama `main`.
3. **Settings → Pages → Source: Deploy from a branch → main / (root) → Save**.
4. En 1-2 minutos tendrás la web en:
   `https://TU_USUARIO.github.io/fotos-boda/`

**Ese es el enlace que hay que mandar a los invitados**, no el del repositorio (el del repo enseña el código, no la web). Genera también un QR con ese enlace para ponerlo en las mesas.

## Notas

- La lista de fotos de Cloudinary se cachea ~1 minuto: una foto recién subida por otra persona puede tardar un poco en aparecer (pulsa ↻). Las tuyas aparecen al instante.
- Las fotos se reducen a 2560 px antes de subirlas: calidad de sobra para el móvil e incluso para imprimir, y la subida es mucho más rápida con la cobertura del banquete.
- Cualquiera con el enlace puede subir y ver fotos. Para una boda es lo práctico; simplemente no lo publiques en abierto.
- Para descargar todas las fotos de golpe después de la boda: Cloudinary → Media Library → carpeta `boda` → seleccionar todo → Download.
- Prueba antes del día: sube 2-3 fotos desde un iPhone y un Android, descárgalas, y luego bórralas desde la Media Library.
