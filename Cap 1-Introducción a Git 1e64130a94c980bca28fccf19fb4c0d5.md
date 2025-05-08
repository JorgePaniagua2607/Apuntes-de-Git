# Introducción a Git

Estado: Listo

- **Control de versiones**
    - Sistema que registra todo cambio en un código fuente de un proyecto
        - Para tener un **historial** de cambios (sabiendo quién y cuándo)
    - Con el fin de tener:
        - Rendimiento (solo tenemos lo necesario)
        - Seguridad (conserva todo lo que necesitamos)
        - Flexibilidad (evita el desarrollo lineal)
    - Fichero
        - Archivo que contiene datos, mismos que forman parte del proyecto
    - **Línea de tiempo**
        - 1990
            - Nace CVS, primer controlador de versiones (Antigua y actualmente obsoleta)
        - 2005
            
            Creación de Git 
            
            - Creada por Linus Torvalds por la necesidad de tener un controlador de versiones libre y gratuita (Reemplazo de BitKeeper, antecesor de Git)
        - 2008
            
            Creación de GitHub
            
            - Para que los desarrolladores guarden y accedan a otros proyectos que trabajan con Git
        - 2018
            
            Microsoft compra GitHub
            
            - Por 7.5 mil millones de dólares
        - 2024
            
            Git domina el mercado
            
            - GitHub implementa el soporte multimodelo de IA
            - Nace la herramienta GitHun Spark, que permite crear aplicaciones web en lenguaje natural
- **Git**
    - Es un sistema de control de versiones distribuido para:
        - Guardar **versiones del código** (como "puntos de control")
        - Comparar versiones y ver qué cambió
        - Recuperar versiones anteriores si algo sale mal
        - Trabajar en **ramas separadas** sin afectar el código principal
        - **Colaborar** con otras personas sin sobrescribir su trabajo
    - Qué significa que “sea distribuido”
        - Que al momento de clonar un repositorio se obtiene TODO, historial, archivos, ramas, versiones y para consultarlos, una vez clonados, no se requiere de internet
        - Comparación entre Git (distribuido) y CVS/SVN (centralizados)
        
        | Acción | Git (Distribuido) | CVS/SVN (Centralizados) |
        | --- | --- | --- |
        | ¿Tienes el historial? | Sí, completo | No, solo el servidor lo tiene |
        | ¿Necesitas internet? | No, puedes trabajar 100% localmente | Sí, necesitas conexión para casi todo |
        | ¿Colaboración eficiente? | Sí, incluso offline | Más limitado y lento |
        | ¿Redundancia? | Alta: muchos backups (copias) locales | Baja: un solo punto de fallo (el servidor) |
        - Lo que lo vuelve más independiente
- **Repositorio**
    - Base de datos de cambios de un proyecto
    - Carpeta donde se almacenan diferentes versiones de ficheros de un proyecto
    - **Repositorio remoto**
        - Se encuentra en un servidor (GitHub, GitLab) a diferencia de un repositorio local que está en una computadora
        - Se puede **acceder** al repositorio por internet y todo un equipo puede acceder al mismo, tal que lo controla un servidor
        - Tiene sus propias acciones como: `push`, `pull`, `fetch`, `clone`
        - Sirve para compartir cabios y colaborar
        
        <aside>
        💡
        
        Git te permite trabajar en un repositorio local y después sincronizarlo con uno remoto
        
        </aside>
        
    
- **Crear un repositorio local**
    
    ```bash
    git init nuevo-proyecto
    cd nuevo proyecto
    
    // si quieres ponerlo en una carpeta específica, basta con iniicar el comando en el directorio
    
    cd directorio-requerido/
    git init nuevo-proyecto
    
    // si quieres que la rama principal tenga otro nombre
    
    git init nuevo-proyecto --initial-branch=main
    ```
    
    Crea una carpeta con la funcionalidad git