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
