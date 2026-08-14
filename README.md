# Violencia Laboral — Módulo de carga (PWA) · IPEC Misiones

Aplicación web de carga para el registro estadístico de violencia laboral.
IPEC — Observatorio de Violencia Familiar y de Género. Instrumento: matriz v2.1
(diccionario de 6 bloques; catálogos D-01 a D-11).

**Sin datos identificatorios.** El módulo no tiene campos para nombres, DNI,
CUIL ni contactos; las personas se registran como V1, V2… / S1, S2…, y los
campos libres tienen un detector que advierte si se pega un dato identificatorio.
Los tres casos embebidos como "juego de prueba" son **ficticios** (4700-9001,
9002 y 9003): los expedientes reales nunca viajan en este repositorio ni en la
aplicación publicada; residen solo en el equipo institucional que los carga.

## Archivos

| Archivo | Función |
|---|---|
| `index.html` | La aplicación completa (pantallas, catálogos, validaciones, exportación) |
| `manifest.webmanifest` | Permite instalarla como aplicación |
| `sw.js` | Funcionamiento sin conexión (caché `vl-v1`) |
| `icon-192.png`, `icon-512.png`, `icon-maskable-512.png` | Ícono |

Los cuatro primeros deben quedar **en la misma carpeta**, sin subcarpetas.

## Publicación (GitHub Pages, igual que el Relevamiento Vial)

1. Crear repositorio público (sugerido: `carga-vl`).
2. **Uploading an existing file** → arrastrar los seis archivos → **Commit**.
3. **Settings → Pages** → *Deploy from a branch* → `main` / root → **Save**.
4. En 1–2 minutos queda en `https://USUARIO.github.io/carga-vl/`.

El `index.html` incluye `noindex,nofollow`: la dirección funciona pero no se
indexa en buscadores. Migrar más adelante a un servidor institucional es
copiar estos mismos archivos (y, si cambia la ruta, nada más).

## Actualizar la aplicación

Si se modifica `index.html`, abrir `sw.js` y subir la versión
(`vl-v1` → `vl-v2`). Sin ese cambio los equipos siguen usando la copia en caché.

## Flujo de datos (supuestos 17 y 18 del rediseño)

- Carga en equipos institucionales del IPEC; datos solo en `localStorage`
  del equipo (claves `vl_cfg`, `vl_exps`). Nada se envía a ningún servidor.
- Exportación: tres CSV (separador `;`) espejo de las hojas 4–6 de la matriz
  v2.1, con los casos PRUEBA excluidos; respaldo/consolidación por JSON.
- Entrega únicamente por correo institucional; nunca mensajería personal.
- Pestaña **Datos → Verificar exportación**: compara la salida con el patrón
  embebido (regresión del exportador).

## Catálogo de municipios (D-11)

Embebido con las 79 unidades vigentes según cartografía IPEC 2026 (más las
categorías operativas "Fuera de la provincia" y "Sin dato"); el bloque
`var MUNIS` de `index.html` permite agregar o quitar entradas en un minuto.
Pendiente menor (no bloquea la carga: la matriz almacena la etiqueta): volcar
los códigos de gobierno local (Res. 89/2019 / georef) por join automático,
p. ej. `https://apis.datos.gob.ar/georef/api/municipios?provincia=54&max=100`,
y cotejar el listado con el dataset "Municipios" de la Subsecretaría de
Ordenamiento Territorial en `datos.misiones.gob.ar`.
