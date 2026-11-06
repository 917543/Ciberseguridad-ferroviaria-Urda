# Tutorial de Uso y Dependencias del Proyecto: Ciberseguridad-ferroviaria-Urda

Este documento detalla las instrucciones de uso, configuración de entorno y gestión de repositorios para el proyecto de tesis en Ciberseguridad Ferroviaria.

## 1. Requisitos Previos y Herramientas

- **Git**: Sistema de control de versiones (instalado: 2.50.1).
- **GitHub CLI (`gh`)**: Herramienta de línea de comandos oficial de GitHub (instalada: 2.103.3).
- **GitHub Desktop**: Aplicación gráfica oficial de GitHub (instalada: 3.6.10).
- **Python 3.x**: Recomendado para scripts de modelado, simulación de inyección de fallos o análisis estadístico de RAMS.
- **Herramientas de Análisis Estático / Formal (futuro)**: SonarQube, Frama-C, Scade o UPPAAL para verificación de estados y deadlocks (CWE-833).

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

## 3. Estructura Documental y Múltiples Repositorios

De acuerdo con el flujo de trabajo del proyecto, se utilizarán diferentes repositorios para una misma función o módulo.
Estructura actual del repositorio:
- [`docs/estudio_funcional_sil4_freno.md`](file:///c:/Users/josea_3vii47j.DESKTOP-I95E237/Desktop/tosferina26/docs/estudio_funcional_sil4_freno.md): Estudio funcional y propuesta de vía de respaldo para vulnerabilidades SIL 4 (CWE-833, CWE-400) y pérdida de comandancia neumática.
- [`AGENTS.md`](file:///c:/Users/josea_3vii47j.DESKTOP-I95E237/Desktop/tosferina26/AGENTS.md): Definición de rol y directrices del asistente técnico (Claudio).
- [`README.md`](file:///c:/Users/josea_3vii47j.DESKTOP-I95E237/Desktop/tosferina26/README.md): Portada y resumen general.

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
