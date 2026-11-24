# V30 — Diego Familiar (integración opcional)

- Se conserva V29: calculador de HC, pauta, ratios, recordatorio de sensor, bitácora y fotos.
- Se añade panel familiar con registro/inicio de sesión individual mediante Firebase Auth y confirmación de email.
- Crear espacio privado, invitar correo específico, rol editor/lector, revocar miembros.
- Firestore sincroniza únicamente los documentos de bitácora cuando se configure Firebase, con actualizaciones en tiempo real.
- Los registros previos se respaldan localmente antes de conexión, y se importan con consentimiento explícito.
- Las instrucciones están en CONFIGURAR-DIEGO-FAMILIAR.md; reglas en firestore.rules.
- No se cambian ratios, insulina, datos médicos ni archivos clínicos.

**Estado:** prototipo que requiere configurar Firebase, probar reglas de seguridad y realizar validación real en iPhone/Android antes de usar datos clínicos.
