# Tutorial de Uso y Dependencias del Proyecto

Este documento detalla las instrucciones de uso, configuración de entorno y gestión de repositorios para el proyecto.

## 1. Requisitos Previos y Herramientas

- **Git**: Sistema de control de versiones (instalado en el sistema).
- **GitHub CLI (`gh`)**: Herramienta de línea de comandos oficial de GitHub (instalada en el sistema).
- **Python 3.x** (opcional según las necesidades del módulo).

## 2. Configuración con GitHub

Para sincronizar este repositorio local con tu cuenta de GitHub, sigue estos pasos:

### Opción A: Mediante GitHub CLI (`gh`)
1. Iniciar sesión en GitHub desde la terminal:
   ```powershell
   gh auth login
   ```
   Selecciona `GitHub.com`, protocolo `HTTPS` y sigue las instrucciones para autenticarte mediante el navegador web o tu token.

2. Crear y subir el repositorio a GitHub:
   ```powershell
   gh repo create tosferina26 --public --source=. --remote=origin --push
   ```
   *(O usa `--private` si prefieres que el repositorio sea privado).*

### Opción B: Mediante GitHub Desktop
Si prefieres una interfaz gráfica, puedes instalar GitHub Desktop ejecutando:
```powershell
winget install --id GitHub.GitHubDesktop -e
```
Una vez instalado, abre GitHub Desktop, añade este repositorio local (`File > Add Local Repository`) y haz clic en **Publish repository**.

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
