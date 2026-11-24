# Diego Familiar V30 — guía de activación (prototipo)

Esta versión añade la **infraestructura de sincronización opcional**; **no está activada automáticamente**. No subas información de salud de Diego a la nube hasta configurar y probar acceso, reglas y respaldos.

## 1. Antes de comenzar

1. Abre la V29 actual en el teléfono con los registros originales.
2. En **Bitácora → Respaldo JSON**, descarga un respaldo y guárdalo en lugar privado.
3. La V30 también crea un respaldo local interno `diego.v30.precloudBackup` antes de conectarse; aun así, el respaldo descargado es indispensable.
4. NO compartas contraseñas ni claves privadas. Cada integrante debe usar su correo personal.

## 2. Crear Firebase

1. En https://console.firebase.google.com/ crea un proyecto nuevo, preferentemente con región apta para el tratamiento de datos de salud. Revisa condiciones, privacidad y costos antes de habilitar datos reales de un menor.
2. Configura una **aplicación web** y copia el objeto de configuración pública (apiKey, authDomain, projectId, appId) en `firebase-config.js`, sustituyendo el `null` actual. La `apiKey` **del SDK web de Firebase** es identificador público y no equivale a una clave secreta de OpenAI.
3. Authentication → Sign-in method → activa **Email/Password**. Authentication → Settings → Authorized domains: registra `simon7921.github.io` (y el dominio personalizado de pruebas, si lo hubiera).
4. Firestore Database → crea base. **No** selecciones reglas abiertas; copia `firestore.rules` y publica las reglas antes de ingresar información real. Debes probarlas contra el emulador o Rules Playground.
5. Sube los archivos descomprimidos al repositorio de pruebas **Nueva-APP**, sin tocar otras aplicaciones. Publica Pages desde `main` y `/(root)`.
6. Comprueba acceso en tres ventanas privadas antes de cargar datos reales; haz prueba con información **ficticia**. Verifica que un correo no invitado no pueda leer ni editar.

## 3. Activar espacio familiar

1. Abre `https://simon7921.github.io/Nueva-APP/` después de publicar V30.
2. En **Bitácora de Diego → Configurar o administrar acceso familiar**, crea tu cuenta con contraseña única, confirma el email de verificación y vuelve a iniciar sesión.
3. Pulsa **Crear espacio privado de Diego**. Su ID es identificador, **no contraseña ni permiso**.
4. En **Autorizar correo**, escribe el correo real y elige editor (registra) o viewer (solo consulta). Envía el ID a esa persona por privado.
5. El familiar crea/verifica su cuenta en el mismo sitio, pega el ID y pulsa **Unirme con invitación**.
6. El propietario puede revisar integrantes y **revocar** su acceso desde la misma sección. Para bloquear una invitación todavía no utilizada se debe borrar en Firestore → `families/{id}/invites/{email}`.
7. Una vez comprobado el acceso, y con un **respaldo JSON ya guardado**, pulsa **Subir registros locales de este dispositivo** una sola vez. Se usa el respaldo previo a la primera conexión, los IDs previenen duplicados y no se borra el historial remoto.

## Datos que sincroniza

- Solo registros de `Bitácora` (glucosas introducidas, comidas y sus HC, insulina aplicada, bajas y ejercicio).
- **No** sincroniza ratios, Tresiba, otros parámetros médicos ni archivos/fotografías.
- Los registros compartidos se reflejan entre teléfonos conectados. La app usa una copia local como respaldo de consulta.

## Limitaciones importantes antes de uso real

- **Prototipo no auditado**: reglas pendientes de prueba formal con emulador, privacidad y evaluación legal; no usar con datos sensibles reales hasta hacerlo.
- En caso de falta de internet, las escrituras pueden quedar pendientes y **no hay garantía de sincronización en segundo plano con la app cerrada**. Exporta respaldos y revisa el estado mostrado.
- Si dos personas editan el **mismo registro al mismo tiempo**, puede prevalecer el último cambio; no hay conciliación avanzada ni historial inmutable.
- No existe migración de la pauta ni integración con sensor, ni seguimiento automático. No se agregan recomendaciones de dosis.
- Las fotografías con IA siguen requiriendo un servicio externo aparte.
- El acceso familiar no reemplaza las alertas de glucosa ni las indicaciones clínicas.

## Prueba mínima recomendada

- Dos correos verificados: propietario y editor; un tercero no invitado.
- Invitación correcta, acceso correcto y bloqueo del tercero.
- Crear una glucosa ficticia desde A, verla en B; corregirla en B y verla en A; borrar y verificar la eliminación.
- Intentar editar desde cuenta viewer (debe rechazar), revocar miembro y verificar denegación al volver a conectarse.
- Exportar JSON y comprobar que los registros anteriores sigan disponibles.
- Revisar que los ratios de Diego sigan siendo desayuno 1:18, almuerzo 1:22, once 1:20, cena 1:22, colaciones sin insulina y Tresiba 12 U según última pauta comunicada. No se modifican ni se sincronizan.
