# ZIZI · Cobro automatizado de cuotas

Propuesta de automatización del cobro de cuotas del Instituto Tecnológico de Matehuala
(proceso TecNM-AD-PO-002), con identificación del pago y facturación automática.

- **Alumno:** Amaury Alí Tristán Córdova · 24660188 · 5to Sistemas
- **Materia:** Fundamentos de Ingeniería de Software (SCC-1007)
- **Docente:** Garza Ortega Jesús Alberto
- **Empresa ficticia:** ZIZI · «Si es con ZIZI, es easy»

## Prototipo en línea

**https://link0n1.github.io/zizi-pagos/**

Es una página web navegable con datos inventados. Simula el portal donde el alumno consulta sus adeudos, solicita trámites (constancias, credenciales y tarjetas de acceso) y paga con tarjeta de prueba. Al terminar recibe un comprobante con folio. También incluye un panel del personal de Recursos Financieros.

> Es un prototipo académico. No es el sitio oficial del Tec, solo acepta tarjetas de prueba y nunca guarda números de tarjeta.

## Dónde está el código

El código de la página y su base de datos, que hacen funcionar la dirección de arriba, están en un **repositorio aparte**: [zizi-pagos](https://link0n1.github.io/zizi-pagos/).

En este repositorio, la carpeta **`Web/`** contiene también el código (`index.html`) y la base de datos (`BD_ZIZI_Pagos.xlsx`). Esa copia no tiene una dirección web propia, pero es prácticamente lo mismo que está publicado.

## Instrucciones de uso

1. Entra a https://link0n1.github.io/zizi-pagos/
2. Escribe un **número de control que esté en la base de datos** (por ejemplo `23690001`).
3. **Primera vez:** la página te pide crear una **contraseña**. Puede ser cualquiera (mínimo 8 caracteres y un número). Se guarda en tu navegador para tus siguientes visitas.
4. En el inicio verás lo que **tienes por pagar** y la sección **Solicitar un trámite**, donde puedes pedir una constancia o un duplicado de credencial o tarjeta de acceso.
5. Pulsa **Pagar** y elige la forma de pago:
   - **Tarjeta:** usa una tarjeta de prueba (más abajo).
   - **Referencia:** copia la referencia y pulsa «Simular depósito del banco».
6. Al aprobarse el pago, la página muestra el **recibo**, que se puede imprimir o descargar.

### Datos que valida la página

Los datos de la base de datos, [BD_ZIZI_Pagos.xlsx](https://github.com/LINK0N1/zizi-pagos/blob/main/BD_ZIZI_Pagos.xlsx) (también en la carpeta `Web/` de este repositorio), **son los que valida la página**. Por eso, para que funcione hay que usar los datos de ese archivo: el número de control tiene que existir en la hoja `Alumnos`.

Ejemplos de la hoja `Alumnos`:

| Número de control | Alumno | Dígito verificador |
|---|---|---|
| 23690001 | Ana López | 7 |
| 22690002 | Carlos Pérez | 7 |
| 24690003 | Valentina Zúñiga | 8 |
| 21690004 | Diego Torres | 4 |
| 21690005 | Fernanda Rangel | 1 |

El **dígito verificador** también se pide al pagar con tarjeta, para confirmar que el pago es para ese número de control. Está en la columna `NumVerificador` de la hoja `Alumnos`.

### Pago con tarjeta de prueba

Las tarjetas de prueba **ya están guardadas** en la hoja `TarjetasPrueba`, así que no hace falta agregar otra. Para pagar solo se inventa el **nombre del titular** (nombre y apellido). En la página, el botón «Usar» de «Tarjetas de prueba» llena el número, el vencimiento y el código.

| Tarjeta | Número | Vencimiento | Código | Resultado |
|---|---|---|---|---|
| Visa débito | 4242 4242 4242 4242 | 12/30 | 123 | Aprobada |
| Mastercard crédito | 5555 5555 5555 4444 | 08/29 | 456 | Aprobada |
| Visa débito | 4000 0000 0000 9995 | 11/28 | 321 | Fondos insuficientes |
| Visa crédito | 4000 0000 0000 0002 | 05/29 | 999 | Rechazada por el banco |

El número, el vencimiento y el código deben coincidir con los de la tabla; el **nombre del titular** es libre.

### Otras opciones

- **Panel del personal:** en la pantalla de inicio, pulsa «Ver alumnos de prueba y panel del personal».
- **Cargar otra base de datos:** en el panel del personal, «Cargar base de datos (Excel)» lee un archivo con el mismo formato que `BD_ZIZI_Pagos.xlsx` (requiere internet).
- **Empezar de cero:** «Restablecer prototipo» borra las contraseñas, los pagos nuevos y los trámites solicitados.

## Contenido de este repositorio

- `docs/` entregas en PDF (E2, E3)
- `diseno/` BPMN TO-BE, arquitectura, wireframes y el primer prototipo
- `Web/` código y base de datos de la página
- `src/` código del proyecto (E4)

## Pila tecnológica

HTML, CSS y JavaScript en un solo archivo, con base de datos en Excel. La propuesta contempla Python con Flask, SQLite, Stripe en modo de prueba, facturación simulada y Brevo para los correos.

## Aviso

Todos los datos son inventados. La pasarela y la facturación son simuladas. No se solicita ni se guarda ningún dato real de tarjeta.
