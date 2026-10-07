# Sistema completo — lectura técnica rápida

## Propósito

El sistema asiste la preparación y carga de recursos de mantenimiento. La inteligencia artificial se usa para **interpretar, recuperar y estructurar**, mientras que la autoridad operativa se conserva en validadores determinísticos, fuentes maestras y confirmación humana.

## 1. Entrada

La solicitud puede originarse en:

- interfaz web;
- texto escrito;
- canal de voz cuando se valida ASR;
- panel ESP32-S3-4848S040 mediante Device API.

La entrada se transforma en una intención estructurada. Ninguna entrada tiene autoridad directa para escribir en la fuente de verdad.

## 2. Recuperación RAG

El flujo local documentado utiliza:

- **Ollama** para inferencia local;
- **Qwen3 8B** como modelo de lenguaje;
- **nomic-embed-text** para embeddings;
- recuperación top-k sobre inventario;
- proyección/visualización de inventario mediante UMAP cuando corresponde.

La recuperación semántica sirve para localizar candidatos. No sustituye la comprobación de IDs.

## 3. Plan estructurado

La salida útil del modelo se expresa como un plan o contrato estructurado. El objetivo es convertir una solicitud ambigua en campos verificables:

```text
intención
  ├─ tarea candidata
  ├─ recurso candidato
  ├─ cantidades / horas cuando corresponde
  ├─ fuente/evidencia
  └─ operación propuesta
```

El plan todavía **no es una escritura autorizada**.

## 4. Validación determinística

Antes de mostrar una propuesta como ejecutable se comprueba:

- existencia del TareaId;
- existencia del recurso en su catálogo;
- correspondencia entre tipo de recurso y campos permitidos;
- reglas de negocio;
- duplicados;
- permisos;
- estado vigente del origen;
- idempotencia / repetición de una operación;
- integridad de la vista previa antes de confirmar.

Si cambia la fuente entre vista previa y confirmación, la operación debe detenerse o volver a validarse.

## 5. Human-in-the-loop

La persona revisa la vista previa y puede:

- confirmar;
- corregir;
- rechazar;
- pedir aclaración si la recuperación fue ambigua.

La arquitectura separa **propuesta probabilística** y **autoridad de persistencia**.

## 6. Persistencia y auditoría

Después de la confirmación:

1. se vuelve a comprobar el estado necesario;
2. se ejecuta la escritura en el destino controlado;
3. se registra el resultado;
4. la auditoría conserva la relación solicitud → plan → IDs → operación → resultado.

El registro estructurado permite reconstruir qué se propuso, qué se aceptó y qué ocurrió finalmente.

## 7. Canal ESP32

El panel físico opera como interfaz, no como base de decisión.

```text
ESP32
  ↓ POST command
Device API
  ↓
pending_confirmation
  ↓
revisión humana
  ├─ applied
  └─ rejected
  ↓ polling
ESP32 muestra el estado
```

El firmware usa la Device API y consulta el estado periódicamente. El panel no debe escribir directamente en Excel ni saltar la confirmación.

## 8. Relación con el sistema de mantenimiento

La unidad técnica central es la asociación **tarea ↔ recurso**. La fuente maestra determina identificadores y categorías válidas; el RAG ayuda a recuperar contexto y candidatos.

Ejemplos de recursos:

- materiales;
- herramientas;
- maquinaria;
- mano de obra / Labour1 cuando corresponde al modelo de datos.

## 9. Componentes por repositorio

### `erp-mantto-esp32`

Contiene la capa embebida y su validación:

- ESP32-S3-4848S040;
- ST7701S;
- GT911;
- firmware PlatformIO;
- configuración ESPHome/LVGL;
- Device API contract;
- pruebas Python/C++;
- CI/CD;
- validación física separada.

### `asistente-3c`

Contiene el monitor y la integración de comandos:

- React + Express;
- vista previa;
- confirmación humana;
- API para ESP32;
- estados de comando;
- controles de columnas y catálogos.

### Módulo RAG local

El módulo RAG documentado incorpora React, FastAPI, Ollama, embeddings, lectura de inventario, proyección, planes y auditoría. En este repositorio de presentación se describe su función sin publicar secretos ni rutas locales.

## 10. Qué debe poder explicar el asesor en una sola lectura

La tesis no plantea que “la IA decide y escribe”. Plantea una cadena controlada:

> **La IA interpreta → el RAG recupera → el backend valida → el especialista confirma → el sistema registra y audita.**

Ese es el núcleo funcional y metodológico del proyecto.
