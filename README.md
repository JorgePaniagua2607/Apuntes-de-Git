# Introducción a Git: Control de Versiones

Git es un sistema de control de versiones distribuido diseñado para registrar y gestionar los cambios realizados en el código fuente de un proyecto. Permite mantener un historial detallado de las modificaciones, identificando quién hizo qué cambios y cuándo, lo que mejora significativamente la colaboración en equipos de desarrollo.

## ¿Por qué usar Git?

- 🕓 Historial completo de cambios.
- 🔐 Seguridad y control sobre el código.
- 🤝 Trabajo colaborativo sin conflictos.
- ⚡ Alto rendimiento y flexibilidad.

## Breve Historia

- **1990**: Surge CVS (actualmente obsoleto).
- **2005**: Linus Torvalds crea Git como alternativa libre a BitKeeper.
- **2008**: Nace GitHub como plataforma para alojar repositorios remotos.
- **2024**: Git se consolida como el estándar con integración de IA y herramientas como GitHub Spark.

## Conceptos Clave

- **Repositorio**: Base de datos que almacena versiones del proyecto (puede ser local o remoto).
- **Estados en Git**:
  - `Modified`: Archivo cambiado pero no preparado.
  - `Staged`: Cambios listos para confirmar.
  - `Committed`: Cambios guardados en el historial.
- **Commit**: Registro puntual de cambios.
- **Branch (rama)**: Línea de desarrollo independiente.
- **Merge**: Integración de una rama a otra.

## Git vs. GitHub

- **Git**: Herramienta local de control de versiones.
- **GitHub**: Plataforma en la nube para gestionar repositorios remotos.
  - Alternativas: GitLab, Bitbucket.

## Flujo de Trabajo Básico

```bash
# Clonar un repositorio
git clone <url-del-repositorio>

# Crear y cambiar de rama
git branch nueva-rama
git checkout nueva-rama

# Agregar y confirmar cambios
git add .
git commit -m "Mensaje descriptivo"

# Subir y descargar cambios
git push
git pull
