## Client ETL

Script ETL sencillo en **Python** para normalizar datos de personas y generar una salida en **JSON**.

### Tabla de contenidos

- [Client ETL](#client-etl)
  - [Tabla de contenidos](#tabla-de-contenidos)
  - [1. Descripción](#1-descripción)
  - [2. Requisitos y dependencias](#2-requisitos-y-dependencias)
  - [3. Estructura del proyecto](#3-estructura-del-proyecto)
  - [4. Clonado y ejecución rápida](#4-clonado-y-ejecución-rápida)
  - [5. Uso detallado](#5-uso-detallado)
    - [5.1. Indicando el archivo por línea de comandos](#51-indicando-el-archivo-por-línea-de-comandos)
    - [5.2. Seleccionando el archivo con un diálogo gráfico](#52-seleccionando-el-archivo-con-un-diálogo-gráfico)
  - [6. Salida (`outputs/result.json`)](#6-salida-outputsresultjson)
  - [7. Notas adicionales](#7-notas-adicionales)

### 1. Descripción

Este proyecto es un pequeño script ETL en Python que:

- Lee un archivo de texto de entrada con datos de personas.
- Normaliza y valida teléfonos y códigos postales.
- Estandariza los campos (nombre, apellido, teléfono, color, código postal).
- Genera un archivo `outputs/result.json` con:
  - **entries**: registros válidos ordenados por `lastname`, luego `firstname`.
  - **errors**: índices de líneas del archivo original que no se pudieron parsear o que tienen datos inválidos.

### 2. Requisitos y dependencias

- **Python**: 3.8 o superior.
- **Módulos estándar de Python** (ya vienen con la instalación de Python):
  - `json`
  - `re`
  - `sys`
  - `tkinter`
  - `operator` (`itemgetter`)

No se requieren dependencias externas ni archivo `requirements.txt`.

> Nota: En algunas instalaciones mínimas de Python en Windows, `tkinter` puede no venir preinstalado.  
> Si al ejecutar el script aparece un error de importación relacionado con `tkinter`, instala el paquete correspondiente a tu distribución de Python o reinstala Python asegurándote de incluir `tcl/tk`.

### 3. Estructura del proyecto

- `client_etl` → Script principal en Python.
- `inputs/` → Carpeta con archivos de ejemplo de entrada.
  - `sample_input.txt`
  - `generated_test_cases.txt`
- `outputs/` → Carpeta donde se crea el archivo `result.json` (se genera al ejecutar el script).

Si la carpeta `outputs/` no existe, créala manualmente antes de ejecutar el script:

```bash
mkdir outputs
```

### 4. Clonado y ejecución rápida

Desde una terminal:

```bash
git clone https://github.com/USUARIO/client_etl.git
cd client_etl
mkdir outputs  # solo la primera vez
python client_etl inputs/sample_input.txt
```

Sustituye `USUARIO` por tu usuario/organización real de GitHub.

### 5. Uso detallado

Puedes usar el script de dos maneras:

#### 5.1. Indicando el archivo por línea de comandos

Desde la carpeta raíz del proyecto (`client_etl`), ejecuta:

```bash
python client_etl inputs/sample_input.txt
```

O bien, con cualquier otro archivo de texto:

```bash
python client_etl ruta/al/archivo.txt
```

#### 5.2. Seleccionando el archivo con un diálogo gráfico

Si ejecutas el script sin argumentos, se abrirá un cuadro de diálogo para seleccionar el archivo de entrada:

```bash
python client_etl
```

Pasos:

1. Se abrirá una ventana de selección de archivo (Tkinter).
2. Selecciona el `.txt` que quieres procesar.
3. El script procesará el archivo y generará `outputs/result.json`.

### 6. Salida (`outputs/result.json`)

El archivo de salida tiene el formato:

```json
{
  "entries": [
    {
      "color": "Blue",
      "firstname": "John",
      "lastname": "Doe",
      "phonenumber": "703-742-0996",
      "zipcode": "10013"
    }
  ],
  "errors": [1, 4]
}
```

- **entries**: Lista de objetos válidos, con el teléfono ya normalizado al formato `xxx-xxx-xxxx`.
- **errors**: Lista de índices de línea (basados en 0) del archivo de entrada donde hubo error de formato o validación.

### 7. Notas adicionales

- Las líneas vacías del archivo de entrada se ignoran.
- Los códigos postales se consideran válidos solo si contienen exactamente 5 dígitos.
- Los números de teléfono se normalizan siempre que contengan exactamente 10 dígitos (después de eliminar caracteres no numéricos).
