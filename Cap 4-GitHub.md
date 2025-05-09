# GitHub

Estado: Sin empezar

- **Diferencia entre Git y GitHub**
    - Git
        - Es un controlador de versiones
    - GitHub
        - Es un servicio en la nube que almacena y maneja repositorios de manera remota
        - Otras alternativas de servicio como GitHub son:
            - Bitbucket
            - GitLab
        
        | Plataforma | Propietario | Enfoque principal |
        | --- | --- | --- |
        | **GitHub** | Microsoft | Comunidad de código abierto y colaboración masiva. |
        | **Bitbucket** | Atlassian | Integración con herramientas de desarrollo (especialmente Jira y Trello). |
        | **GitLab** | GitLab Inc. | Plataforma DevOps todo en uno (ciclo completo de desarrollo). |
- **Repositorios remotos**
    - Son repositorios que se encuentran en un servidor y funcionan como un punto de sincronización entre repositorios locales
    - Enlazar un repositorio local con uno remoto
        - Primero creamos un repositorio remoto en GitHub
        - Una vez creado nos dará dos direcciones, una HTTPS y una SSH (últimamente la más usada)
            
            Nos quedamos con la SSH (copiamos el link proporcionado)
            
        - Después, en la terminal, ejecutamos:
            
            ```bash
            git remote add origin <el link que copiamos>
            ```
            
        
        💡 Un repositorio local puede estar enlazado a varios otros repositorios remotos
        
        - **Generar key SSH**
            - Para poder conectarse a un repositorio remoto, sin poner los datos cada vez y de manera segura, generamos una llave que nos permite ser identificados por el servidor.
            - Para generar una llave procedemos:
                
                ```bash
                ls ~/.ssh # verificamos si ya tenemos llaves o no (con nombre y tipo)
                ```
                
                - Hay dos tipos de llaves más utilizadas que son:
                    
                    RSA
                    
                    ```bash
                    ssh-keygen -t rsa -b 4096 -C "correo@ejemplo.com"
                    ```
                    
                    ED25519
                    
                    ```bash
                    ssh-keygen -t ed25519 -C "correo@ejemplo.com"
                    ```
                    
                    La diferencia es que la ED25519 es más rápida y pequeña que la RSA, pero esta última tiene total compatibilidad con sistemas modernos y antiguos que el anterior que su compatibilidad es con sistemas modernos
                    
            - Después seguimos con:
                
                ```bash
                cat ~/.ssh/id_rsa.pub # Copiamos la llave PUBLICA
                ```
                
            - Vamos a GitHub al apartado de [https://github.com/settings/keys](https://github.com/settings/keys):
                - Hacemos clic en **“New SSH key”**
                - Ponemos un nombre en **Title** (ej. *Mi laptop*)
                - En **Key**, pegamos la llave pública que copiamos
                - Hacemos clic en **“Add SSH key”**
            - Probamos la conexión
                
                ```bash
                ssh -T git@github.com # Seguidamente escribimos yes
                ```
                
    - Escribir en un repositorio remoto
        - Después de trabajar en un repositorio local, todos los cambios los escribimos en un repositorio remoto de esta manera:
            
            ```bash
            git push origin main
            ```
            
            Donde “origin” es un alias del repositorio remoto y el “main” la rama local que estamos subiendo
            
            ```bash
            git push -u origin main
            ```
            
            A este le aumentamos el parámetro -u que es la abreviación de `--set-upstream`. Indica que vas a **vincular tu rama local con una rama remota** del mismo nombre. Esto te permite luego usar solo `git push` o `git pull` sin especificar ramas
            
    - Rama remota
        - Primero creamos una rama local
        - Mandamos la rama al repositorio remoto:
            
            ```bash
            git push origin rama-para-repo-remoto
            ```
            
- **Clonar repositorios**
    - Para clonar un repositorio remoto debemos obtener su dirección
        - En GitHub, en el repositorio remoto desplegamos el botón “code”
        - Vamos a SSH (por preferencia)
        - Copiamos la dirección que nos da
    - En la terminal
        
        ```bash
        git clone <dirección SSH o HTTP>
        ```
        
- **Eliminar ramas**
    - Rama local
        
        ```bash
        git branch -d nombre-de-la-rama
        ```
        
    - Rama Remota
        
        ```bash
        git push origin --delete nombre-de-la-rama
        ```
        
    - Ramas locales que ya no existen en el repo remoto
        
        ```bash
        git fetch -p # Actualizamos la lista de ramas remotas
        ```
        
        Actualiza las ramas remotas y limpia las ramas eliminadas (actualiza y limpia)
        
        ```bash
        git remote prune origin
        ```
        
        Solo elimina referencias locales a ramas remotas ya eliminadas (rápido si ya está sincronizado todo)
        
- **Comandos para con repositorios remotos**
    - git fetch
        - Descarga los cambios del repositorio remoto SIN aplicarlos aún en la rama actual (no los mezcla aún)
        - Carga:
            - commits nuevos
            - Ramas nuevas
            - Referencias actualizadas
        - Para ver lo que ha cambiado en el servidor desde el último pull
            
            ```bash
            git log main..origin/main # Después de un git fetch 
            ```
            
        - Para aplicar esos cambios a la rama local
            
            ```bash
            git pull 
            ```
            
        - Comandos de fetch
            
            
            | Comando | Descripción |
            | --- | --- |
            | `git fetch` | Trae cambios de todos los remotos configurados. |
            | `git fetch origin` | Trae solo del remoto llamado `origin`. |
            | `git fetch --prune` | Además, elimina ramas remotas que ya no existen en el servidor. |
            | `git fetch --all` | Trae de todos los remotos, si tienes más de uno. |
    - git remote -v
        - Nos da una lista de repositorios remotos asociados a nuestro proyecto (tipo con los que “compartimos”)
        - Lo usamos más para:
            - Confirmar que estás conectado al repositorio correcto (ver la URL)
            - Ver si estás usando **HTTPS o SSH**
            - Revisar la URL del remoto antes de hacer `git push`
    - git remote add origin <url>
        - Es para conectar un repositorio local a uno remoto (agregando un nuevo repo remoto al proyecto)
        - Si queremos cambiar de URL
            
            ```bash
            git remote set-url origin <nueva-url>
            ```