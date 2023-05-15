# SSH

Antes de configurar ssh debemos verificar que el IOS lo soporta, para ello con el comando `show version` en el modo de EXEC Privilegiado `#`
![Screenshot de la respuesta del comando show version.](/img/ssh.1.png)
Buscamos la imagen del sistema operativo, en el nombre tiene que tener k9.

**SSH** funciona en el puerto **22 TCP**.
1. Inicialmente el dispositivo tiene que tener un nombre único.
`(config)#`
```
hostname <Nombre>
```
2. Configurar el nombre de dominio IP de la red
`(config)#`
```
ip domain name <Nombre.com>
```
3. Generar una llave para encriptar tráfico SSH
SSH cifra el tráfico entre el origen y el destino. Sin embargo, para ello, se debe generar una clave de autenticación única mediante el comando de configuración global crypto. El módulo bits determina el tamaño de la clave y se puede configurar de 360 bits a 2048 bits. Cuanto mayor sea el valor de bit, más segura será la clave. Sin embargo, los valores de bits más grandes también tardan más en cifrar y descifrar la información. La longitud mínima de módulo recomendada actualmente es de 1024 bits.
`(config)#`
```
crypto key generate rsa general-keys modulus <bits>
```
4. Base de datos local
Cree una entrada de nombre de usuario en la base de datos local utilizando el comando  username de configuración global. En el ejemplo, el parámetro secret 5 se usa para que la contraseña se encripte con MD5.
`(config)#`
```
username <Usuario> secret <Contraseña>
```
5. Configuramos las líneas vty
`(config)#`
```
line vty 0 15
```
6. Configurar protocolo.
De forma predeterminada, no se permite ninguna sesión de entrada en las líneas vty. Puede especificar varios protocolos de entrada, incluidos Telnet y SSH mediante el transport input <ssh | telnet>
`(config-line)#`
```
transport input ssh
```
7. Activamos el inicio de sesión con la base de datos local (la del dispositivo de red Switch o Router)
`(config-line)#`
```
login local
```
8. Agregamos el usuario
`(config)#`
```
username <Nombre> secret <Contraseña>
```
## Verificar configuración
`(config)#`
```
show ip ssh
```

## Verificar conexiones
`(config)#`
```
show ssh
```
## No logs telnet|ssh
Por default cuando nos conectamos a través de ssh o telnet se muestran todos los logs, por ejemplo cuando se levanta o se apaga una interfaz, cuando se configura, etc. Para evitar esto configuramos en las líneas vty el siguiente comando:
`(config-line)#`
```
logging synchronous
```