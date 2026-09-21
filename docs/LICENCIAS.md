# Solicitud y activación de licencias

La licencia habilita los módulos contratados y queda vinculada al hotel, dominio e instalación. La firma se genera offline; la clave privada nunca se guarda en Cloudflare ni en la VPS del cliente.

## Flujo simplificado

1. En la VPS ejecutá `./instalar.sh` para generar `solicitud-licencia.json`.
2. Entregá ese archivo al proveedor por el canal acordado.
3. El proveedor validará el hotel, dominio, instalación, vigencia, usuarios y módulos contratados.
4. Recibirás un ZIP de activación firmado para instalarlo en la VPS.

La licencia se valida localmente en el servidor y en la APK. El proveedor no necesita acceso remoto a la VPS para emitirla.

## Formulario de cliente

| Campo | Ejemplo | Formato |
|---|---|---|
| Nombre | `Hotel Central` | Nombre comercial |
| Código | `HOTEL_CENTRAL` | Letras, números, espacios, `-` o `_`; se normaliza a mayúsculas |
| Correo | `administracion@hotel.com` | Correo válido |
| Dominio | `gestion.hotel.com` | Sin protocolo, puerto ni ruta |
| Notas | `Contacto: Juan` | Opcional |

El código y el dominio deben coincidir con `solicitud-licencia.json`. Por ejemplo, no escribas `https://gestion.hotel.com/` en el campo dominio.

## Formulario de licencia

| Campo | Significado |
|---|---|
| Cliente | Hotel que recibirá la licencia |
| ID de instalación | UUID generado por la VPS; se completa al importar el JSON |
| Plan comercial | Preselección de módulos que después puede personalizarse |
| Vigencia en días | Entre 1 y 3650 días |
| Usuarios activos máximos | Total de cuentas activas: serenos, administradores, recepción y demás usuarios |
| Módulos | Apartados que podrá utilizar ese hotel |

La restricción de módulos y usuarios se aplica en el servidor, incluso si alguien intenta acceder directamente a una URL oculta.

## Activar en la VPS

Copiá el ZIP recibido y ejecutá:

```bash
cd /opt/hotel-control
./instalar.sh paquete-activacion-HOTEL.zip
```

El instalador valida firma, código del hotel, dominio e ID de instalación antes de iniciar el sistema. Una licencia de otro hotel o de otra VPS será rechazada.

## Renovación o cambio de servidor

- Para renovar, generá una licencia nueva manteniendo el mismo cliente e ID de instalación.
- Para cambiar de dominio o VPS, generá una solicitud nueva y emití otra licencia para el nuevo dominio o UUID.
- La licencia vencida no elimina datos. Conservá siempre respaldos antes de reemplazarla.
