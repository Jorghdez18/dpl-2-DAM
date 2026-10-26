## Práctica guiada: configuración del acceso remoto mediante SSH

### Incidencia 1: El servicio SSH no está instalado

**Problema detectado**

Al ejecutar `sudo systemctl status ssh`, apareció el mensaje:

`Unit ssh.service could not be found.`

**Causa**

El sistema tenía disponible el cliente OpenSSH, pero no estaba instalado el paquete del servidor OpenSSH.

**Solución aplicada**

Se actualizaron los repositorios y se instaló el servidor SSH mediante los siguientes comandos:

```bash
sudo apt update
sudo apt install openssh-server
```

Después, se inició el servicio y se comprobó su estado:

```bash
sudo service ssh start
sudo service ssh status
```

**Evidencia**

![](images/cap1DPL.png)

---

### Incidencia 2: Generación de las claves SSH

#### Problema detectado: 

Al comenzar la configuración de la autenticación mediante claves SSH, era necesario generar un par de claves para identificar al usuario de forma segura al conectarse al servidor.
 
#### Causa:

Todavía no se disponía de un par de claves SSH generado para realizar la autenticación mediante clave pública.

#### Solución aplicada:

Se ejecutó el siguiente comando para generar un par de claves Ed25519:

```bash
ssh-keygen -t ed25519
```

Durante el proceso, el sistema solicitó la ubicación donde guardar las claves. Se pulsó Enter para aceptar la ubicación predeterminada:

```bash
/home/jorge18/.ssh/id_ed25519
```

A continuación, se configuró una frase de contraseña para proteger la clave privada y se confirmó introduciéndola de nuevo.

El proceso generó dos archivos:

id_ed25519: clave privada, que debe mantenerse protegida y no compartirse.

id_ed25519.pub: clave pública, que se utilizará para configurar la autenticación en el servidor remoto.

Para comprobar que los archivos se habían creado correctamente, se ejecutó:

```
ls -l ~/.ssh/
```

También se puede verificar que la clave pública existe mediante:

```
cat ~/.ssh/id_ed25519.pub
```

#### Evidencia:

![](images/cap2DPL.png)




