# Instalación en una VPS nueva

Esta guía instala Vigía Hotel en Ubuntu Server 24.04 LTS sin clonar repositorios ni usar credenciales privadas de GitHub.

## Requisitos

- VPS x86_64 con Ubuntu Server 24.04 LTS.
- 2 vCPU, 4 GB de RAM y 50 GB SSD como mínimo.
- IP pública fija.
- Un subdominio, por ejemplo `gestion.hotel.com`, apuntando a la IP.
- Puertos TCP 22, 80 y 443 habilitados. No publiques PostgreSQL ni otros puertos internos.

## 1. Descargar y comprobar el instalador

Descargá la versión más reciente desde [Releases](https://github.com/SkuuIll/Vigia-Hotel-Descargas/releases/latest). Necesitás estos dos archivos:

- `hotel-control-onprem-VERSION.tar.gz`
- `hotel-control-onprem-VERSION.tar.gz.sha256`

Copialos a la VPS y verificá la descarga:

```bash
cd /tmp
sha256sum -c hotel-control-onprem-VERSION.tar.gz.sha256
```

Continuá solamente si el resultado indica `OK`.

## 2. Extraer y preparar Ubuntu

```bash
sudo mkdir -p /opt/hotel-control
sudo tar -xzf hotel-control-onprem-VERSION.tar.gz \
  -C /opt/hotel-control --strip-components=1
sudo chown -R "$USER":"$USER" /opt/hotel-control
cd /opt/hotel-control
./preparar-vps.sh
```

Cerrá la sesión SSH y volvé a entrar para aplicar los permisos de Docker.

## 3. Crear la configuración

```bash
cd /opt/hotel-control
./instalar.sh
```

El asistente solicita:

| Campo | Ejemplo | Regla |
|---|---|---|
| Nombre del hotel | `Hotel Central` | Nombre visible para los usuarios |
| Código | `HOTEL_CENTRAL` | Letras, números, guiones o guiones bajos |
| Dominio | `gestion.hotel.com` | Sin `https://` ni rutas |
| Correo | `sistemas@hotel.com` | Se utiliza para el certificado HTTPS |

El instalador genera automáticamente contraseñas, PIN, URLs y un identificador único. Si todavía no existe una licencia, crea `/opt/hotel-control/solicitud-licencia.json` y se detiene de forma segura.

## 4. Solicitar la licencia

Seguí la [guía de licencias](LICENCIAS.md). Recibirás un archivo parecido a `paquete-activacion-HOTEL_CENTRAL.zip`.

## 5. Activar e iniciar

Copiá el ZIP a `/opt/hotel-control` y ejecutá:

```bash
cd /opt/hotel-control
./instalar.sh paquete-activacion-HOTEL_CENTRAL.zip
docker compose --env-file .env -f docker-compose.yml ps
```

Comprobá el servicio sustituyendo el dominio:

```bash
curl -fsS https://gestion.hotel.com/api/v1/health
```

Después abrí `https://gestion.hotel.com` en el navegador.

## 6. Instalar la aplicación Android

La APK vinculable a cualquier hotel queda disponible en:

```text
https://gestion.hotel.com/downloads/vigia-hotel.apk
```

Instalala en el teléfono operativo y vinculala con el QR generado por el panel administrativo.

## 7. Actualizar

Realizá las actualizaciones fuera del horario operativo:

```bash
cd /opt/hotel-control
ENV_FILE=./.env ./actualizar.sh NUEVA_VERSION
```

Ejemplo: `./actualizar.sh 1.4.0`. El script descarga la versión pública, comprueba SHA-256 y firma Sigstore, crea respaldos y restaura la versión anterior si algo falla. No necesita `docker login` ni un token de GitHub.

## 8. Respaldo básico

```bash
cd /opt/hotel-control
mkdir -p backups
./respaldar.sh ./backups
```

Guardá copias externas de `backups/`, `.env` y `licencia.json`. No publiques ninguno de esos archivos.

## Problemas frecuentes

- **El dominio no abre:** verificá que DNS apunte a la VPS y que 80/443 estén abiertos.
- **Error de certificado:** comprobá el dominio y los registros DNS; no uses una IP en lugar del dominio.
- **Licencia rechazada:** no edites `licencia.json`; dominio, hotel e ID de instalación deben coincidir con la solicitud.
- **Panel con error 502:** ejecutá `docker compose --env-file .env -f docker-compose.yml ps` y revisá los contenedores detenidos.
