# Configuracion de contraseñas
**Inicialmente** los dispositivos **no cuentan con contraseña** para ningún modo y esto es una **falla de seguridad**, para repararlo y **proteger** los dispositivos de red contra intrusos malintencionados se puede poner **contraseña a cada modo de ejecucion**.

Las contraseñas deben seguir las siguientes estructuras para tener seguridad:
- Mínimo 8 caracteres, entre una longitud más grande estará más protegida contra ataques de fuerza bruta.
- Incluya una combinación de letras mayúsculas y minúsculas, números, símbolos y espacios, si están permitidos.
- Evitar contraseñas comunes de diccionario, como nombres de personas, mascotas, shows de televisión, películas, etc.
- Escriba una contraseña con errores de ortografía a propósito. Por ejemplo, Smith = Smyth = 5mYth, o Seguridad = 5egur1dad.
- Cambiar contraseñas periódicamente.
- No anotar contraseñas en lugares obvios


|Débil|Fuerte|
|-----|------|
|Cisco|C15c0!2054|
|Firulais|&514Lur1F$|
|LosVengadores123|12^h u4@1p7|# Configuracion de contraseñas
**Inicialmente** los dispositivos **no cuentan con contraseña** para ningún modo y esto es una **falla de seguridad**, para repararlo y **proteger** los dispositivos de red contra intrusos malintencionados se puede poner **contraseña a cada modo de ejecucion**.

Las contraseñas deben seguir las siguientes estructuras para tener seguridad:
- Mínimo 8 caracteres, entre una longitud más grande estará más protegida contra ataques de fuerza bruta.
- Incluya una combinación de letras mayúsculas y minúsculas, números, símbolos y espacios, si están permitidos.
- Evitar contraseñas comunes de diccionario, como nombres de personas, mascotas, shows de televisión, películas, etc.
- Escriba una contraseña con errores de ortografía a propósito. Por ejemplo, Smith = Smyth = 5mYth, o Seguridad = 5egur1dad.
- Cambiar contraseñas periódicamente.
- No anotar contraseñas en lugares obvios


|Débil|Fuerte|
|-----|------|
|Cisco|C15c0!2054|
|Firulais|&514Lur1F$|
|LosVengadores123|12^h u4@1p7|

En los routers Cisco, se ignoran los espacios iniciales para las contraseñas, pero no ocurre lo mismo con los espacios que le siguen al primer carácter. Por lo tanto, un método para crear una contraseña segura es utilizar la barra espaciadora y crear una frase compuesta de muchas palabras. Esto se conoce como frase de contraseña. Una frase de contraseña suele ser más fácil de recordar que una contraseña simple. Además, es más larga y más difícil de descifrar.

## EXEC de usuario
El modo de EXEC de usuario es el modo principal. Es el modo que aparece cuando se conecta uno por `consola`, `ssh` o `telnet`. Se caracteriza por tener en el prompt el carácter `>`.

1. Primero se tiene que ingresar al modo de **configuracion de linea** `(config-line)#`.

El siguiente comando se ingresa en el modo de **configuracion global** `(config)#`.
El `0` indica que es la primera (en la mayoría de los casos la única) interfaz de consola.
```
line console 0
```
2. La contraseña puede contener números, caracteres especiales, letras mayúsculas, minúsculas y espacios después del primer carácter.
```
password <Contraseña>
```
3. Activamos el acceso con contraseña.
```
login
```
4. Salimos del modo de configuración.
```
end
```

## EXEC Privilegiado
El modo de EXEC Privilegiado es el que se utiliza para configurar o ver la configuracion del dispositivo de red. Se caracteriza por tener en el prompt el carácter `#`. 
**Se requiere habilitar para poder configurar por conexión a través de ssh.**

El siguiente comando se ejecuta en el modo de configuración global `(config)#`.
```
enable secret <Contraseña>
```

## Las líneas de terminal virtual (VTY)
Las VTY permiten el acceso remoto mediante Telnet o SSH al dispositivo. Muchos switches de Cisco admiten hasta 16 líneas VTY que se numeran del 0 al 15.
Los comandos se ingresan en el modo de configuración global `(config)#`.

1. El comando recibe una o un rango de líneas a configurar.
```
line vty <Linea>
```
```
line vty <LineaIncial> <LineaFinal>
```
### Ejemplo:
```
line vty 0 15
```
2. Establer la contraseña.
A partir de aquí los comandos se ingresan en el modo de configuracion de linea `(config-line)#`.
```
password <Contraseña>
```
3. Se activa para que pida contraseña.
```
login
```
4. Salimos del modo de configuración.
```
end
```
# Tiempo de sesión
Se puede establecer un tiempo específico en el cual si no hay actividad se cerrará la sesión. Esto se hace en las líneas ya sea console, vty, etc `(config-line)#`.

```
exec-timeout <mins> <secs>
```

# Encriptar Contraseñas
Por default las contraseñas se quedan guardadas en texto plano en la configuración del dispositivo y podrían ser vulneradas. Para ello el siguiente comando encripta las contraseñas para que no puedan ser legibles a simple vista.

Se ingresa en el modo de configuración global `(config)#`.
```
service password-encryption
```

# Mensaje de acceso
Se puede configurar un mensaje cuando alguien se conecte al dispositivo ya sea por consola o por algún medio como SSH.
El mensaje debe estar contenido entre dos caracteres los cuales no los puede incluir el mensaje. En este caso `#`, pero podría ser `$`, `%`, `&`, etc. Incluso una letra o número pero este no puede estar dentro del mensaje.
## Ejemplo:
**Bien**
```
# Acceso restringido #
```
**Mal**
```
# Acceso restringido para #10 usuarios #
```
## Configuración:
Se ingresa en el modo de configuración global `(config)#`.
```
banner motd #<Mensaje>#
```
