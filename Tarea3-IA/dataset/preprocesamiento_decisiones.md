# Preprocesamiento y Segmentación (borrador)

**Normalización aplicada**
- Unicode NFC (mantener tildes correctas).
- Limpieza de caracteres de control (excepto \n y \t).
- Estandarización de comillas/guiones (“ ” ‘ ’ — – … → " ' - ...).
- Unión de palabras cortadas por guion al fin de línea (e.g., "infor-\nmación" → "información").
- Colapso de espacios y saltos en blanco excesivos.
- Conversión a minúsculas (para comparar segmentaciones bajo mismas condiciones).

**Segmentación A – Chunks fijos**
- Tamaño ≈ 400 palabras, solapamiento ≈ 80.
- Ventajas: control de longitud, útil para evaluación reproducible.
- Desventajas: puede cortar ideas a mitad.

**Segmentación B – Encabezados/Secciones**
- Reglas: detec. de Abstract/Resumen/Introducción/Conclusión/Referencias, numerales (1., 2., ...), romanos (I., II., ...), títulos en MAYÚSCULAS.
- Se fusionan secciones muy cortas (<120 palabras) con la siguiente para asegurar contexto mínimo.
- Ventajas: mantiene unidades semánticas; Desventajas: depende de patrones editoriales.

**Salidas**
- base_documentos.jsonl / .parquet: texto completo normalizado por documento + metadata (autor/fecha/tema).
- seg_a.jsonl / seg_b.jsonl: fragmentos con `id_doc`, `chunk_id`, `segmentacion`, `idx`, `texto`, y metadata.
- txt_por_doc/: útil para inspección rápida o depurar PDF problemáticos.

**Razonamiento para comparación**
- A: garantiza tamaño estable → resultados de recuperación comparables.
- B: favorece coherencia semántica → potencialmente mejor grounding.
- Compañero 2 debe crear dos índices (A y B) y comparar métricas (recall@k, precisión manual, tiempo respuesta).
