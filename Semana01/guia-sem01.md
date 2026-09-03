# Módulo OS
El módulo os proporciona una **API de bajo nivel para interactuar con el sistema operativo**. Su diseño busca portabilidad entre plataformas (Windows, Linux, macOS), aunque ciertas funciones pueden variar según el sistema subyacente, con cambios mínimos.

**Arquitectura y Portabilidad**
Cuando hablamos de arquitectura y portabilidad en Python, nos referimos a cómo el lenguaje logra que un mismo programa pueda ejecutarse en distintos sistemas operativos (Windows, Linux, Mac) sin que el programador tenga que cambiar el código.
Esto es posible porque Python actúa como una capa intermedia entre el código que escribimos y las funciones específicas del sistema operativo. Así, el desarrollador trabaja con instrucciones universales, mientras que Python se encarga de traducirlas al lenguaje que entiende cada sistema.
* Abstracción dinámica: durante la compilación detecta el SO. (patrón de diseño)
* Módulos específicos (capa comunicarse con diferentes so: posix, nt)
* Importación condicional: modulo especifico para cada SO

```python
# Cargar el módulo OS
import os

# Documentación de un módulo
help(os)

# Lista de elementos que componen el módulo
dir(os)
```

## 🔑 Propiedades principales de `os`

- **`os.name`**  
  Devuelve el nombre del sistema operativo dependiente del módulo importado.  
  - `"posix"` → sistemas tipo Unix/Linux/Mac.  
  - `"nt"` → Windows.  

- **`os.sep`**  
  Separador de directorios usado por el sistema operativo.  
  - `"/"` en Linux/Mac.  
  - `"\\"` en Windows.  

- **`os.pathsep`**  
  Separador usado en las variables de entorno para separar rutas.  
  - `":"` en Linux/Mac.  
  - `";"` en Windows.  

- **`os.extsep`**  
  Separador de extensión de archivos. Normalmente `"."`.  

- **`os.curdir`**  
  Representa el directorio actual. Generalmente `"."`.  

- **`os.pardir`**  
  Representa el directorio padre. Generalmente `".."`.  

- **`os.linesep`**  
  Carácter de salto de línea usado por el sistema operativo.  
  - `"\n"` en Linux/Mac.  
  - `"\r\n"` en Windows.  

- **`os.environ`**  
  Diccionario que contiene las variables de entorno del sistema.

## 🔒 Laboratorio N° 01: Ejercicios Uso de Módulo `os` en colab
### 🔒 Uso de Propiedades

```python
import os

# Nombre del sistema operativo
print("Sistema operativo:", os.name)
# Separadores
print("Separador de directorios:", os.sep)
print("Separador de rutas en variables de entorno:", os.pathsep)
print("Separador de extensión:", os.extsep)
# Directorios especiales
print("Directorio actual (curdir):", os.curdir)
print("Directorio padre (pardir):", os.pardir)
# Salto de línea repr() convierte ese valor en una representación legible
print("Salto de línea:", repr(os.linesep))
# Salto de línea repr() convierte ese valor en una representación legible
print("Salto de línea:", repr(os.linesep))
```
## 📂 Funciones de manejo de directorios y archivos
- `os.getcwd()` → devuelve el directorio actual.  
- `os.chdir(path)` → cambia el directorio de trabajo.  
- `os.listdir(path)` → lista archivos y carpetas.  
- `os.makedirs(path, exist_ok=True)` → crea directorios recursivamente.  
- `os.remove(path)` → elimina un archivo.  
- `os.rmdir(path)` → elimina un directorio vacío.  
- `os.rename(src, dst)` → renombra archivo o carpeta.  
- `os.stat(path)` → devuelve información del archivo (tamaño, permisos, fechas).  

## ⚙️ Funciones de procesos y sistema
- `os.system(command)` → ejecuta un comando del sistema.  
- `os.startfile(path)` (solo Windows) → abre un archivo con la aplicación predeterminada.  
- `os.execv(path, args)` → reemplaza el proceso actual por otro.  
- `os.fork()` (Unix) → crea un nuevo proceso.  
- `os.kill(pid, sig)` → envía una señal a un proceso.  
- `os.getpid()` → obtiene el ID del proceso actual.  
- `os.getppid()` → obtiene el ID del proceso padre.  

## 🌍 Funciones de entorno
- `os.getenv(key, default)` → obtiene el valor de una variable de entorno.  
- `os.putenv(key, value)` → establece una variable de entorno.  

## 🖥️ Funciones de información del sistema
- `os.uname()` (Unix) → información detallada del sistema.  
- `os.cpu_count()` → número de núcleos de CPU disponibles.  

## 🔒 Funciones de permisos y acceso
- `os.chmod(path, mode)` → cambia permisos de un archivo.  
- `os.access(path, mode)` → verifica permisos de acceso.  
## 🔒 Laboratorio N° 01: Ejercicios Uso de Módulo `os` en colab
### 🔒 Uso de Funciones
```python
from google.colab import drive
drive.mount('/content/drive')

# 1. `os.getcwd()` → obtener directorio actual
print("Directorio actual:", os.getcwd())
# 2. `os.chdir()` → cambiar directorio
os.chdir("/content/drive/MyDrive")
# 3. `os.listdir(path)` → listar archivos
print("Contenido de MyDrive:", os.listdir("/content/drive/MyDrive"))
# 4. Crear directorios - "/content/drive/MyDrive/Padre/Hijo"
dir_path = "/content/drive/MyDrive/DirectorioPrueba"
os.makedirs(dir_path, exist_ok=True)
# 5 Crear un directorio
os.mkdir("/content/drive/MyDrive/DirectorioPrueba2")
# 6. Crear un archivo de texto dentro de esa carpeta
file_path = "/content/drive/MyDrive/PruebasOS/ejemplo.txt"
with open(file_path, "w") as f:
    f.write("Este es un archivo de prueba creado con Python.")
# 7. Eliminar el archivo creado
os.remove(file_path)
print("Archivo eliminado:", file_path)
### 8. `os.environ` → variables de entorno
print("Variable HOME:", os.environ.get("HOME"))
print("Variable PATH (primeros 100 caracteres):", os.environ.get("PATH")[:100], "...")
```
## Práctica Calificada 01: Gestor de proyectos con auditoría de archivos

### Objetivo
Construir un script que simule un **gestor de proyectos** en Google Drive, usando funciones de `os` para crear, listar, renombrar, mover, eliminar y auditar archivos y directorios.  

---

### Descripción de la práctica
El programa debe:

1. **Detectar el sistema operativo** con `os.name` y mostrar un mensaje de bienvenida adaptado.  
2. **Crear una carpeta principal** llamada `ProyectoOS`.  
3. **Generar subcarpetas**: `Entradas`, `Procesados`, `Errores`, `Backups`.  
4. **Crear archivos de texto** en `Entradas` con nombres `entrada1.txt`, `entrada2.txt`, etc., y escribir contenido simulado.  
5. **Listar todo el contenido** de la carpeta principal con `os.listdir()` y mostrarlo en pantalla.  
6. **Renombrar un archivo** de `Entradas` a `entrada_procesada.txt` y moverlo a la carpeta `Procesados`.  
7. **Simular un error**: mover un archivo inexistente y capturar la excepción con un mensaje claro.  
8. **Auditar los archivos**: usar `os.stat()` para mostrar tamaño y fecha de creación de cada archivo en `Procesados`.  
9. **Crear un backup**: copiar los archivos de `Procesados` a `Backups` (puede ser con `os.rename()` o `shutil.copy()`).  
10. **Eliminar selectivamente**: borrar un archivo de `Errores` y luego eliminar toda la estructura de carpetas con `os.rmdir()` (asegurándose de que estén vacías).  
11. **Consultar variables de entorno**: mostrar `HOME` y los primeros 80 caracteres de `PATH`. 