# Solicitud y activación de licencias

La licencia habilita los módulos contratados y queda vinculada al hotel, dominio e instalación. La firma se genera offline; la clave privada nunca se guarda en Cloudflare ni en la VPS del cliente.

## Flujo simplificado

1. En la VPS ejecutá `./instalar.sh` para generar `solicitud-licencia.json`.
2. Abrí el [portal de licencias](https://vigia-licencias-portal.moreappmix.workers.dev/).
3. Registrá el hotel si todavía no existe.
4. En **Licencias**, seleccioná **Importar solicitud del servidor** y elegí el JSON.
5. Elegí plan, vigencia, usuarios activos máximos y módulos.
6. Descargá la solicitud comercial y firmala con Vigía Licencias portable para Windows.
7. Entregá el ZIP resultante al hotel y, si querés conservar una copia, adjuntalo al registro del portal.

La importación del JSON ocurre localmente en el navegador. El archivo no se sube a Cloudflare. El portal tampoco interviene en la validación diaria del hotel o de la APK.

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
