# Estudio Jurídico Rietman

Web institucional estática, sin servicios externos de tipografías, analítica, formularios ni base de datos. Node.js 24 disponible en el entorno. No necesita instalar paquetes para ejecutar o construir.

## Revisar

Desde este directorio:

```sh
npm run dev
```

Abrir el puerto 5173 en un navegador cuando el entorno permita acceso. En una computadora propia, abrir http://localhost:5173. Las capturas de revisión están en `revision/` (archivos locales ignorados por Git).

```sh
npm run check
npm run build
```

La construcción copia los archivos estáticos a `dist/`. Para servir esa construcción: `cd dist && node ../scripts/serve.mjs`.

## Actualizar

- `src/content.js`: datos de contacto, mensajes de WhatsApp, áreas y preguntas frecuentes. El número argentino móvil usa 549 y el número sin 0 ni 15. No se muestra teléfono de llamadas hasta confirmarlo por separado.
- `index.html`: presentación, sobre el estudio y pasos de consulta.
- `src/style.css`: diseño adaptable.
- Sin fotografías, redes ni mapa hasta contar con material o indicaciones. No se presumen días de atención.

El nombre profesional y del estudio en encabezados y presentación están también en `index.html`. Actualizarlos allí si cambian.

## Publicar, solo después de la aprobación

1. Revisar contenido, matrícula, horarios y datos de contacto; probar el WhatsApp real y confirmar que corresponde al estudio.
2. Cambiar `contact.confirmed` a `true` en `src/content.js` para retirar el aviso de muestra.
3. Ejecutar `npm run check` y `npm run build -- --publish`. Este último bloquea la construcción pública si falta la confirmación o algún dato requerido.
4. Subir **solo `dist/`** a un alojamiento estático, por ejemplo Netlify o Cloudflare Pages. También puede conectarse el repositorio, con construcción `npm run build -- --publish` y carpeta de salida `dist`. No se ha contratado ni configurado ningún proveedor. Sus planes gratuitos pueden servir para esta web; revisar límites y precios vigentes.
5. Para un dominio propio, registrarlo con un proveedor (tiene costo y renovación, variables según extensión y proveedor). Agregar el dominio en el alojamiento y configurar los registros DNS que este indique. Activar/verificar HTTPS y redirección entre www y el dominio principal.
6. Revisar en el dominio real la navegación, WhatsApp, correo y visualización móvil.

La carpeta del repositorio contiene los cambios locales. No se han enviado a GitHub ni publicado. Para conservarlos allí, revisar el diff, hacer commit y push a la rama elegida mediante el flujo habitual del repositorio.

## Comprobación de navegador opcional

`scripts/verify.cjs` usa Playwright y Chromium disponibles en este entorno. Fuera del entorno requiere Playwright instalado y un navegador Chromium; las rutas pueden configurarse con `PLAYWRIGHT_MODULE` y `CHROMIUM_PATH`. Comprueba tamaños de pantalla, menú, preguntas frecuentes, mensajes preparados y errores JavaScript. No envía mensajes de WhatsApp.
