# Guía de reunión con el Dr. Ing. Freedy Sotelo Valer — 15 minutos

> Objetivo: presentar el problema, el funcionamiento y la metodología sin leer capítulos completos.  
> Estado administrativo: el docente manifestó disponibilidad para asumir la asesoría; la formalización institucional se gestiona por la vía correspondiente.

## 0:00–0:45 · Apertura

**Mostrar:** título de tesis y objetivo de la reunión.

**Decir:**

“Buenos días, ingeniero Sotelo. Muchas gracias por su tiempo y por su disposición para apoyarme con la asesoría. Quisiera presentarle de manera breve la problemática, el funcionamiento de la solución y la forma en que planteo validarla. Mi objetivo hoy es recibir su orientación para dejar correctamente delimitado el alcance y priorizar las pruebas.”

## 0:45–2:00 · Problema

**Mostrar:** flujo manual y ejemplo de relación tarea–recurso.

**Idea clave:** preparar recursos exige revisar fuentes, resolver nombres ambiguos y comprobar identificadores antes de cargar.

**Decir:**

“El problema aparece al relacionar una tarea de mantenimiento con materiales, herramientas, maquinaria o recursos de trabajo. Una descripción parecida no basta para afirmar que se trata del recurso correcto. Si se carga sin verificar, pueden aparecer duplicados, omisiones o retrabajo.”

## 2:00–3:15 · Objetivo y aporte

**Mostrar:** RAG híbrido = recuperación + control.

**Decir:**

“La propuesta utiliza RAG para recuperar contexto y elaborar una propuesta, pero la IA no recibe autoridad de escritura. Los identificadores y reglas se validan fuera del modelo, y el especialista confirma antes de registrar.”

## 3:15–5:15 · Arquitectura

**Mostrar:** diagrama del README.

Recorrer:

1. interfaz React;
2. FastAPI;
3. embeddings;
4. Ollama / Qwen3;
5. plan estructurado;
6. validación determinística;
7. vista previa;
8. confirmación;
9. escritura y auditoría.

**Frase de cierre:** “La separación principal es interpretación probabilística frente a control determinístico.”

## 5:15–6:30 · Unidad de análisis

**Mostrar:** imagen de la tabla de estrategias.

**Decir:**

“La unidad de trabajo que quiero medir es una relación tarea–recurso. El TareaId mantiene la referencia a la tarea y el recurso se resuelve contra su catálogo. Esto permite detectar duplicados y revisar cada relación por separado.”

## 6:30–8:00 · Canal ESP32

**Mostrar:** mapa técnico y mapa de subsistemas.

**Decir:**

“El ESP32 funciona como canal de interacción. Envía la orden a la Device API y recibe estados. No aplica el cambio directamente. La pantalla, el táctil y la comunicación tienen una validación física separada de las pruebas de software.”

## 8:00–9:30 · Validación

**Mostrar:** mapa de compilación/carga/validación.

**Decir:**

“Distingo documentación, implementación, pruebas automáticas, CI y validación física. Una compilación exitosa no demuestra que la pantalla y el táctil funcionen en el equipo real.”

## 9:30–11:00 · Metodología

**Mostrar:** esquema pretest/postest.

Puntos:

- casos apareados;
- diseño preexperimental;
- 360 casos previstos;
- 20 casos críticos antes de la muestra completa;
- tiempo, exactitud, integridad, duplicados, trazabilidad y retrabajo.

## 11:00–12:00 · Estadística

**Decir:**

“Para tiempos usaré mediana y rango intercuartílico. La comparación apareada se plantea con Wilcoxon. Para retrabajo binario, requerir o no corrección, se plantea McNemar. También separaré ejecuciones frías y calientes.”

## 12:00–13:00 · Estado actual

**Mostrar:** implementado vs. pendiente.

**Decir:**

“La arquitectura, los controles y los componentes están documentados. Para cerrar científicamente el trabajo debo completar la matriz experimental y conservar evidencia trazable de cada comparación. No quiero atribuir porcentajes de mejora antes de tener esa medición.”

## 13:00–15:00 · Preguntas al asesor

1. ¿Considera correcto concentrar la evaluación en la preparación y carga controlada de recursos?
2. ¿Qué ajustes recomienda para alinear objetivos, indicadores y casos apareados?
3. ¿Qué evidencia debería priorizar antes de ejecutar los 360 casos: integración extremo a extremo, casos críticos o validación física?
4. ¿Qué observaciones debería corregir en el Plan de Tesis antes de gestionar su conformidad ante la Escuela?

## Regla de exposición

No leer el README completo. Usarlo como mapa visual. Si el profesor pregunta por un componente, abrir la sección técnica correspondiente.
