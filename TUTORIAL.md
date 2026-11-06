# Tutorial de Uso y Dependencias del Proyecto: Ciberseguridad-ferroviaria-Urda

Este documento detalla las instrucciones de uso, configuración de entorno y gestión de repositorios para el proyecto.

## 1. Requisitos Previos y Herramientas

- **Git**: Sistema de control de versiones (instalado: 2.50.1).
- **GitHub CLI (`gh`)**: Herramienta de línea de comandos oficial de GitHub (instalada: 2.103.3).
- **GitHub Desktop**: Aplicación gráfica oficial de GitHub (instalada: 3.6.10).
- **Python 3.x**: Opcional según las necesidades del módulo o análisis de datos.

## 2. Repositorio en GitHub

El repositorio remoto está configurado y vinculado:
- **URL remota:** https://github.com/917543/Ciberseguridad-ferroviaria-Urda
- **Nombre:** `Ciberseguridad-ferroviaria-Urda`
- **Visibilidad actual:** Privado
- **Rama principal:** `main`

Para cambiar la visibilidad a público si lo deseas:
```powershell
gh repo edit 917543/Ciberseguridad-ferroviaria-Urda --visibility public
```

## 3. Estructura y Múltiples Repositorios

De acuerdo con el flujo de trabajo del proyecto, se utilizarán diferentes repositorios para una misma función o módulo. Mantén cada repositorio con su propio `TUTORIAL.md` actualizado con sus dependencias específicas.

## 4. Comandos Básicos de Git

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
- Obtener actualizaciones:
  ```powershell
  git pull origin main
  ```
