## Tunel local SSH + RDP


## Exposición de un Servicio desde una VPS Privada a través de una VPS Pública

En una **VPC (Red Privada Virtual)** con dos **VPS**, una pública y otra privada, queremos exponer un servicio que se ejecuta en la máquina privada a nuestro host, utilizando la máquina pública como puente.

### Arquitectura de la Configuración

1. **VPS Pública**: Tiene una IP pública y acceso desde el exterior.

2. **VPS Privada**: No tiene IP pública y solo es accesible desde la red interna.

3. **Servicio**: Corre en la VPS privada y debe ser accesible desde el host local.

4. **Túnel SSH o Reenvío de Puertos**: Se usa para redirigir el tráfico desde la máquina pública hacia la privada.


### Método de Exposición

#### **Reenvío de Puertos con SSH**

Desde el **host local**, podemos usar **SSH** para establecer un túnel que permita acceder al servicio como se muestra en las siguientes capturas:


```bash
ssh -L 127.0.0.1:8000:<IP_PRIVADA>:8000 root@<IP_PUBLICA>
```

![](ANEXOS/Pasted%20image%2020250404193433.png)



![](ANEXOS/Pasted%20image%2020250404193406.png)

![](ANEXOS/Pasted%20image%2020250404193417.png)

---

Una vez seguidos los pasos desde nuestro host podremos ver el servidor http de nuestra maquina privada e incluso podríamos conectarnos a través de un RDP a nuestro host privado, para ello usaremos el escritorio remoto de windows y habra que instalar xrdp y xcf4 en nuestro vps privado

![](ANEXOS/Pasted%20image%2020250404204350.png)

# Instalación de Xfce4 y XRDP en un VPS para escaneos "anónimos"

Este documento explica cómo instalar **Xfce4** y **XRDP** en un VPS para acceder de forma remota a un entorno de escritorio ligero.

---

## Instalación en Debian/Ubuntu

1. **Actualizar los paquetes**
    
    ```bash
    sudo apt update && sudo apt upgrade -y
    ```
    
2. **Instalar Xfce4**
    
    ```bash
    sudo apt install xfce4 xfce4-goodies -y
    ```
    
3. **Instalar XRDP**
    
    ```bash
    sudo apt install xrdp -y
    ```
    
4. **Configurar XRDP para usar Xfce4**
    
    ```bash
    echo "xfce4-session" > ~/.xsession
    sudo systemctl restart xrdp
    ```
    
5. **Habilitar XRDP en el arranque**
    
    ```bash
    sudo systemctl enable xrdp
    ```

---

## Auditorías de Páginas Externas sin Exponer la IP Pública

Una vez configurado el acceso remoto a nuestro VPS con XRDP, podemos realizar auditorías de sistemas externos sin exponer nuestra IP pública. En este caso, he encontrado a través de Shodan un PLC expuesto que podríamos intentar atacar.

### Procedimiento:

1. **Buscar sistemas expuestos en Shodan**  
   Utilizando Shodan, podemos localizar dispositivos expuestos, como PLCs.


![](ANEXOS/Pasted%20image%2020250410125212.png)


2. **Intentar atacar el PLC**  
Con el PLC identificado, podríamos intentar explotar vulnerabilidades conocidas

3. **Ver el contenido a través del RDP**  
Gracias a nuestro acceso remoto al VPS mediante RDP, podemos visualizar el contenido del sistema atacado de forma segura y sin exponer nuestra IP pública.


