# Cambiar nombre al router o switch
Este comando sirve para cambiar localmente el nombre del dispositivo de red.
Esto facilita la administración de los dispositivos al tener identificado en cual se está trabajando.

Se ejecuta en el modo de configuración global `Router(config)#` o `Switch(config)#`.

```
hostname <NuevoNombre>
```
---
## Ejemplo1:
```
Router(config)# hostname R1
```
```
R1(config)#
```
## Ejemplo2:
```
Swtich(config)# hostname SMain
```
```
SMain(config)#
```