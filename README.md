# ZIZI · Cobro automatizado de cuotas

Propuesta de automatización del cobro de cuotas del Instituto Tecnológico de Matehuala
(proceso TecNM-AD-PO-002), con identificación del pago y facturación automática.

- **Alumno:** Amaury Alí Tristán Córdova · 24660188 · 5to Sistemas
- **Materia:** Fundamentos de Ingeniería de Software (SCC-1007)
- **Docente:** Garza Ortega Jesús Alberto
- **Empresa ficticia:** ZIZI · «Si es con ZIZI, es easy»

## Prototipo en línea

**https://link0n1.github.io/zizi-pagos/**

Es una página web navegable con datos inventados. Simula el portal donde el alumno consulta sus adeudos, solicita trámites (constancias, credenciales y tarjetas de acceso) y paga con tarjeta de prueba o con referencia. Al terminar recibe un comprobante con folio. También incluye un panel para el personal de Recursos Financieros, con corte diario y bitácora de acciones, y una sección «Acerca de nosotros» sobre ZIZI.

> Es un prototipo académico. No es el sitio oficial del Tec, solo acepta tarjetas de prueba y nunca guarda números de tarjeta.

## Dónde está el código

El código de la página y su base de datos, que hacen funcionar la dirección de arriba, están en un **repositorio aparte**: [zizi-pagos](https://github.com/LINK0N1/zizi-pagos).

En este repositorio, la carpeta **`Material/`** contiene también el código (`index.html`) y la base de datos (`BD_ZIZI_Pagos.xlsx`). Esa copia no tiene una dirección web propia, pero es prácticamente lo mismo que está publicado.

## Instrucciones de uso

### Como alumno

1. Entra a https://link0n1.github.io/zizi-pagos/
2. Escribe un **número de control que esté en la base de datos** (por ejemplo `23690001`). La lista completa se ve en «Ver alumnos de prueba y acceso del personal».
3. **Primera vez:** la página te pide crear una **contraseña**. Puede ser cualquiera (mínimo 8 caracteres y un número). Se guarda cifrada en tu navegador para tus siguientes visitas.
4. En el inicio verás tu **ficha de pago** (número de control y número verificador), lo que **tienes por pagar** y la sección **Solicitar un trámite**, donde puedes pedir una constancia o un duplicado de credencial o tarjeta de acceso.
5. Pulsa **Pagar** y elige la forma de pago:
   - **Tarjeta:** usa una tarjeta de prueba (más abajo). Se pide el número verificador que aparece en tu ficha de pago.
   - **Referencia:** copia la referencia y pulsa «Simular depósito del banco».
6. Al aprobarse el pago, la página muestra el **recibo**, que se puede imprimir o descargar.

### Como personal de Recursos Financieros

1. En la pantalla de inicio, pulsa «Ver alumnos de prueba y acceso del personal» y luego **Acceso del personal**.
2. Escribe tu **usuario** (los de prueba están en la tabla siguiente). **Primera vez:** la página te pide crear tu contraseña (mínimo 8 caracteres y un número), que se guarda cifrada en tu navegador.
3. Según tu rol verás:

| Usuario de prueba | Nombre | Rol | Qué puede hacer |
|---|---|---|---|
| `contador` | Laura Hernández | Contador | Ver ingresos, pagos y el **corte diario**; descargarlo en CSV |
| `jefatura` | Marco Salazar | Jefatura | Todo lo anterior, más la **bitácora de acciones**, la tabla de alumnos con verificadores, la carga de la base de datos y el restablecimiento |
| `contador2` | Sergio Pineda | Contador | Cuenta **dada de baja**: no puede entrar (sirve para probar la baja) |

4. **Corte diario:** elige un día y la página muestra los pagos por concepto, el total y el desglose por método de pago. «Descargar CSV» genera el archivo del día, que termina con la fila **«Generado por»** (persona, rol y fecha). El panel indica quién descargó el último corte de cada día.
5. **Bitácora de acciones** (solo Jefatura): registra inicios y cierres de sesión, descargas de corte, carga de la base y restablecimientos, con persona, rol, fecha y detalle.

### Datos que valida la página

Los datos de la base de datos, [BD_ZIZI_Pagos.xlsx](https://github.com/LINK0N1/zizi-pagos/blob/main/BD_ZIZI_Pagos.xlsx) (también en la carpeta `Material/` de este repositorio), **son los que valida la página**. Por eso, para que funcione hay que usar los datos de ese archivo: el número de control tiene que existir en la hoja `Alumnos` y el usuario del personal en la hoja `Personal`.

El archivo tiene estas hojas:

| Hoja | Contenido |
|---|---|
| `Instrucciones` | Cómo se usa el archivo, el dígito verificador y las contraseñas |
| `Alumnos` | Alumnos de prueba con su número de control y dígito verificador |
| `Conceptos` | Catálogo de cuotas con los montos de la lista oficial 2026 y su tipo (Periodo, Constancia, Credencial) |
| `Adeudos` | Lo que debe cada alumno, con su referencia calculada |
| `Pagos` | Pagos ya registrados |
| `Personal` | Usuarios del personal: Usuario, Nombre, Rol (Contador o Jefatura) y Estatus (Activo o Baja) |
| `TarjetasPrueba` | Tarjetas de prueba y su resultado |

Las **contraseñas no están en el Excel**: cada persona la crea la primera vez que entra.

Ejemplos de la hoja `Alumnos`:

| Número de control | Alumno | Dígito verificador |
|---|---|---|
| 23690001 | Ana López | 7 |
| 22690002 | Carlos Pérez | 7 |
| 24690003 | Valentina Zúñiga | 8 |
| 21690004 | Diego Torres | 4 |
| 21690005 | Fernanda Rangel | 1 |

El **dígito verificador** también se pide al pagar con tarjeta, para confirmar que el pago es para ese número de control. Lo ves en tu ficha de pago, en el inicio, y está en la columna `NumVerificador` de la hoja `Alumnos`.

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

- **Cargar otra base de datos** (solo Jefatura): en el panel, «Cargar base de datos (Excel)» lee un archivo con el mismo formato que `BD_ZIZI_Pagos.xlsx`, incluida la hoja `Personal` (requiere internet). Si el archivo no trae esa hoja, se conserva el personal actual. Debe haber al menos una persona de Jefatura activa.
- **Empezar de cero** (solo Jefatura): «Restablecer prototipo» borra las contraseñas, los pagos nuevos y los trámites solicitados. La bitácora se conserva.
- **Acerca de nosotros:** enlace al pie de cada pantalla, con la presentación, el eslogan, la misión, la visión y los valores de ZIZI.

## Contenido de este repositorio

- `docs/` libro final y entregas en PDF (E1, E2, E3 y E4)
- `diseno/` BPMN TO-BE, arquitectura, wireframes y el primer prototipo
- `Material/` código y base de datos de la página
- `src/` código del proyecto (E4)

## Pila tecnológica y alcance

El prototipo está hecho con **HTML, CSS y JavaScript en un solo archivo**, con una base de datos en Excel que la página lee y valida. Se eligió así para poder abrirlo con un enlace y probarlo con usuarios reales dentro del plazo.

La arquitectura propuesta para una implementación real (E3) usa Python con Flask, SQLite, Stripe en modo de prueba, facturación simulada y Brevo para los correos.

### Límites del prototipo

- **No hay servidor.** Las contraseñas, los pagos nuevos, los trámites solicitados y la bitácora se guardan en el navegador de cada persona. Un pago hecho en un equipo no se ve desde otro.
- **La seguridad es de demostración.** El acceso del personal y los roles se validan en el navegador, no en un servidor, así que no sustituyen una autenticación real.
- **No está construida toda la automatización del área:** faltan la factura real, el correo, la conciliación con el banco y la cola de excepciones.
- **La conexión sí va cifrada:** GitHub Pages sirve la página con HTTPS, que protege los datos en tránsito.

## Pruebas

La entrega E4 documenta **30 casos de prueba** (más los casos de roles y de corte diario agregados después) y una prueba de usabilidad con 5 personas (SUS promedio de 76.5). Las pruebas automáticas se ejecutaron en Chromium.

## Aviso

Todos los datos son inventados. La pasarela y la facturación son simuladas. No se solicita ni se guarda ningún dato real de tarjeta.
