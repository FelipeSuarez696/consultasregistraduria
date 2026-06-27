# 🚀 Instrucciones de uso del notebook

## 📋 Requisitos previos

Antes de ejecutar el notebook, asegúrate de contar con un archivo que contenga las cédulas a consultar.

El programa admite los siguientes formatos de entrada:

* Archivo de texto (`.txt`) con una cédula por línea.
* Archivo CSV (`.csv`) con una columna llamada **cedula**.

### Ejemplo de archivo de texto (`.txt`)

```text
1234567890
9876543210
1122334455
```

### Ejemplo de archivo CSV (`.csv`)

```csv
cedula
1234567890
9876543210
1122334455
```

El archivo de entrada debe ubicarse en la siguiente ruta:

```text
/Volumes/datacedulas/bronze/zona_aterrizaje/
```

---

## ▶️ Ejecución del notebook

1. Verifica que el archivo de entrada exista en la ruta configurada.
2. Ejecuta las celdas del notebook en el orden establecido.
3. El programa leerá automáticamente las cédulas del archivo.
4. Realizará una consulta individual a la API de la Registraduría para cada documento.
5. Los resultados serán almacenados automáticamente en un archivo CSV.

---

## 🔄 Reanudación del proceso

Si la ejecución se interrumpe por alcanzar el tiempo máximo permitido o por cualquier otra causa, solo debes volver a ejecutar la celda de ejecución.

El programa continuará automáticamente desde la última cédula procesada gracias al archivo de progreso.

---

## 📄 Archivo de salida

Los resultados se almacenan en:

```text
/Volumes/datacedulas/bronze/zona_aterrizaje/salidascedula.csv
```

Cada registro contiene la siguiente información:

* Número de cédula.
* Resultado obtenido de la API.
* Fecha y hora de la consulta.

### Ejemplo del archivo generado

```csv
cedula,resultado,fecha_consulta
1234567890,VIGENTE,2026-06-25 14:32:10
9876543210,CANCELADA POR MUERTE,2026-06-25 14:32:15
1122334455,ERROR: HTTP 500,2026-06-25 14:32:20
```

---

## ⚙️ Consideraciones importantes

* El programa espera **4 segundos** entre consultas para evitar saturar la API.
* Cada solicitud tiene un tiempo máximo de espera de **10 segundos**.
* El progreso se guarda automáticamente después de procesar cada cédula.
* Si ocurre un error durante una consulta, este queda registrado en el archivo de resultados y el procesamiento continúa con la siguiente cédula.
* Cuando todas las consultas finalizan correctamente, el archivo temporal de progreso se elimina automáticamente.
