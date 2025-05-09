# Push, pull y pull request

Estado: En curso

- **Diferencia entre git push y git pull**
    - git push
        - Sube los cambios del repositorio local al remoto (local → remoto)
    - git pull
        - Descarga y aplica los cambios del repositorio remoto al local (remoto → local)
- **git push**
    - git push -u
        - El parámetro -u o set-upstream es un indicador para aclarar a qué rama remota está conectada la rama local
        - Es correcto usarlo solo la primera vez que se sube una nueva rama al repo remoto (después git “ya sabe” qué rama está vinculada a la rama local)
    - git push --all
        - Es para subir TODAS las ramas locales al repositorio remoto especificado
        - Es correcto usarlo cuando quieres sincronizar un repositorio local con el remoto por completo. También cuando estamos migrando de un repositorio a otro
            - Hay que tomar en cuenta que esto sube todo, incluyendo ramas en desarrollo, ramas que ya no se usan, etc.
    - git push -f
        - Este incluye el parámetro -f o force, mismo que fuerza al push a realizarse, sobrescribiendo el historial remoto (sobrescribir está prohibido por seguridad, git bloquea por defecto si el historial ha cambiado)
        - Es correcto usarlo cuando manualmente reescribimos el historial con rebase y necesitamos actualizar el repo remoto. También cuando queremos deshacer commits remotos mediante reset
        - Una alternativa más segura en casos de trabajo en equipo:
            
            ```bash
            git push --force-with-lease origin rama
            ```
            
            Esto solo lo forzará si nadie más a subido algo nuevo
            
    - git push origin <rama1> <rama2><ramaN>
        - Este nos permite subir varias ramas a la vez (las que aclaremos)
        - Es correcto usarlo cuando queremos subir ramas que ya desarrollamos, funcionalidades que ya forman parte importante del proyecto, con el fin de compartirlas y respaldarlas en el repo remoto. También cuando estamos configurando un repositorio
- **git pull**
    - pullgit pull --set-upstream origin<rama>
        - Este descarga los cambios del repositorio remoto, fusiona los cambios con la rama actual y con el -u vincula la rama local para futuros git pull o git push
        - Se usa para cuando queremos descargar contenido y sincronizarla para futuros pull o push
        - Actualmente lo recomendable es:
            
            ```bash
            git branch --set-upstream-to=origin/<rama>
            ```
            
            Tal que este solo configura el seguimiento entre la rama local y la remota, sin hacer pull, para que después de estar seguros recién hacer un pull
            
    - git pull --all
        - Recorre cada rama remota configuradas, hace fetch de cada una y luego hace pull en la rama local actual pero desde todos las ramas remotas que existen
        - Se usa cuando tenemos varios repositorio remotos y queremos traer todos los cambios posibles desde todos ellos
- **Fork**
    - Un fork es una copia completa de un repositorio de Git creado en una cuenta para trabajar en el de manera independiente sin arriesgar el repositorio oirginal
    - Una copia con la que se puede hacer cambios libremente sin necesidad de permisos al original, probar ideas, proponer ideas mediante una pull request
    - Diferencia entre fork y clone
        - fork
            
            Crea una copia del repositorio en la cuenta de GigHub
            
        - clone
            
            Descarga el repositorio en la computadora
            
    - Conserva todo el historial de commits del repo original
    - Puedes sincronizar el fork con el repositorio original usando un remoto upstream
    - Usando fork
        1. Hacer un fork desde GitHub
            
            Vamos al repositorio original y buscamos en la esquina superior derecha el botón de fork y lo creamos
            
            GitHub hará un nuevo repositorio 
            
        2. Clonar el fork 
            
            ```bash
            git clone https://github.com/usuario/proyecto.git
            cd proyecto
            ```
            
        3. Configurar el remoto
            
            ```bash
            git remote add upstream https://github.com/usuario-original/proyecto.git
            ```
            
            Sirve para cambios más adelante para el repositorio original
            
            ```bash
            git remote -v
            ```
            
            Verificamos los remotos con este comando
            
        4. Creamos una rama para trabajar
            
            No es bueno trabajar en la main
            
        5. Crear una pull request
            1. Vamos al fork en GitHub
            2. Hacemos clic en “compare & pull request”
            3. Hacemos un mensaje 
            4. Creamos el pull request
        6. Sincronizamos el fork con el original
            
            ```bash
            git fetch upstream
            git checkout main # o con switch
            git merge upstream/main
            git push origin main
            ```
            
- **pull request**
    - Es para hacer una solicitud para que los cambios hechos en una rama sean revisados y después integrados (fusionados) en otra rama
    - Es usado para repositorio remotos
    - Sirve para:
        - Proponer cambios
        - Revisar código antes de fusionar
            - Otros miembros lo revisen y consideren
        - Ejecutar pruebas automáticas
            - Se activan pipelines que prueban el código antes de aprobarlo
        - Fusionar cambios con seguridad
            - Se fusiona solo al haber sido aprobada
    - Para usarlo
        1. Hacemos un fork
        2. Creamos una rama en el fork (o en el repositorio)
        3. Hacemos cambios y después commits y push
        4. En GitHub creamos una pull request desde la rama en la que estamos hacia la rama del proyecto original (la main por ejemplo)
        5. Se revisa por el equipo y se aprueba 
        6. Alguien con permisos hace el merge 
    - Para hacer una buena PR
        - El código debe tener un solo propósito
            - Más fácil de revisar y aceptar algo único y objetivo
        - Explica el Pull Request
            - Mostrar en video o imágenes la funcionalidad del código es bastante bueno
    - Para revisar una PR
        - Ser constructivos
        - Ser concretos y claros
        - Entender bien el contexto, no importa si no esta bonito, lo primero es que cumpla su cometido de la manera más eficiente