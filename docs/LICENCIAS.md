# Solicitud y activación de licencias

La licencia habilita los módulos contratados y queda vinculada al hotel, dominio e instalación. La VPS del cliente nunca contiene la clave privada de firma.

## Flujo simplificado

1. En la VPS ejecutá `./instalar.sh` para generar `solicitud-licencia.json`.
2. Enviá ese archivo al proveedor.
3. El proveedor devuelve un archivo como `activacion-HOTEL_CENTRAL.vigia`.
4. Copialo a la VPS y activalo con el mismo instalador.

La validación diaria ocurre dentro de la instalación. El sistema puede seguir funcionando sin conexión a internet durante toda la vigencia contratada.

## Activar en la VPS

Copiá el archivo recibido y ejecutá:

```bash
cd /opt/hotel-control
./instalar.sh activacion-HOTEL_CENTRAL.vigia
```

El instalador valida firma, código del hotel, dominio e ID de instalación antes de iniciar el sistema. Una licencia de otro hotel o de otra VPS será rechazada.

## Renovación o cambio de servidor

- Para renovar, solicitá otro archivo `.vigia` para la misma instalación y ejecutá nuevamente `./instalar.sh archivo.vigia`.
- Para cambiar de dominio o VPS, generá una solicitud nueva y emití otra licencia para el nuevo dominio o UUID.
- El instalador valida la nueva licencia antes de reemplazar la activa y conserva la anterior como `licencia.json.previous`.
- Una renovación inválida no modifica la licencia que está en producción.
- La licencia vencida no elimina datos.
