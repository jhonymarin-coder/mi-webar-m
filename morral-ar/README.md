# Morral AR — Web AR de reconocimiento de imagen

Esta web activa un modelo 3D animado cuando la cámara del celular reconoce
el frente de tu morral. Usa **MindAR** (reconocimiento de imagen) + **A-Frame**
(motor 3D), corre 100% en el navegador, sin apps ni instalaciones.

## Estado actual

✅ Estructura de la web lista y funcionando
✅ Modelo 3D real (carro de carreras, .glb) integrado, escalado y con animación de giro
✅ Marcador AR (`targets/morral.mind`) compilado desde la foto real del morral
🎉 **Proyecto completo — listo para probar y publicar**

### Nota sobre licencia del modelo 3D
El modelo de carro viene de un banco de modelos gratuitos (Poly Pizza /
Quaternius). Revisa la licencia específica del modelo que descargaste: la
mayoría son CC0 (uso libre) pero algunas requieren dar crédito al autor en
la web o en la descripción. Si la tuya lo requiere, dime y te ayudo a
agregar un pequeño crédito discreto en la esquina de la pantalla.

## Cómo probarlo YA (con el modelo de prueba)

Necesitas HTTPS o localhost para que el navegador permita usar la cámara.
Opción más simple:

```bash
cd morral-ar
npx serve .
```

Abre la URL que te dé (algo como `http://localhost:3000`) desde el celular
(en la misma red WiFi que tu computador, o usando un túnel como `ngrok`),
o directamente desde el computador si tiene webcam.

⚠️ Ahora mismo, como aún no existe `targets/morral.mind`, la cámara se abrirá
pero NO reconocerá nada todavía. Ese archivo se genera en el siguiente paso.

## Paso 1 — Generar el marcador (target) desde tu foto

1. Ve a: https://hiukim.github.io/mind-ar-js-doc/tools/compile
2. Sube la foto del frente del morral (la que ya tienes lista).
   - Buena luz, sin reflejos, imagen nítida y de frente.
   - Entre más textura/detalle visual tenga el morral (logos, costuras,
     colores variados), mejor lo reconoce. Superficies lisas de un solo
     color cuestan más trabajo.
3. El compilador te muestra un puntaje de "features" detectados — mientras
   más alto, mejor.
4. Descarga el archivo `targets.mind`.
5. Renómbralo a `morral.mind` y reemplaza el archivo en la carpeta `targets/`.

## Paso 2 — (Opcional) Poner tu modelo 3D real

Si tienes un archivo `.glb` con tu modelo animado:

1. Ponlo en `assets/modelo.glb`
2. Abre `index.html` y:
   - Descomenta la línea `<a-asset-item id="modeloMorral" ...>` dentro de `<a-assets>`
   - Descomenta el bloque `<a-gltf-model ...>` marcado como "MODELO REAL"
   - Borra o comenta el bloque marcado como "PLACEHOLDER"
3. Ajusta `scale` y `position` según el tamaño real de tu modelo (lo normal
   es que necesites achicarlo bastante, la mayoría de exportadores de
   Blender/Sketchfab generan modelos grandes).

Si no tienes un modelo `.glb` todavía, dímelo y te ayudo a conseguir uno
gratuito (ej. Sketchfab con licencia libre) o a generarlo.

## Paso 3 — Publicar en GitHub Pages

1. Crea un repositorio nuevo en GitHub (puede ser público).
2. Sube todo el contenido de esta carpeta (`index.html`, `assets/`, `targets/`).
3. Ve a **Settings → Pages** del repositorio.
4. En "Source" elige la rama `main` y la carpeta `/ (root)`.
5. Guarda. GitHub te dará una URL tipo:
   `https://tu-usuario.github.io/tu-repo/`
6. Esa URL ya es HTTPS automáticamente (GitHub Pages lo da gratis), así que
   la cámara funcionará sin problema desde cualquier celular.

## Estructura del proyecto

```
morral-ar/
├── index.html          ← toda la lógica de la web AR
├── assets/
│   └── modelo.glb       ← (aquí va tu modelo 3D cuando lo tengas)
├── targets/
│   └── morral.mind       ← (aquí va el marcador generado desde tu foto)
└── README.md
```

## Notas

- Funciona en Chrome/Safari móviles modernos. iOS necesita Safari 15+.
- Si el modelo no aparece alineado con el morral, ajusta `position` y
  `scale` del `<a-entity>` dentro de `index.html`.
- Puedes tener varios morrales/objetos distintos usando varias imágenes
  target — pídeme ayuda si quieres esa versión más adelante.
