# Solicitud y activación de licencias

La licencia habilita los módulos contratados y queda vinculada al hotel, dominio e instalación. La VPS del cliente nunca contiene la clave privada de firma.

## Flujo simplificado

1. Instalá el sistema normalmente. No pide una licencia durante la instalación.
2. Abrí la web y copiá el único código `VIGIA-INST2...` que aparece.
3. Enviá ese código al proveedor.
4. El proveedor devuelve una clave larga `VIGIA2...` o, como alternativa, un archivo `.vigia`.
5. Pegá la clave o cargá el archivo en esa misma pantalla. La activación se aplica inmediatamente.

La validación diaria ocurre dentro de la instalación. El sistema puede seguir funcionando sin conexión a internet durante toda la vigencia contratada.

## Activar en la web

La API valida la firma, el código del hotel, el dominio, el vencimiento y el ID de instalación antes de guardar nada. Una clave de otro hotel o de otra VPS será rechazada. Si una renovación falla, la licencia anterior permanece intacta.

## Renovación o cambio de servidor

- Para renovar, solicitá otra clave para la misma instalación y pegala en la pantalla de activación. También podés cargar otro `.vigia`.
- Para cambiar de dominio o VPS, generá una solicitud nueva y emití otra licencia para el nuevo dominio o UUID.
- El sistema valida la nueva licencia antes de reemplazar la activa y conserva un respaldo local.
- Una renovación inválida no modifica la licencia que está en producción.
- La licencia vencida no elimina datos.
