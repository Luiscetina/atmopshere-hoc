# hoc-loader: Horizon OC 2.6.1 + USB en un solo Loader

Esta carpeta junta el codigo de overclock de **Horizon OC 2.6.1** con el Loader
de este Atmosphere (que ya trae la integracion USB de Nexus), para compilar un
`hoc.kip` que tenga las dos cosas.

## Contenido

| Archivo | Origen |
| --- | --- |
| `source/ldr_process_creation.cpp` | Fusion: el de Horizon OC 2.6.1 + los cambios USB de este repo. Fusion de 3 vias, 0 conflictos. |
| `source/oc/` | Codigo de overclock de Horizon OC 2.6.1, sin cambios. |
| `loader.json` | De Horizon OC 2.6.1. Agrega el acceso a 0x7000F000 (FUSE) que usa `oc/`. |
| `system_module.mk` | De Horizon OC 2.6.1 (agrega la opcion `HOC_UART_LOG`). |
| `LICENSE-HorizonOC` | Licencia de Horizon OC (GPL-2.0). |

El Loader normal de `stratosphere/loader/` **no se modifica**: sigue siendo el
que lleva el USB y va dentro del paquete de Atmosphere. El workflow copia estos
archivos encima solo durante la compilacion.

## Como compilar

1. Sube este repositorio a GitHub (privado esta bien).
2. Ve a **Actions -> "Build hoc.kip (HOC + USB)" -> Run workflow**.
3. Al terminar, descarga el artefacto `hoc-kip-usb`. Dentro esta `atmosphere/kips/hoc.kip`.

## Como probarlo

1. Antes que nada crea en Hekate una entrada de arranque **sin** la linea `kip1=`
   y respalda tu emuMMC.
2. Copia el `hoc.kip` nuevo a `atmosphere/kips/hoc.kip` en la SD.
3. Usa el overlay y `hoc-clk` **de Horizon OC 2.6.1**. No los mezcles con otra version.
4. Probablemente tengas que volver a poner tus valores de overclock, porque el
   KIP nuevo trae los valores por defecto.

## Cuando cambies el Loader

Si modificas `ldr_process_creation.cpp`, `loader.json` o `system_module.mk` en
`stratosphere/loader/`, hay que volver a fusionar con la copia de esta carpeta.

## Creditos y licencia

- **Horizon OC** (https://github.com/Horizon-OC/Horizon-OC), GPL-2.0: codigo de overclock en `source/oc/`, `loader.json` y `system_module.mk`. Ver sus creditos en el README original.
- **Atmosphere-NX**, GPL-2.0: Loader base. Los archivos conservan su aviso de copyright.
- **Nexus-USB-Firmware** (TR4UNEXUS): integracion USB incluida en `ldr_process_creation.cpp`.

Si compartes el `hoc.kip` o un paquete que lo incluya, la GPL-2.0 te obliga a
ofrecer tambien el codigo fuente correspondiente.
