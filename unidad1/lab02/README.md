# Laboratorio 02

## Fundamentos de Redes y Modelos de Referencia (OSI y TCP/IP)

## Temas:
- Laboratorio GNU/Linux.
  - Inspección de interfaces de red mediante ip a, ifconfig, diagnóstico de conectividad básico con ping y trazado de rutas con traceroute / mtr.
- Programación Emisor-Receptor.
  - Construcción de un script emisor-receptor de Socket RAW para la captura e inspección visual de bytes en bruto sobre la interfaz de red local.

## Crear dos nodos Emisor-Receptor con Docker

- Se puede utilizar Docker para crear dos contenedores que estén conectados en una misma red y tengan los paquetes necesarios para realizar pruebas de comunicación y envío de paquetes.
- **Dockerfile**
  - Este archivo crea la imagen rcd_lab01_image_escobedo con OpenJDK 17, Vim, ip, ifconfig, ping, traceroute y mtr.
```bash
FROM eclipse-temurin:17-jdk

RUN apt-get update && \
    apt-get install -y \
        vim \
        iproute2 \
        net-tools \
        iputils-ping \
        traceroute \
        mtr-tiny \
    && rm -rf /var/lib/apt/lists/*

CMD ["tail", "-f", "/dev/null"]
```
- **docker-compose.yml**
```bash
services:

  container1:
    build:
      context: .
      dockerfile: Dockerfile
    image: rcd_lab01_image_escobedo
    container_name: rcd_lab01_container1_escobedo
    hostname: container1
    networks:
      - rcd_lab01_network_escobedo
    stdin_open: true
    tty: true
    restart: unless-stopped

  container2:
    build:
      context: .
      dockerfile: Dockerfile
    image: rcd_lab01_image_escobedo
    container_name: rcd_lab01_container2_escobedo
    hostname: container2
    networks:
      - rcd_lab01_network_escobedo
    stdin_open: true
    tty: true
    restart: unless-stopped

networks:
  rcd_lab01_network_escobedo:
    name: rcd_lab01_network_escobedo
    driver: bridge
```
- **Construir la imagen y crear los contenedores**
- Desde la carpeta donde están Dockerfile y docker-compose.yml:
```bash
docker compose up -d --build
```
```bash
docker ps
```
```bash
docker exec -it rcd_lab01_container1_escobedo bash
```
- Si quieres eliminar los contenedores y la red creada por Compose:
```bash
docker compose down
```

## Inspección de Interfaces de Red

- Estas herramientas permiten verificar qué tarjetas de red (físicas o virtuales) están activas, sus direcciones IP, máscaras de subred y direcciones MAC.
  
- **Comando ip a (o ip address)**
  - Es la herramienta moderna y estándar en todas las distribuciones Linux actuales (paquete iproute2).
    ```bash
    ip a

  <img width="1109" height="503" alt="image" src="https://github.com/user-attachments/assets/e71ec736-4a9a-43ed-979c-d5ebcb2bcaf4" />




    ```
  - **lo**: Interfaz de loopback (local, siempre 127.0.0.1).
  - **eth0, enp3s0, wlan0**: Nombres de las interfaces físicas (Ethernet o Wi-Fi).
  - **inet**: Muestra la dirección IPv4 asignada y su máscara en formato CIDR (ej. 192.168.1.15/24).
  - **link/ether**: Muestra la dirección MAC física del dispositivo.
  - **UP**: Indica que la interfaz está encendida y operativa.

- **Comando ifconfig**
  - Es la herramienta tradicional. Aunque está obsoleta (deprecated) y ha sido reemplazada por ip, todavía se encuentra en muchos sistemas antiguos o servidores estables (paquete net-tools).
  ```bash
  ifconfig
  ```
  - **inet**: Dirección IPv4.
  - **netmask**: Máscara de subred tradicional (ej. 255.255.255.0).
  - **ether**: Dirección MAC.
  - **RX packets / TX packets**: Estadísticas de paquetes recibidos y transmitidos (útil para detectar errores o pérdida de paquetes a nivel de hardware).
 <img width="832" height="842" alt="image" src="https://github.com/user-attachments/assets/ec31c186-165e-4c1f-96f5-005b8b109c1b" />
Direccion IPV4:
Propio: 192.168.40.238
Compañera: 192.168.40.239
MAscara de subred: 255.255.255.0
Dirección Fisica: BC-EC-A0-39-16-89
## Diagnóstico de Conectividad Básico

- Una vez verificada la interfaz local, el siguiente paso es comprobar si el equipo puede comunicarse con otros nodos de la red.
- **Comando ping**
  - Envía paquetes de solicitud de eco (ICMP Echo Request) a un destino para verificar si está encendido y accesible.
  ```bash
  ping 8.8.8.8
  ```
  <img width="490" height="245" alt="image" src="https://github.com/user-attachments/assets/38bea686-5ba2-40ff-96b6-0b9de856ad26" />
 
  ```bash
  ping -c 4 google.com
  ```
  <img width="551" height="230" alt="image" src="https://github.com/user-attachments/assets/0b649941-dedb-405d-8979-ca2c0b0be02b" />

  - **time=XX ms**: El tiempo de ida y vuelta (Round Trip Time o RTT). Valores bajos indican una conexión rápida.
  - **packet loss**: El porcentaje de paquetes perdidos. Lo ideal es 0%. Si es mayor, hay problemas de saturación, interferencia o fallas en el cableado.
 Revisa los tiempos en milisegundos (Tiempo = XXms) y confirma que el porcentaje de paquetes perdidos sea 0%.
## Trazado de Rutas
- Cuando el comando ping falla o la conexión es lenta, el trazado de rutas ayuda a identificar exactamente en qué punto o salto (hop) de la red pública o privada se está interrumpiendo o ralentizando el tráfico.
  
  - **Comando traceroute**
  - Muestra la ruta exacta que toman los paquetes desde tu equipo hasta el destino, listando cada uno de los routers (saltos) por los que pasa.
   ```bash
  traceroute google.com
  ```
   <img width="633" height="169" alt="image" src="https://github.com/user-attachments/assets/863a20f6-1f6c-423a-9d64-bcec2ef8c441" />

  - **Cómo funciona**: Incrementa el tiempo de vida (TTL) del paquete de 1 en 1. Cada router en el camino descarta el paquete cuando el TTL llega a cero y devuelve un mensaje de error ICMP, revelando su identidad.
  - **Qué buscar**: Si ves asteriscos (* * *), significa que ese router intermedio tiene bloqueados los paquetes de diagnóstico por motivos de seguridad o que la red se cayó en ese punto exacto.
 
## Comando mtr (My Traceroute)
- Es una herramienta avanzada que combina la funcionalidad de ping y traceroute en una interfaz interactiva y en tiempo real.
  ```bash
  mtr google.com
  ```
- **Ventajas**: No realiza una sola pasada como traceroute, sino que sigue enviando paquetes de forma continua a cada salto.
- **Loss%**: Permite ver con precisión matemática qué router intermedio del proveedor de internet está perdiendo paquetes.
- **Last/Avg/Best/Wrst**: Estadísticas de latencia (última, promedio, mejor y peor) por cada salto, ideal para detectar picos de lag intermitentes.



## Actividades
Trabajar preferentemente en grupos de 2 estudiantes.
Elaborar un informe detallado, paso a paso, que explique e incluya capturas de pantalla (README.md:títulos, subtítulos, párrafos, tablas, imágenes, diagramas, autocalificación, etc.).
1. Crear dos contenedores en Docker de acuerdo con la nomenclatura utilizada para realizar la inspección de las interfaces de red, el diagnóstico de conectividad y el trazado de rutas (Utilice todos los comandos explicados).
2. Programar un emisor y un receptor en el lenguaje de programación Java, con tipos de conexión simplex, dúplex o bidireccional. Utilizando los ejercicios de las figuras 4.8, 4.9, 4.10, 4.11 y 4.12 del libro de M. L. Liu. (2004). Computación Distribuida Fundamentos y Aplicaciones.
   a) Pruebas de la comunicación simplex local (utilizando los contenedores en la misma máquina anfitriona).
   b) Pruebas de comunicación dúplex en la intranet de la universidad (utilizando los contenedores y la red de área local del laboratorio de cómputo).
Creación de carpeta en el disco C

<img width="523" height="165" alt="image" src="https://github.com/user-attachments/assets/95bd9433-67fe-4dc0-b31f-5f2f6f63b461" />
 Creación del archivo en java
 
 <img width="735" height="250" alt="image" src="https://github.com/user-attachments/assets/7ec6d48f-312a-48c4-8114-b6314d9a6c3b" />
creacion del emisor
<img width="582" height="91" alt="image" src="https://github.com/user-attachments/assets/1f279b91-2fb1-466e-adfa-2b3b1ca64719" />
<img width="927" height="730" alt="image" src="https://github.com/user-attachments/assets/39d743ec-168c-476c-a9f4-736cbfe03e9e" />
Creacion del receptor
<img width="594" height="101" alt="image" src="https://github.com/user-attachments/assets/19abc0d2-652b-460c-8149-2337ccacf091" />
<img width="876" height="487" alt="image" src="https://github.com/user-attachments/assets/b5847a4b-e00d-4ec0-8c44-6d8be17df814" />
Escuchando 
<img width="559" height="231" alt="image" src="https://github.com/user-attachments/assets/1aad5648-a6f1-45f2-81ab-52a32ff80192" />


## Rúbrica de Calificación

## Referencias 
- [Capítulo 1. Primeros pasos con Docker](https://recetas-docker.readthedocs.io/es/latest/capitulo_1.html)
- [ifconfig(8) - Linux man page](https://linux.die.net/man/8/ifconfig)
- [ping(8) - Linux man page](https://linux.die.net/man/8/ping)
- [traceroute(8) - Linux man page](https://linux.die.net/man/8/traceroute)
- [M. L. Liu. (2004). Computación Distribuida Fundamentos y Aplicaciones. Pearson](https://drive.google.com/file/d/1IWbPqprv7DjRywDDr67QuPHK1Y4LZIbX/view?usp=sharing). 
