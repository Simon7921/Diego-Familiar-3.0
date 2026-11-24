# Diego AI V31 — Inteligencia Glucémica experimental

## Entregado e integrado
- Botón «Diego AI» en el menú lateral y acceso desde Bitácora. Conserva Inicio, alimentos, recetas, pauta, bitácora, Firebase familiar y ratios médicos existentes.
- Importación CSV LibreView con cabecera reconocida, con filas de metadatos; fechas locales de día/mes/año o año/mes/día; mg/dL y mmol/L. Sensor histórico, escaneo y tira capilar; duplicados evitados por tipo/fecha/valor. Archivo procesado solo en el dispositivo, guardado en IndexedDB. Exportación y eliminación.
- Gráfico SVG temporal de valores reales, línea 70 mg/dL, marcadores de eventos. No crea puntos de glucosa ficticios ni conecta segmentos separados por grandes huecos. Compara registros de bitácora (sin sincronizar automáticamente todo el CSV a Firebase).
- Patrones 3/7/14/30 días, conteos, ventanas horarias, mínimos/máximos, pares de mediciones, episodios con Fiasp documentada, actividad y rescates, pares sensor-capilar. Señala datos faltantes.
- Proyecciones experimentales a 15/30 minutos usando ejemplos históricos comparables de nivel y cambio en 15 minutos, con percentiles empíricos 10–90. Se muestran SOLO con lectura de sensor de <=10 min, >=3 días de historial, >=80 pares para entrenamiento, >=30 muestras válidas de evaluación cronológica, error absoluto medio <=25 mg/dL y cobertura >=70%. No hay horizonte de 60 minutos.
- Retrospectiva temporal (último cuarto de los datos reservado para evaluación), con MAE, cobertura, bajas no anticipadas y falsos avisos calculados. Es una evaluación exploratoria, no validación clínica.
- Asistente de preguntas frecuentes basado exclusivamente en cálculos de bitácora + CSV, sin usar LLM remoto ni enviar datos a servidores. Informe TXT para diabetóloga.

## Restricciones importantes
- El programa NO se conecta en vivo con Abbott FreeStyle Libre ni obtiene lecturas continuas automáticamente. LibreView se importa manualmente.
- El programa NO conoce con exactitud insulina activa, orden de los alimentos ni sueño; no los inventa. El CSV importado NO se sincroniza con la familia, solo los datos de la bitácora existente.
- La proyección NO es una alarma ni se debe usar para descartar una hipoglucemia, postergar el tratamiento, dar insulina, cambiar ratios o ajustar carbohidratos de rescate.
- El algoritmo no es un modelo clínicamente validado. Sus intervalos son percentiles históricos, no bandas de confianza clínica. La evaluación temporal es solo una revisión técnica preliminar.
- No hay conexión automática a un modelo generativo. El asistente utiliza respuestas deterministas y explicables con recuentos reales, evitando alucinaciones.
- Valores de LibreView o bitácora se tratan como datos de salud sensibles. Antes de usar datos reales, validar Firestore con cuentas ficticias y políticas de acceso, usar respaldos y probar en iPhone/Android.

## Instalación en GitHub Pages
1. Guarda la ZIP V31 como copia de respaldo, descomprime y sube sus archivos a tu repositorio de pruebas Diego-Familiar-3.0 (index.html en raíz). No subir el ZIP como único archivo.
2. Si ya configuraste el archivo `firebase-config.js`, conserva la configuración existente del repositorio: el de esta ZIP contiene `null` para no incluir datos de tu Firebase.
3. Antes de habilitar el módulo familiar, publica y prueba las reglas `firestore.rules` en Firebase con datos ficticios. Contiene la corrección de revocación en `diego-familiar.js`.
4. La prueba de Diego AI puede hacerse sin Firebase. Abre Bitácora → Diego AI → Importar LibreView CSV. No requiere clave OpenAI.
5. Revisa la sección de evaluación; si hay pocos datos, debe indicar «Información insuficiente para proyectar».

No se ha publicado ni modificado GitHub ni Firebase mediante esta entrega. No se ha realizado prueba real en Safari iPhone.
