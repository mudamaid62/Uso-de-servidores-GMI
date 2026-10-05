# Uso-de-servidores-GMI
Como acceder a los servidores Ada y Dayhoff.

## Como obtener una cuenta

1. Solicite la creación de una cuenta en Ada y/o Dayhoff a Patricio.

2. Una vez su usuario haya sido creado, siga las instrucciones de acceso.

## Acceso a los servidores

1. Desde el terminal de su computador (puede acceder a este usando MobaXterm, PuTTY, WSL-2, o similares), ejecute el siguiente comando para generar una ssh-key.

```
ssh-keygen -t ed25519 -f ~/.ssh/id_sshfs -N "" -C "Cualquier nombre que le quieran dar a su key"
```

2. OPCIONAL: Si desea incrementar la seguridad de conexión, puede colocar una segunda contraseña sin restricciones de formato, llamada PASS PHRASE, al generar el ssh-key con la opción -N.

```
ssh-keygen -t ed25519 -f ~/.ssh/id_sshfs -N "PASS PHRASE" -C "Cualquier nombre que le quieran dar a su key"
```

3. Copie su public key en el servidor para el que se le haya otorgado una cuenta. IMPORTANTE: El paso 1 generará 2 archivos, id_sshfs e id_sshfs.pub, el primero es un archivo privado que no debe compartir con nadie, el segundo es público.

```
ssh-copy-id -i ~/.ssh/id_sshfs.pub user@ip_server
```

4. Verifique que la copia de ssh-key haya funcionado correctamente.

```
ssh -i ~/.ssh/id_sshfs user@ip_server
```

Si el servidor le da acceso sin pedirle password, habra realizado la copia de ssh-key correctamente.

5. Desde la terminal de su computador cree el siguiente archivo: ~/.ssh/config, usando su editor de textos preferido, e.g. nano.

```
nano ~/.ssh/config
```

6. En dicho archivo, escriba bloques con el siguiente formato (uno por cada servidor que este utilizando), y luego guárdelo.

```
Host server_name
        HostName ip_server 
        User user
        IdentityFile ~/.ssh/id_sshfs
        BatchMode yes
        StrictHostKeyChecking accept-new
        Port 22
```

7. Finalmente, podra acceder al servidor utilizando el siguiente comando:

```
ssh server_name
```

