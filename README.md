# Introducción a Git
## Control de versiones

Git es un sistema distribuido que registra todos los cambios realizados en el código fuente de un proyecto. Permite mantener un historial detallado, saber quién hizo qué y cuándo, y facilita el trabajo colaborativo sin sobrescribir el trabajo de otros.

### Ventajas principales

- Guarda versiones del código (puntos de control).
- Permite comparar y recuperar versiones anteriores.
- Facilita trabajar con ramas independientes.
- No requiere internet para trabajar con el historial.
- Permite colaborar de forma eficiente, incluso sin conexión.

### Breve historia

- En los años 90 nace CVS (ya obsoleto).
- En 2005, Linus Torvalds crea Git.
- En 2008 aparece GitHub para alojar proyectos Git.
- En 2018, Microsoft compra GitHub.
- En 2024, Git integra IA y domina el mercado.

### Repositorio

Un repositorio es donde se almacenan los cambios del proyecto. Puede ser local (en tu equipo) o remoto (en plataformas como GitHub o GitLab). Git permite trabajar localmente y luego sincronizar con el repositorio remoto.

### Crear un repositorio local

```bash
git init nombre-del-proyecto
cd nombre-del-proyecto

# Si deseas usar otro nombre para la rama principal:
git init nombre-del-proyecto --initial-branch=main
