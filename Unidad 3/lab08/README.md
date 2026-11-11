 <div align="left">
    <!-- PRIMERA TABLA: ENCABEZADO Y CURSO -->
    <table style="width: 80%; border: 1px solid #ddd; padding: 20px; text-align: center; border-collapse: collapse; margin-bottom: 20px; font-family: Arial, sans-serif;">
        <thead>
            <tr>
                <td style="width: 150px; text-align: center; padding: 10px;">
                     <img src="https://github.com/leonardouwz/lp3_vectorcitos/blob/main/lab05 ev4/Consola/logo_ULASALLE_grande.png" width="120" />
                </td>
                <th style="text-align: left; padding: 10px;">
                    <span style="font-weight: bold; font-size: 20px;">UNIVERSIDAD LA SALLE</span><br />
                    <span style="font-weight: bold; font-size: 16px;">FACULTAD DE INGENIERÍA DE SOFTWARE</span>
                </th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td colspan="2" style="text-align: center; padding-top: 20px; font-weight: bold; font-size: 16px;">Curso: Redes y Comunicación de Datos</td>
            </tr>
            <tr>
                <td style="font-weight: bold; text-align: left; padding: 10px; width: 150px;">Fecha:</td>
                <td style="text-align: left; padding: 10px;">11/11/2026</td>
            </tr>
        </tbody>
    </table>
</div>

<div align="left">
    <!-- SEGUNDA TABLA: INFORMACIÓN BÁSICA -->
    <table style="width: 80%; border: 1px solid #ddd; padding: 20px; border-collapse: collapse; font-family: Arial, sans-serif;">
        <thead>
            <tr>
                <th colspan="6" style="text-align: center; font-size: 20px; padding: 10px; background-color: #f5f5f5; border-bottom: 1px solid #ddd;">INFORMACIÓN BÁSICA</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td style="font-weight: bold; padding: 8px; width: 180px;">ASIGNATURA:</td>
                <td colspan="5" style="padding: 8px;">Redes y Comunicación de Datos</td>
            </tr>
            <tr>
                <td style="font-weight: bold; padding: 8px;">TÍTULO:</td>
                <td colspan="5" style="padding: 8px;">Laboratorios</td>
            </tr>
            <tr>
                <td style="font-weight: bold; padding: 8px;">NÚMERO DE PRÁCTICA:</td>
                <td style="padding: 8px;">08</td>
                <td style="font-weight: bold; padding: 8px;">AÑO LECTIVO:</td>
                <td style="padding: 8px;">2026B</td>
                <td style="font-weight: bold; padding: 8px;">NRO. SEMESTRE:</td>
                <td style="padding: 8px;">VI</td>
            </tr>
            <tr>
                <td colspan="6" style="font-weight: bold; padding: 10px 8px 4px 8px;">DOCENTES:</td>
            </tr>
            <tr>
                <td colspan="6" style="padding: 4px 8px 12px 24px;">
                    <ul style="margin: 0; padding-left: 20px;">
                        <li>Richart Smith Escobedo Quispe - r.escobedo@ulasalle.edu.pe</li>
                    </ul>
                </td>
            </tr>
            <tr>
                <td colspan="6" style="font-weight: bold; padding: 10px 8px 4px 8px;">ESTUDIANTE:</td>
            </tr>
            <tr>
                <td colspan="6" style="padding: 4px 8px 12px 24px;">
                    <ul style="margin: 0; padding-left: 20px;">
                        <li style="margin-bottom: 5px;">Juan Arturo Colque Aragon - jcolque@ulasalle.edu.pe</li>
                    </ul>
                </td>
            </tr>
         <tr>
                <td colspan="6" style="font-weight: bold; padding: 10px 8px 4px 8px;">Desarrollo teórico:</td>
            </tr>
            <tr>
                <td colspan="6" style="padding: 4px 8px 12px 24px;">
                    <ul style="margin: 0; padding-left: 20px;">
                                             
                    
### 3.1 Concepto de Subnetting
El **subnetting** (o subdivisión de redes) es el proceso lógico mediante el cual se divide una red IP física o principal en dos o más subredes más pequeñas e independientes.
* **Mecanismo:** Consiste en tomar prestados bits de la porción de *host* y asignarlos a la porción de *red*, modificando la máscara de subred original.
* **Beneficios:** 
  * Optimización del tráfico al reducir los dominios de difusión (*broadcast*).
  * Mejora de la seguridad mediante la segmentación de redes.
  * Mayor eficiencia en la administración del direccionamiento IP.

### 3.2 Clasificación de Redes IPv4

| Clase | Rango Primer Octeto | Máscara por Defecto | Prefijo | Bits Red / Host |
| :---: | :---: | :---: | :---: | :---: |
| **A** | $1 - 127$ | `255.0.0.0` | `/8` | 8 bits / 24 bits |
| **B** | $128 - 191$ | `255.255.0.0` | `/16` | 16 bits / 16 bits |
| **C** | $192 - 223$ | `255.255.255.0` | `/24` | 24 bits / 8 bits |

### 3.3 Fórmulas Fundamentales (FLSM)

* **Subredes requeridas ($N_s$):** 
  $$N_s = 2^n$$ *(donde $n$ es el número de bits prestados de host)*
* **Hosts totales por subred ($H_t$):** 
  $$H_t = 2^h$$ *(donde $h$ es el número de bits restantes de host)*
* **Hosts útiles por subred ($H_u$):** 
  $$H_u = 2^h - 2$$
* **Tamaño del bloque / Salto de Red ($S$):** 
  $$S = 256 - \text{Valor del octeto modificado en la máscara}$$

---

## ⚙️ 4. Desarrollo del Subnetting (FLSM)

### Caso Práctico: Subnetting Clase C (`192.168.10.0 /24`)
* **Requisito:** Dividir la red en **4 subredes**.
* **Cálculos:**
  * Bits prestados ($n$): $2^2 = 4 \implies n = 2$ bits.
  * Nueva Máscara: `255.255.255.192` (`/26`).
  * Salto de red: $256 - 192 = 64$.
  * Hosts útiles por subred: $2^6 - 2 = 62$.

#### Tabla de Subredes Calculadas

| Subred # | Dirección de Red | Máscara | Primer Host Útil | Último Host Útil | Broadcast | Prefijo |
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| **Subred 0** | `192.168.10.0` | `255.255.255.192` | `192.168.10.1` | `192.168.10.62` | `192.168.10.63` | `/26` |
| **Subred 1** | `192.168.10.64` | `255.255.255.192` | `192.168.10.65` | `192.168.10.126` | `192.168.10.127` | `/26` |
| **Subred 2** | `192.168.10.128` | `255.255.255.192` | `192.168.10.129` | `192.168.10.190` | `192.168.10.191` | `/26` |
| **Subred 3** | `192.168.10.192` | `255.255.255.192` | `192.168.10.193` | `192.168.10.254` | `192.168.10.255` | `/26` |

---

## 💻 5. Configuración de Dispositivos

### Tabla de Asignación de Direcciones IP

| Dispositivo | Interfaz | Dirección IP | Máscara de Subred | Gateway |
| :--- | :--- | :--- | :--- | :--- |
| **Router-1** | `GigabitEthernet0/0/0` | `192.168.10.1` | `255.255.255.192` | N/A |
| **Router-1** | `GigabitEthernet0/0/1` | `192.168.10.65` | `255.255.255.192` | N/A |
| **PC-A** | `FastEthernet0` | `192.168.10.10` | `255.255.255.192` | `192.168.10.1` |
| **PC-B** | `FastEthernet0` | `192.168.10.70` | `255.255.255.192` | `192.168.10.65` |

### Script de Configuración CLI (Cisco IOS)

```cisco
enable
configure terminal
hostname R1

! Configuración Interfaz Subred 0
interface GigabitEthernet0/0/0
 description Conexion a LAN Subred 0
 ip address 192.168.10.1 255.255.255.192
 no shutdown
 exit

! Configuración Interfaz Subred 1
interface GigabitEthernet0/0/1
 description Conexion a LAN Subred 1
 ip address 192.168.10.65 255.255.255.192
 no shutdown
 exit

end
write memory
```
### Diagrama de la Topología

<img width="471" height="455" alt="image" src="https://github.com/user-attachments/assets/77231c28-4e2a-4e47-94ef-69b3e2e9002b" />

<img width="471" height="455" alt="image" src="https://github.com/user-attachments/assets/77231c28-4e2a-4e47-94ef-69b3e2e9002b" />

### Configuración
* Configuración del Router
<img width="668" height="721" alt="config ro" src="https://github.com/user-attachments/assets/e9f20358-e520-40c3-969c-815c92c5b278" />

* Configuración de Pcs
<img width="748" height="721" alt="configPC4" src="https://github.com/user-attachments/assets/4aab504f-8dda-4b05-902e-cb6f4738d128" />
<img width="748" height="721" alt="configPC2" src="https://github.com/user-attachments/assets/cdac2da0-d32f-424b-b146-74539fa557c5" />
<img width="748" height="721" alt="configPC1" src="https://github.com/user-attachments/assets/887b39f3-84c5-4ad2-ae38-b11ac2fd234c" />

* Máscaras y puertas de enlace.

<img width="689" height="100" alt="verificando R1" src="https://github.com/user-attachments/assets/4a198e04-a0a3-4929-8411-7e672fe5781d" />

* Comandos utilizados
<img width="680" height="721" alt="configuracion2" src="https://github.com/user-attachments/assets/a1ea785b-402e-40cb-ad00-4e1de3b49ba9" />




                    </ul>
                </td>
            </tr>
        </tbody>
    </table>
</div>
