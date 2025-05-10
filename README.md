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
```

----------------------------------------------------------------------------------------------------------

## Estados de Git

Git maneja tres estados principales para los archivos:

- **Modified**: El archivo fue cambiado pero aún no se ha preparado para confirmación. Si es nuevo y no está siendo rastreado, se considera "untracked".
- **Staged**: El archivo ha sido marcado para ser incluido en el próximo commit (usando `git add`).
- **Committed**: Los cambios han sido guardados en el historial local con `git commit`.

**Resumen del flujo:**
```bash
WORKING DIR → git add → STAGING AREA → git commit → REPO LOCAL
```

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

----------------------------------------------------------------------------------------------------------

# Git y GitHub

## Diferencia entre Git y GitHub

**Git** es un sistema de control de versiones distribuido, mientras que **GitHub** es un servicio en la nube para almacenar y manejar repositorios Git de forma remota.

### Alternativas a GitHub

- **Bitbucket**: Integración con herramientas de desarrollo como Jira y Trello.
- **GitLab**: Plataforma DevOps todo en uno, que incluye CI/CD, repositorios, etc.

## Repositorios remotos

Los repositorios remotos son aquellos almacenados en un servidor y sirven como punto de sincronización entre repositorios locales.

## Enlazar repositorio local con uno remoto

1. Crea un repositorio en GitHub.
2. Copia la URL SSH del repositorio.
3. En la terminal, enlaza el repositorio local con el remoto:

```bash
git remote add origin <URL-SSH>
```

> Un repositorio local puede estar enlazado a varios repositorios remotos.

## Generar llave SSH

Verifica si ya existen llaves:

```bash
ls ~/.ssh
```

Genera una nueva llave SSH:

- **RSA** (compatible con todo):

```bash
ssh-keygen -t rsa -b 4096 -C "correo@ejemplo.com"
```

- **ED25519** (más rápida y moderna):

```bash
ssh-keygen -t ed25519 -C "correo@ejemplo.com"
```

Copia la clave pública:

```bash
cat ~/.ssh/id_rsa.pub
```

Agrega la llave pública en GitHub: [https://github.com/settings/keys](https://github.com/settings/keys)

Prueba la conexión:

```bash
ssh -T git@github.com
```

## Subir cambios a repositorio remoto

Para subir los cambios al repositorio remoto, usa:

```bash
git push origin main
```

O si es la primera vez que subes la rama:

```bash
git push -u origin main
```

## Crear y subir rama remota

1. Crea una nueva rama local:

```bash
git checkout -b nombre-rama
```

2. Sube la rama al repositorio remoto:

```bash
git push origin nombre-rama
```

## Clonar repositorio remoto

1. Copia la URL SSH desde GitHub.
2. Clona el repositorio con el siguiente comando:

```bash
git clone <URL-SSH>
```

## Eliminar ramas

- **Eliminar rama local**:

```bash
git branch -d nombre-rama
```

- **Eliminar rama remota**:

```bash
git push origin --delete nombre-rama
```

- **Limpiar ramas eliminadas en remoto**:

```bash
git fetch -p
git remote prune origin
```

## Comandos con repositorios remotos

- **Ver remotos configurados**:

```bash
git remote -v
```

- **Agregar remoto**:

```bash
git remote add origin <url>
```

- **Cambiar URL del remoto**:

```bash
git remote set-url origin <nueva-url>
```

## git fetch vs git pull

- `git fetch`: descarga los cambios del repositorio remoto sin aplicarlos en la rama actual.
- `git pull`: descarga y aplica los cambios del repositorio remoto en la rama actual.

Comandos adicionales para fetch:

```bash
git fetch
git fetch origin
git fetch --prune
git fetch --all
```

Ver diferencias entre la rama local y la remota:

```bash
git log main..origin/main
```

Aplicar los cambios:

```bash
git pull
```

----------------------------------------------------------------------------------------------------------

# Git: Push, Pull y Pull Request

## Diferencia entre `git push` y `git pull`

- **git push**: Sube los cambios del repositorio local al remoto (local → remoto).
- **git pull**: Descarga y aplica los cambios del repositorio remoto al local (remoto → local).

## Comandos comunes de `git push`

- **`git push -u`**: Vincula la rama local a una rama remota, útil solo la primera vez que se sube una nueva rama al repositorio remoto.
- **`git push --all`**: Sube todas las ramas locales al repositorio remoto.
- **`git push -f`**: Fuerza el push y sobrescribe el historial remoto. Se usa para actualizar el repositorio después de un `rebase` o `reset`.
- **`git push --force-with-lease`**: Una alternativa más segura para no sobrescribir cambios de otros usuarios.
- **`git push origin <rama1> <rama2> ...`**: Sube múltiples ramas a la vez.

## Comandos comunes de `git pull`

- **`git pull --set-upstream origin <rama>`**: Descarga y fusiona cambios del repositorio remoto y vincula la rama local para futuros `git pull` o `git push`.
- **`git branch --set-upstream-to=origin/<rama>`**: Configura el seguimiento entre la rama local y remota sin hacer un `git pull` directamente.
- **`git pull --all`**: Hace `fetch` y `pull` de todas las ramas remotas.

## Fork y Clone

### Fork

Un **fork** es una copia de un repositorio en tu cuenta de GitHub que puedes modificar sin afectar al repositorio original. Es útil para trabajar de manera independiente o proponer cambios a proyectos de otros.

### Clone

Un **clone** es una copia local del repositorio completo, que puedes descargar a tu computadora. Mantiene el historial de commits y puedes sincronizarlo con el repositorio original.

### Diferencia entre Fork y Clone

- **Fork**: Crea una copia del repositorio en tu cuenta de GitHub.
- **Clone**: Descarga el repositorio a tu máquina local.

## Usando Fork

1. Haz un fork desde GitHub: En el repositorio original, haz clic en "Fork".
2. Clona el fork a tu máquina local:

   ```bash
   git clone https://github.com/usuario/proyecto.git
   cd proyecto
   ```

3. Configura el remoto para sincronizar con el repositorio original:

   ```bash
   git remote add upstream https://github.com/usuario-original/proyecto.git
   ```

4. Crea una nueva rama para trabajar (evita trabajar en `main`).

5. Sincroniza tu fork con el repositorio original:

   ```bash
   git fetch upstream
   git checkout main
   git merge upstream/main
   git push origin main
   ```

## Pull Request (PR)

Un **Pull Request** es una solicitud para que los cambios hechos en una rama sean revisados e integrados en otra rama (usualmente la rama principal del repositorio original).

### ¿Cómo hacer una Pull Request?

1. Haz un fork del repositorio.
2. Crea una rama en el fork, haz cambios y realiza `commit` y `push`.
3. En GitHub, crea una pull request desde tu rama hacia la rama del repositorio original.
4. La PR será revisada por el equipo y, si se aprueba, se fusionará.

### Consejos para hacer una buena PR

- Asegúrate de que el código tenga un solo propósito y sea fácil de revisar.
- Explica claramente los cambios realizados.
- Si es posible, muestra videos o imágenes que ilustren la funcionalidad.
- Sé constructivo y claro en los comentarios de la revisión.

### Para revisar una PR

- Sé concreto y claro, entendiendo bien el contexto del cambio.
- El código debe ser eficiente y cumplir su cometido, no importa si no está perfecto visualmente.

----------------------------------------------------------------------------------------------------------

# Git Flow

## ¿Qué es GitFlow?

GitFlow es una estrategia de ramificación para Git propuesta por Vincent Driessen. Está diseñada para gestionar el desarrollo de software de manera ordenada, especialmente útil en proyectos con ciclos de versiones definidos.

## Ramas principales

- **main**: Contiene el código en producción. Cada commit en esta rama representa una versión estable.
- **develop**: Contiene el código en desarrollo, donde se integran nuevas funcionalidades antes de pasar a producción.

## Ramas de soporte

- **feature/**: Usadas para desarrollar nuevas funcionalidades. Se crean desde `develop` y se fusionan de nuevo en `develop`. Ejemplo: `feature/login`, `feature/pago-online`.
- **release/**: Preparan una nueva versión de producción. Se crean desde `develop`, y una vez lista, se fusionan en `main` y `develop`. Ejemplo: `release/v1.0.0`.
- **hotfix/**: Se usan para corregir errores críticos directamente en producción. Se crean desde `main` y se fusionan en `main` y `develop`. Ejemplo: `hotfix/error-login`.

## Flujo básico de trabajo

1. Clona el repositorio y cámbiate a la rama `develop`.
2. Crea una rama `feature/` para tu funcionalidad.
3. Cuando termines, haz `merge` a `develop`.
4. Al cerrar un ciclo de desarrollo, crea una rama `release/`.
5. Realiza pruebas y ajustes finales en `release/`.
6. Cuando esté lista, haz `merge` a `main` y etiqueta con la versión.
7. También haz `merge` de `release/` a `develop`.
8. Si hay errores en producción, crea una rama `hotfix/`.

## Ventajas de GitFlow

- Organización clara del proceso de desarrollo.
- Facilita el trabajo en equipo.
- Ideal para proyectos con entregas y versiones definidas.

## Cuándo evitar GitFlow

En proyectos muy pequeños o de desarrollo continuo (como en DevOps), puede ser excesivo. Alternativas más simples incluyen **GitHub Flow** o **Trunk Based Development**.
