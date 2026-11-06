# Tutorial de Uso y Dependencias del Proyecto

Este documento detalla las instrucciones de uso, configuración de entorno y gestión de repositorios para el proyecto.

## 1. Requisitos Previos y Herramientas

- **Git**: Sistema de control de versiones (instalado: 2.50.1).
- **GitHub CLI (`gh`)**: Herramienta de línea de comandos oficial de GitHub (instalada: 2.103.3).
- **GitHub Desktop**: Aplicación gráfica oficial de GitHub (instalada: 3.6.10).
- **Python 3.x**: Opcional según las necesidades del módulo.

## 2. Configuración con GitHub

Para sincronizar este repositorio local con tu cuenta de GitHub, puedes usar cualquiera de estas dos opciones:

### Opción A: Mediante GitHub Desktop (Recomendada con Interfaz Gráfica)
1. Abre la aplicación **GitHub Desktop** desde el menú Inicio de Windows.
2. Inicia sesión con tu cuenta de GitHub (`File > Options > Accounts > Sign in`).
3. Añade este repositorio:
   - Ve a `File` > `Add Local Repository...`
   - Selecciona la ruta: `C:\Users\josea_3vii47j.DESKTOP-I95E237\Desktop\tosferina26`
4. Haz clic en el botón superior **Publish repository** para crearlo en tu cuenta de GitHub (puedes marcarlo como público o privado).

### Opción B: Mediante GitHub CLI (`gh`)
1. Inicia sesión desde la terminal:
   ```powershell
   gh auth login
   ```
   Selecciona `GitHub.com` -> `HTTPS` -> autenticación web.

2. Crea y publica el repositorio en GitHub directamente:
   ```powershell
   gh repo create tosferina26 --public --source=. --remote=origin --push
   ```
   *(Cambia `--public` por `--private` si prefieres que sea privado).*

## 3. Estructura y Múltiples Repositorios

De acuerdo con el flujo de trabajo del proyecto, se utilizarán diferentes repositorios para una misma función/módulo. Mantén cada repositorio con su propio `TUTORIAL.md` actualizado con sus dependencias específicas.

## 3. Comandos Básicos de Git

- Comprobar estado:
  ```powershell
  git status
  ```
- Añadir cambios y crear commit:
  ```powershell
  git add .
  git commit -m "Mensaje descriptivo"
  ```
- Subir cambios a la rama remota:
  ```powershell
  git push origin main
  ```

