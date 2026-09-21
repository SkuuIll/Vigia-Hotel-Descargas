# Vigía Hotel · Descargas oficiales

Este repositorio contiene únicamente los instaladores compilados de Vigía Hotel. El código fuente, las claves de firma y el generador de licencias se mantienen en repositorios privados.

## Qué descargar

- **Instalación nueva:** `hotel-control-onprem-VERSION.tar.gz` y su comprobante `.sha256`.
- **Aplicación Android:** `vigia-hotel-VERSION.apk` y su comprobante `.sha256`.

Las descargas están en [Releases](../../releases/latest). No descargues **Source code**, porque GitHub lo genera automáticamente y no es el instalador.

## Guías públicas

- [Instalar el sistema en una VPS nueva](docs/INSTALACION.md)
- [Solicitar y activar una licencia](docs/LICENCIAS.md)
- [Abrir el portal de licencias](https://vigia-licencias-portal.moreappmix.workers.dev/)

## Activación

El paquete puede descargarse públicamente, pero el sistema requiere una licencia Ed25519 emitida para el hotel, dominio e instalación correspondientes. La descarga pública no permite activar módulos ni reutilizar una licencia en otro servidor.

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
