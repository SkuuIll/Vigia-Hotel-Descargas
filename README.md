# Vigía Hotel · Descargas oficiales

Este repositorio contiene únicamente los instaladores compilados de Vigía Hotel. El código fuente, las claves de firma y el generador de licencias se mantienen en repositorios privados.

## Qué descargar

- **Instalación nueva:** `hotel-control-onprem-VERSION.tar.gz` y su comprobante `.sha256`.
- **Aplicación Android:** `vigia-hotel-VERSION.apk` y su comprobante `.sha256`.

Las descargas están en [Releases](../../releases/latest). No descargues **Source code**, porque GitHub lo genera automáticamente y no es el instalador.

## Guías públicas

- [Instalar el sistema en una VPS nueva](docs/INSTALACION.md)
- [Solicitar y activar una licencia](docs/LICENCIAS.md)

## Activación

El paquete puede descargarse e instalarse públicamente sin una clave. Al abrir la web, el sistema muestra una pantalla de activación y permanece bloqueado hasta recibir una licencia Ed25519 emitida para ese hotel e instalación. La activación se hace con una sola clave larga o un archivo `.vigia`, sin depender del sistema operativo ni de una conexión permanente a internet.

## Actualizaciones

Cada versión publicada y aprobada en el repositorio privado se copia automáticamente aquí. Las instalaciones deben usar versiones concretas; nunca la etiqueta `latest` para imágenes Docker.

La actualización del servidor la realiza el proveedor durante una ventana de mantenimiento mediante el script incluido en el paquete, con respaldo y recuperación automática si falla.

## Integridad

Antes de instalar en Ubuntu:

```bash
sha256sum -c hotel-control-onprem-VERSION.tar.gz.sha256
```

Para verificar la APK:

```bash
sha256sum -c vigia-hotel-VERSION.apk.sha256
```
