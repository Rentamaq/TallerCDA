# Conexión del bot con la página KPI Taller

- **Página (para ver):** https://rentamaq.github.io/TallerCDA/kpi-taller.html
- **Archivo que alimenta la página:** `kpi-data.json`, en la raíz del repositorio `Rentamaq/TallerCDA`, rama `main`.
- Lectura pública del archivo: https://rentamaq.github.io/TallerCDA/kpi-data.json

La página es estática (GitHub Pages): no recibe datos por la URL. El bot debe **escribir `kpi-data.json` en el repositorio** con la API de GitHub. Cada cambio se publica en ~1 minuto.

## Formato de `kpi-data.json`
```json
{
  "actualizado": "2026-11-25T17:30:00-03:00",
  "reportes": [
    {
      "id": "BOT-20261125-001",
      "reportado_por": "Javier Moroso",
      "hora": "2026-11-25T08:10:00-03:00",
      "equipo": "Excavadora Komatsu PC200",
      "codigo": "EX-06",
      "hora_reporte": "2026-11-25T08:25:00-03:00",
      "detalle": "Falta aceite hidráulico"
    }
  ]
}
```

| Campo | Qué es | Obligatorio |
|---|---|---|
| `id` | Identificador único del reporte (evita duplicados) | Recomendado |
| `reportado_por` | Quién reportó (nombre; **nunca** el teléfono completo, el repo es público) | Sí |
| `hora` | Hora en que ocurrió o se detectó la falla | Opcional (si falta se usa `hora_reporte`) |
| `equipo` | Identificación del equipo (ej. «Excavadora Komatsu PC200») | Sí |
| `codigo` | Código interno (ej. «EX-06»; la página lo normaliza a mayúsculas con guion) | Sí |
| `hora_reporte` | Hora en que se recibió el reporte | Sí |
| `detalle` | Detalle de la falla | Sí |

- Fechas: ISO 8601 con zona de Chile (`-03:00`). También acepta `dd/mm/aaaa hh:mm` o solo `hh:mm` en `hora` (se completa con la fecha del reporte).
- Agregar cada reporte nuevo al final de `reportes` y actualizar `actualizado`. No borrar reportes anteriores: son el historial de los KPI.

## Cómo escribir el archivo (API de GitHub)
1. **Token**: un *fine-grained personal access token* creado por un administrador de la organización Rentamaq, con acceso **solo** al repositorio `Rentamaq/TallerCDA` y permiso **Contents: Read and write**. Guardarlo como secreto del bot (nunca en el código ni en el repositorio).
2. **Leer** el archivo actual y su `sha`:
   `GET https://api.github.com/repos/Rentamaq/TallerCDA/contents/kpi-data.json?ref=main`
   (cabeceras: `Authorization: Bearer <TOKEN>`, `Accept: application/vnd.github+json`). El contenido viene en base64 en `content`.
3. **Agregar** el reporte nuevo al arreglo `reportes` y actualizar `actualizado`.
4. **Escribir**:
   `PUT https://api.github.com/repos/Rentamaq/TallerCDA/contents/kpi-data.json`
   ```json
   { "message": "Bot: nuevo reporte EX-06", "content": "<JSON completo en base64>", "sha": "<sha del paso 2>", "branch": "main" }
   ```
5. Si responde **409** (el archivo cambió entre medio), repetir desde el paso 2.

Recomendación: agrupar varios reportes por escritura (por ejemplo cada 5–15 minutos) en vez de un commit por mensaje.
