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
                <td style="text-align: left; padding: 10px;">18/11/2026</td>
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
                <td colspan="5" style="padding: 8px;">Subnetting</td>
            </tr>
            <tr>
                <td style="font-weight: bold; padding: 8px;">NÚMERO DE PRÁCTICA:</td>
                <td style="padding: 8px;">07</td>
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
                <td colspan="6" style="font-weight: bold; padding: 10px 8px 4px 8px;">Desarrollo:</td>
            </tr>
            <tr>
                <td colspan="6" style="padding: 4px 8px 12px 24px;">
                    <ul style="margin: 0; padding-left: 20px;">


---

## Acceso y Ejecución de la Calculadora VLSM

### 1. Ejecutar en línea
Abrir directamente desde el navegador haciendo clic en el siguiente enlace:

**[Abrir Calculadora de Redes VLSM](https://arturo049.github.io/rcd/Unidad%203/lab07/)**


### 2. Ejecutar de forma local tras clonar el repositorio
Si clona el repositorio en una computadora:
```bash
git clone [https://github.com/arturo049/rcd.git](https://github.com/arturo049/rcd.git)
cd "rcd/Unidad 3/lab07"

##  Guía de Uso de la Calculadora VLSM

1. **Ingresar la Red Base:** Escribe la dirección IP principal junto con su prefijo de máscara en formato CIDR (ejemplo: `192.168.1.0/24` o `172.16.0.0/16`). Si omites el prefijo, el sistema asignará automáticamente la máscara por defecto según la clase (A, B o C).
2. **Definir los Hosts por Subred:** En el segundo campo, indica la cantidad de hosts requeridos separados por comas:
   * **Modo estándar (VLSM):** Escribe cada requerimiento individualmente (ej. `100, 50, 25, 2`). El algoritmo ordenará los valores de mayor a menor de forma automática.
   * **Modo masivo (Multiplicador):** Usa el formato `Cantidad x Hosts` para generar múltiples subredes iguales de una sola vez (ej. `50x30, 20x10`).
3. **Calcular:** Haz clic en el botón **Calcular Subredes VLSM**.
4. **Interpretar Resultados (Salida estilo `ipcalc`):**
   * **Resumen Superior:** Muestra la clase de la IP ingresada, el total de direcciones consumidas frente a las disponibles y recomienda cambiar a Clase A, B o C si los hosts superan la capacidad de la red actual.
   * **Detalle por Subred:** Entrega la máscara de subred (`Netmask`), dirección de red (`Network`), rango de IPs asignables (`HostMin` - `HostMax`) y dirección de difusión (`Broadcast`).
   * **Bits Prestados:** Indica explícitamente cuántos bits fueron tomados de la porción de host y los resalta en color rojo dentro de la representación binaria.
