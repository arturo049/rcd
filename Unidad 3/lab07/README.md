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

## Guía de Uso

1. <b>Dirección IP Base:</b> Ingresar la dirección de red principal junto con su prefijo de máscara en formato CIDR (ejemplo: <code>192.168.1.0/24</code> o <code>172.16.0.0/16</code>). Si se omite el prefijo, el sistema asigna la máscara por defecto según la clase de red.
2. <b>Requerimientos de Hosts:</b> Especificar la cantidad de dispositivos por subred separados por comas:
   - <b>Asignación individual:</b> Ingresar cada requerimiento por separado (ejemplo: <code>100, 50, 25, 2</code>). El algoritmo ordena los valores de mayor a menor de forma automática.
   - <b>Asignación masiva:</b> Utilizar el formato <code>Cantidad x Hosts</code> para generar múltiples subredes del mismo tamaño (ejemplo: <code>50x30, 20x10</code>).
3. <b>Procesamiento:</b> Presionar el botón <b>Calcular Subredes VLSM</b> para generar la tabla de direccionamiento.
4. <b>Interpretación de Resultados:</b>
   - <b>Resumen general:</b> Indica la clase de red detectada, el consumo total de direcciones IP y sugiere una clase superior (A, B o C) en caso de exceder la capacidad del bloque inicial.
   - <b>Detalle por subred:</b> Presenta la máscara de subred (<code>Netmask</code>), dirección de red (<code>Network</code>), rango de direcciones asignables (<code>HostMin</code> - <code>HostMax</code>), dirección de difusión (<code>Broadcast</code>) y el desglose binario con los bits prestados resaltados.
