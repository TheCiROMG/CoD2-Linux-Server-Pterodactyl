# Call of Duty 2 Linux Server - Pterodactyl Egg

Este repositorio contiene un servidor de Call of Duty 2 versión 1.3 para Linux, optimizado para funcionar con Pterodactyl Panel. Incluye un Egg completamente configurado, compatibilidad con Debian, librerías necesarias y el mod zPAM preinstalado.

## 📥 Descarga Directa

Si no deseas utilizar el Egg de Pterodactyl y solo necesitas los archivos del servidor, puedes descargarlos directamente desde el siguiente enlace:

[Descargar Servidor CoD2 Linux](http://179.41.2.31:25596/games/cod2linux/cod2linuxserver.zip)

**Comando de Inicio en consola/CLI** : 

```bash 
LD_PRELOAD=./libCoD2x.so LD_LIBRARY_PATH=./gcc3-libs ./cod2_lnxded +set dedicated 2 +set net_ip 0.0.0.0 +set net_port (SERVERPORT) +set net_queryPort (SERVERPORT) +set sv_lan 0 +exec server.cfg +map mp_pavlov
```

## 🥚 Detalles del Egg (JSON)

El archivo `egg-cod2-linux-deb.json` es la configuración de importación para Pterodactyl.

### Características Principales
- **Imagen Docker**: `ghcr.io/pelican-eggs/steamcmd:debian`
- **Startup Command**:
  ```bash
  LD_PRELOAD=./libCoD2x.so LD_LIBRARY_PATH=./gcc3-libs ./cod2_lnxded +set dedicated 2 +set net_ip 0.0.0.0 +set net_port ${SERVER_PORT} +set net_queryPort ${SERVER_PORT} +set sv_lan 0 +exec server.cfg +map mp_pavlov
  ```
- **Instalación Automática**: El script instala dependencias de 32 bits (`libc6-i386`, `libstdc++5`) y descarga el servidor automáticamente.

## 📂 Estructura del Proyecto y Mods

### `main/`
Directorio principal del servidor.
- **zPAM Mod**: Incluye `zpam336.iwd` (zPAM v3.36).
  - **Nota de Compatibilidad**: Se utiliza esta versión específica de zPAM porque es la más estable para la versión 1.3 del servidor. Versiones más modernas de zPAM tienden a crashear en la 1.3 pura.
  - **Configuración**: El `server.cfg` está preconfigurado para zPAM (modo "comp" por defecto).
- **Mapas**: Incluye `zpam_maps_v6.iwd` y mapas estándar (`iw_*.iwd`).
- **FastDL**: Configurado en `server.cfg` apuntando a `http://179.41.2.31:25596`.

### `libcod2 1 3` & `libCoD2x.so`
El servidor se ejecuta utilizando `libCoD2x.so` inyectado vía `LD_PRELOAD`.
- **Función**: Extiende las capacidades del servidor 1.3, corrige exploits y añade nuevos comandos de script.
- **Experimental**: Aunque se incluye zPAM 3.36 por estabilidad, la presencia de `libCoD2x` *podría* teóricamente permitir ejecutar versiones más modernas de zPAM u otros mods que requieran funciones extendidas, aunque esto no está garantizado ni configurado por defecto.

### `gcc3-libs/`
Librerías de compatibilidad (`libstdc++.so.5`, `libgcc_s.so`) necesarias para ejecutar el binario original de CoD2 (compilado con GCC 3.3) en sistemas Linux modernos (Debian 10/11/12).

### `pb/`
Archivos de PunkBuster. Aunque el soporte oficial de PB finalizó hace años, se mantienen los binarios para compatibilidad legacy con clientes que lo requieran o herramientas de administración antiguas.

## ⚠️ Notas Importantes

- **RCON Password**: Revisa el archivo `main/server.cfg` y cambia la contraseña `rcon_password` antes de poner el servidor en producción.
- **Versión del Juego**: Este servidor corre la versión **1.3**. Asegúrate de que los clientes también estén en la versión 1.3.
