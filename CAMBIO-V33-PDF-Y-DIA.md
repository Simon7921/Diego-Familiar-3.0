# Diego Familiar V33 · PDF LibreView + contexto del día

- Importación de resumen PDF mediante PDF.js en el navegador con revisión y confirmación explícita de los campos detectados: fechas, glucosa media, tiempo en rango, bajo 70, sensor activo, eventos y duración media. No se extraen datos individuales de curvas.
- Conserva CSV de LibreView para lecturas individuales, el calculador actual y la bitácora familiar.
- Nueva sección de contexto diario: cómo estuvo, sueño, actividad, intensidad, situación y nota opcional; selección rápida por fecha.
- Contexto diario se incorpora al informe médico y a patrones descriptivos de Diego AI. Asociación no implica causalidad.
- Datos PDF y contexto diario se guardan SOLO EN ESTE DISPOSITIVO (localStorage), no sincronizados con Firebase. Permite respaldo JSON, pero para importar ese respaldo en otro teléfono se requerirá una mejora posterior.
- PDF.js se carga desde cdnjs por internet. No se sube el PDF a este servicio ni a Firebase; el procesamiento se realiza en el navegador.
- El módulo NO conoce el flujo en vivo del sensor; PDF no habilita pronósticos. La proyección experimental requiere series temporales originales (CSV), evaluación retrospectiva y restricciones ya implementadas.
- Todo prototipo debe probarse en iPhone y con distintos PDF reales. El reporte PDF del 9–22 nov 2026 se usó para probar la lógica de extracción: fechas, 128 mg/dL promedio, 77% en rango, 8% bajo 70, 82% sensor activo, 23 eventos de baja y duración 61 min.
- Mantiene los ratios 1:18 desayuno, 1:22 almuerzo, 1:20 once, 1:22 cena; colación sin insulina; Tresiba 12 U según la configuración precedente. No se dan recomendaciones de dosis ni tratamiento.
- NO subir registros reales a la nube antes de verificar autenticación, roles y revocaciones familiares.
