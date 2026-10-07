# Fuentes y trazabilidad de la presentación

Este repositorio funciona como **capa de presentación para asesoría**. No reemplaza los repositorios técnicos canónicos ni duplica innecesariamente su árbol completo. Resume el sistema, enlaza evidencia existente y conserva la separación entre diseño, implementación, pruebas y validación física.

## 1. Repositorio técnico del panel y firmware

**Repositorio:** `wpv10barza/erp-mantto-esp32`  
**Rama:** `main`

Referencias documentales revisadas para esta presentación:

| Commit | Propósito |
|---|---|
| `0559d74a1a629a8ee1ab1ded12db047bae7acdc5` | documenta compilación del firmware, arquitectura RGB, ST7701S, artefactos y frontera con validación física |
| `6bbd51db59c32b0c478a21dcac12eaf93d3f70ef` | separa condiciones iniciales, diseño, integración, implementación y validación |
| `bec07bbcce72fa8a4cb9d831c7a04e5d48e46f1d` | corrige referencias de capítulos y jerarquía de pruebas/evidencia |

Última referencia revisada de esa secuencia: `bec07bbcce72fa8a4cb9d831c7a04e5d48e46f1d`.

### Imágenes técnicas reutilizadas

Las imágenes mostradas en el README de presentación provienen del mismo árbol técnico usado en la presentación:

| Imagen | Archivo fuente | Blob SHA |
|---|---|---|
| Panel ESP32-S3-4848S040 | `docs/images/esp32-s3-4848s040/fig13_panel_base.png` | `0e41a3e61d8da1077a4ffcd28295ec1b761493c0` |
| Subsistemas y periféricos | `docs/images/esp32-s3-4848s040/fig14_subsystems.png` | `971ee7d6609339c7719a20188a66b63a525c7878` |
| Flujo de validación | `docs/images/esp32-s3-4848s040/fig16_validation_flow.png` | `542ceb4d10668c87efa1d1b937bfdd0a9e1737c9` |

No se presentan estas figuras como evidencia de funcionamiento físico; su función es explicar arquitectura, subsistemas y método de validación.

## 2. Monitor y Device API

**Repositorio:** `wpv10barza/asistente-3c`

Elementos usados en la síntesis:

- React + Express;
- entrada por texto/voz;
- vista previa antes de persistir;
- confirmación humana;
- Device API para ESP32;
- estados `pending_confirmation`, `applied` y `rejected`;
- controles determinísticos sobre campos y catálogos.

La Device API sirve de puente entre el panel y la capa de revisión. Una respuesta HTTP aceptada no equivale a una escritura aprobada.

## 3. Módulo RAG local

La presentación incorpora el funcionamiento documentado del módulo RAG local:

- React;
- FastAPI;
- Ollama;
- Qwen3 8B;
- `nomic-embed-text`;
- recuperación top-k;
- proyección UMAP cuando corresponde;
- generación de planes estructurados;
- validación contra fuentes maestras;
- confirmación humana;
- auditoría.

Por seguridad, esta capa de presentación **no publica claves, rutas locales personales ni datos operativos sensibles**.

## 4. Material de la presentación

La estructura del repositorio se adaptó al material de exposición preparado para la asesoría:

1. problema operativo;
2. objetivo y aporte RAG híbrido;
3. unidad de análisis tarea–recurso;
4. arquitectura técnica;
5. panel y subsistemas ESP32;
6. separación software/hardware;
7. diseño preexperimental;
8. Wilcoxon y McNemar;
9. estado actual de resultados;
10. recorrido de un caso;
11. alcance y limitaciones;
12. preguntas al asesor.

El discurso no se copió literalmente al README. Se convirtió en documentación de lectura rápida y en una guía separada de 15 minutos.

## 5. Regla de evidencia

La presentación conserva esta jerarquía:

```text
documentación
   ↓
implementación
   ↓
pruebas automatizadas
   ↓
CI/CD
   ↓
integración extremo a extremo
   ↓
validación física
```

Un nivel no sustituye al siguiente. En especial:

- tener código no demuestra que fue ejecutado;
- compilar no demuestra operación física;
- CI no demuestra pantalla/táctil/USB reales;
- una propuesta RAG no equivale a un ID válido;
- una vista previa no equivale a una escritura confirmada.

## 6. Uso durante la reunión

Para una explicación breve:

- abrir primero `README.md`;
- usar `docs/GUIA_REUNION_15_MIN.md` como secuencia oral;
- abrir `docs/SISTEMA_COMPLETO.md` solo si el asesor solicita detalle;
- revisar `docs/METODOLOGIA_VALIDACION.md` para metodología;
- cerrar con `docs/ESTADO_Y_PREGUNTAS.md`.

Así el repositorio mantiene una lectura rápida para el asesor y deja el detalle técnico en los repositorios canónicos.
