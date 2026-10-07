# Metodología y validación

## Diseño

La evaluación propuesta utiliza un diseño preexperimental con un solo grupo de casos y observaciones apareadas antes/después:

```text
O1  →  X  →  O2
manual   solución RAG
```

Cada caso debe conservar identidad, datos iniciales y reglas comparables.

## Muestra

- muestra intencional prevista: **N = 360 casos**;
- verificación preliminar: **20 casos críticos**;
- casos válidos, ambiguos, inexistentes, duplicados, cancelados y con restricciones de permisos.

Los 20 casos críticos no sustituyen la muestra principal: sirven como filtro previo de condiciones necesarias.

## Indicadores

| Dimensión | Indicador |
|---|---|
| Eficiencia | tiempo por operación |
| Exactitud | tarea/recurso correctamente resuelto |
| Integridad referencial | IDs válidos / total |
| Duplicados | duplicados no autorizados |
| Trazabilidad | operaciones con registro completo |
| Retrabajo | requiere corrección / no requiere corrección |

## Tratamiento estadístico

### Tiempo

- mediana;
- rango intercuartílico;
- pares manual vs. prototipo;
- prueba no paramétrica **Wilcoxon**.

### Retrabajo

- variable dicotómica;
- pares antes/después;
- prueba **McNemar**.

## Condiciones de latencia

Cuando el modelo o los recursos requieren carga inicial se deben distinguir:

- ejecución fría;
- ejecución caliente.

Mezclarlas puede sesgar la interpretación del tiempo.

## Evidencia

Cada observación debe poder relacionarse con:

- `case_id`;
- versión/configuración de la fuente;
- entrada;
- propuesta;
- evidencia recuperada;
- IDs resueltos;
- validación;
- decisión humana;
- resultado;
- latencia;
- registro de auditoría.

## Validación por capas

```text
Documentación
    ↓
Implementación
    ↓
Pruebas automatizadas
    ↓
CI/CD
    ↓
Integración extremo a extremo
    ↓
Validación física (si pertenece al alcance aprobado)
```

Cada nivel responde una pregunta diferente. No se debe inferir validación física a partir de CI.

## Criterio para cerrar resultados

Un resultado se considera listo para discusión cuando existe:

1. caso identificado;
2. medición manual;
3. medición con intervención;
4. misma regla de aceptación;
5. evidencia de salida;
6. trazabilidad suficiente para repetir o auditar la comparación.
