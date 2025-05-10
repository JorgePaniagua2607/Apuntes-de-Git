# Introducción a Git

Este repositorio presenta los fundamentos del sistema de control de versiones **Git**, herramienta ampliamente utilizada en el desarrollo de software para gestionar el historial de cambios de un proyecto.

Git permite trabajar de forma distribuida, registrar cada modificación al código fuente, mantener múltiples versiones activas mediante ramas, y facilitar la colaboración entre desarrolladores sin riesgo de pérdida o sobrescritura de información.

Se abordan conceptos esenciales como:

- Inicialización de repositorios (`git init`)
- Seguimiento de archivos y confirmación de cambios (`git add`, `git commit`)
- Manejo de ramas (`git branch`, `git checkout`, `git merge`)
- Sincronización con repositorios remotos (`git push`, `git pull`, `git clone`)
- Comparación entre modelos de control de versiones centralizados y distribuidos

Este entorno sirve como base práctica para aplicar los principios de control de versiones, comprender el flujo de trabajo en Git y prepararse para su integración con plataformas como GitHub.

----------------------------------------------------------------------------------------------------------

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

----------------------------------------------------------------------------------------------------------

## Estados de Git

Git maneja tres estados principales para los archivos:

- **Modified**: El archivo fue cambiado pero aún no se ha preparado para confirmación. Si es nuevo y no está siendo rastreado, se considera "untracked".
- **Staged**: El archivo ha sido marcado para ser incluido en el próximo commit (usando `git add`).
- **Committed**: Los cambios han sido guardados en el historial local con `git commit`.

**Resumen del flujo:**
```bash
WORKING DIR → git add → STAGING AREA → git commit → REPO LOCAL

----------------------------------------------------------------------------------------------------------

# Git - Ramas y Conflictos

## Ramas en Git

### ¿Qué es una rama?
Una rama es una línea de desarrollo independiente. Permite trabajar funcionalidades o arreglos sin afectar el código principal (`main` o `master`).

### Crear ramas

**Con `checkout` (más antiguo y versátil):**

```bash
git checkout -b nueva-rama  # Crea y cambia a la nueva rama
```

**Con `switch` (más moderno y enfocado en ramas):**

```bash
git switch -c nueva-rama  # Crea y cambia a la nueva rama
```

### Cambiar de rama

```bash
git checkout nombre-rama
git switch nombre-rama
```

### Fusionar ramas

```bash
git checkout main
git merge nueva-rama
```

Opciones útiles:
- `--edit`: permite editar el mensaje del merge.
- `--no-commit`: no hace commit automático; se revisa antes de confirmar.

### Eliminar ramas

```bash
git branch -d rama       # Borra una rama fusionada
git branch -D rama       # Borra una rama no fusionada (forzado)
```

### Otros comandos útiles

- `git branch`: muestra ramas locales.
- `git branch -a`: muestra ramas locales y remotas.
- `git rebase`: reescribe el historial de una rama sobre otra (más limpio que merge).

Diferencia `merge` vs `rebase`:
- `merge` conserva el historial con bifurcaciones.
- `rebase` crea un historial lineal, sin commits de merge.

## Conflictos en Git

### Conflictos comunes

1. **Al hacer merge**
   - Dos ramas modifican las mismas líneas.
   - Git marca el conflicto para resolver manualmente.

2. **Al hacer rebase**
   - Se intenta reescribir commits que ya han cambiado.
   - Resolver como en merge.

3. **Al hacer pull**
   - Se traen cambios remotos que colisionan con cambios locales no confirmados.
   - Resolver como en merge.

4. **Al cambiar de rama**
   - Hay cambios no confirmados.
   - Solución: hacer commit o stash antes de cambiar.

5. **Al aplicar un stash**

```bash
git stash pop
```

- Si hay conflicto, el stash no se elimina.
- Ver contenido con:

```bash
git stash show -p
```

- Aplicar sin borrar:

```bash
git stash apply
```

- Eliminar stash:

```bash
git stash drop stash@{0}
git stash clear
```

## Buenas prácticas

- Hacer `pull` antes de comenzar a trabajar.
- Dividir el trabajo en ramas pequeñas y específicas.
- Hacer `stash` o `commit` antes de cambiar de rama.
- Evitar `rebase` en ramas compartidas si no se domina.

