# Git Flow

Estado: En curso

- **Qué es GitFlow?**
    - GitFlow es una **estrategia de ramificación** para Git, propuesta por Vincent Driessen. Está diseñada para gestionar de forma ordenada el desarrollo de software, especialmente útil en proyectos con ciclos de versión definidos.
- **Ramas principales**
    1. **`main`**
        - Contiene el código en producción.
        - Cada commit en esta rama representa una versión estable.
    2. **`develop`**
        - Contiene el código en desarrollo.
        - Es donde se integran nuevas funcionalidades antes de pasar a producción.
- **Ramas de soporte**
    1. **`feature/`**
        - Usadas para desarrollar nuevas funcionalidades.
        - Se crean desde `develop` y se fusionan de nuevo en `develop`.
        - Ej: `feature/login`, `feature/pago-online`.
    2. **`release/`**
        - Preparan una nueva versión de producción.
        - Se crean desde `develop`, y una vez lista, se fusionan en `main` y `develop`.
        - Ej: `release/v1.0.0`.
    3. **`hotfix/`**
        - Se usan para corregir errores críticos directamente en producción.
        - Se crean desde `main` y se fusionan en `main` y `develop`.
        - Ej: `hotfix/error-login`.
- **Flujo básico de trabajo**
    1. Clonas el repositorio y te cambias a `develop`.
    2. Creas una rama `feature/` para tu funcionalidad.
    3. Cuando terminas, haces merge a `develop`.
    4. Al cerrar un ciclo de desarrollo, creas una rama `release/`.
    5. Se hacen pruebas y ajustes finales en `release/`.
    6. Cuando está lista, haces merge a `main` y etiquetas con la versión.
    7. También haces merge de `release/` a `develop`.
    8. Si hay errores en producción, se crea un `hotfix/`.
- **Ventajas de GitFlow**
    - Organización clara del proceso de desarrollo.
    - Facilita el trabajo en equipo.
    - Ideal para proyectos con entregas y versiones definidas.
- **Cuándo evitar GitFlow?**
    - En proyectos muy pequeños o de desarrollo continuo (como en DevOps), puede ser excesivo.
    - Alternativas más simples: **GitHub Flow** o **Trunk Based Development**.