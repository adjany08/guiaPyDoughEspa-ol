# PyDough - entorno de desarrollo en WSL (Windows Subsystem for Linux)

Este documento guía paso a paso la configuración necesaria para trabajar con el proyecto **PyDough** en **Windows 10/11** utilizando **WSL** y **Visual Studio Code**. Incluye la instalación de dependencias, configuración del entorno y obtención de los recursos necesarios para ejecutar correctamente los notebooks de demostración.

---

## Requisitos Previos

### 1. Tener instalado WSL (Windows Subsystem for Linux)
Guía oficial para instalarlo:  
[https://learn.microsoft.com/es-es/windows/wsl/install](https://learn.microsoft.com/es-es/windows/wsl/install)

### 2. Tener instalado Visual Studio Code
Descarga aquí:  
[https://code.visualstudio.com/](https://code.visualstudio.com/)

### 3. Tener clonado el repositorio de PyDough
Puedes clonar el proyecto desde GitHub, copiar los archivos manualmente o utilizar la aplicación de GitHub desktop.

```bash
git clone https://github.com/tu-usuario/pydough.git
```

---

## Configuración de WSL

Para facilitar el uso de la terminal, especialmente el **copiar y pegar**, es necesario habilitar ciertas opciones:

1. Abre tu terminal WSL.
2. Haz clic derecho sobre la pestaña de la ventana y selecciona **Propiedades**.
3. Activa las siguientes casillas en la sección de edición:
   - `Usar CTRL+MAYUS+C o V como copiar y pegar`.

Esto facilitará ejecutar comandos desde esta guía.

---

## Configuración en Visual Studio Code

1. Instala la **extensión de WSL** para VS Code:
   - Abre la paleta de comandos (`Ctrl+Shift+P`)
   - Busca `WSL: Install Extension`

2. Desde tu terminal WSL, accede al proyecto y abre VS Code con:

```bash
code .
```

Esto abrirá la carpeta actual con soporte completo para desarrollo en WSL.

---

## Configuración del entorno virtual y PyDough

En tu consola WSL, navega al directorio del proyecto y ejecuta:

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv -y

python3 -m venv pydough-dev-venv
source pydough-dev-venv/bin/activate

pip install --upgrade pip
pip install pydough
```

---

## Copiar el Proyecto desde Windows a WSL (recomendado)

Puedes copiar el proyecto clonado al entorno WSL con el siguiente comando (el proyecto será copiado a tu ruta actual):

```bash
cp -r [ruta del proyecto]
```
---

## Descargar la base de datos utilizada para los ejemplos
Para ejecutar los notebooks correctamente, debes asegurarte de tener el archivo `tpch.db` en la carpeta `demos/` o en algún directorio conocido. Para esto tenemos las siguientes opciones:

### Opción 1: Descargar la base de datos manualmente

```bash
cd demos/
wget https://github.com/lovasoa/TPCH-sqlite/releases/download/v1.0/TPC-H.db -O tpch.db
```

### Opción 2: Usar el script de configuración

1. Asegúrate de estar en la carpeta `demos/` y tener el archivo `setup.thcp.sh`.
2. Ejecuta los siguientes comandos:

```bash
dos2unix setup.thcp.sh
chmod +x setup.thcp.sh
./setup.thcp.sh
```

---

## IMPORTANTE: Conexión a la base de datos

Asegúrate de actualizar esta línea en los notebooks para reflejar la ubicación real del archivo `tpch.db`:

```python
pydough.active_session.connect_database("sqlite", database="../../tpch.db")
```

---

## Prueba Final

Ya con esto tenemos todo lo necesario para ejecutar los notebooks con los ejemplos de PyDough.

---

##  Recomendaciones

- Se recomienda mantener el entorno virtual activo cada vez que se trabajen notebooks:
  
  ```bash
  source pydough-dev-venv/bin/activate
  ```


---



