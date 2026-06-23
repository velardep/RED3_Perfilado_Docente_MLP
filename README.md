# RED3 — Perfilador de Estilo Docente (MLP)

Red neuronal que predice el estilo pedagógico predominante de un docente a partir de su historial de uso del sistema. Usada por el backend de SIPRE para generar recomendaciones personalizadas.

**Notebook original en Google Colab:**
https://colab.research.google.com/drive/1ji9jER7hDSAhIb4QHkm7JVOz5OZLVUFE

---

## Estilos que clasifica

| Estilo | Descripción |
|---|---|
| `PRACTICO_APLICADO` | Orientado a actividades prácticas y aplicación |
| `MAGISTRAL_ESTRUCTURADO` | Enfoque expositivo y teoría estructurada |
| `EVALUATIVO` | Prioriza rúbricas y evaluación continua |
| `TECNOLOGICO_INNOVADOR` | Incorpora recursos tecnológicos |
| `REFLEXIVO_ITERATIVO` | Itera, revisa y adapta sus planificaciones |

---

## Dataset

No requiere dataset externo. El script genera 12.000 muestras sintéticas mediante código usando distribuciones estadísticas (Poisson, Beta, Dirichlet) que simulan el comportamiento real de docentes con distintos estilos. Las muestras se pseudo-etiquetan automáticamente con reglas de bootstrap.

Solo ejecutar el notebook desde la primera celda en orden.

---

## Features de entrada (30)

Agrupadas en: uso del sistema · actividad de chat · generación de PDC · biblioteca PDC · recursos tecnológicos · dimensiones pedagógicas (SABER/HACER/SER/DECIDIR) · señales implícitas (tasa de aprobación y fricción).

---

## Cómo entrenar

1. Abrir el notebook en Google Colab (link arriba)
2. Ejecutar todas las celdas en orden (no se necesita subir ningún archivo)

---

## Artefactos generados

El entrenamiento produce `red3_artifacts.zip` con:

```
red3_model_state.pt      ← pesos del modelo
red3_config.json         ← versión, estilos, configuración
red3_feature_schema.json ← schema de 30 features con tipos
red3_label_map.json      ← lista de estilos
red3_scaler.json         ← mean y std para normalización
red3_metrics.json        ← accuracy, F1, ECE del modelo entrenado
```

Subir el contenido descomprimido a Cloudflare R2 bajo el prefijo `models/red3/`.
