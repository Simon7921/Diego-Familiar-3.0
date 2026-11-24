# Corrección de seguridad — Diego Familiar V30

Se corrigió la revocación de miembros: el propietario ahora elimina en una única transacción por lotes la membresía y la invitación que permitió el ingreso. Esto evita que un integrante retirado vuelva a entrar utilizando una invitación anterior.

## Instalación

Sube todos los archivos descomprimidos a tu repositorio de pruebas Diego-Familiar-3.0, reemplazando la versión anterior; o actualiza `diego-familiar.js` desde este paquete. En Firebase, el archivo `firestore.rules` sigue siendo el mismo que ya copiaste.

**Importante:** mantén las reglas de denegación hasta que hayas publicado el JS corregido y validado con cuentas ficticias. Prueba revocar acceso y, luego, intentar unirse otra vez con el mismo correo e ID; debe denegarse.

No publicar información real de salud hasta verificar lectura/escritura por roles y acceso denegado a terceros.
