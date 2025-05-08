# Ramas, merge y conflictos

Estado: En curso

- **Rama**
    - Línea de desarrollo independiente
        - Se puede trabajar funcionalidades, arreglar errores SIN afectar al código principal (la rama main o master)
        - Para trabajar libremente sin romper el código principal
        - Después se puede fusionar esta a la main (merge)
    - Crear Ramas
        - **Diferencia entre checkout y switch**
            - checkout
                - Es antiguo y más complejo, hace más cosas, como ser:
                    - Crear y cambiar rama
                        
                        ```bash
                        git checkout -b nueva-rama
                        
                        # "-b" es abreviación de branch. Este indica que cree una nueva rama
                        ```
                        
                    - Cambiar de rama
                        
                        ```bash
                        git checkout nombre-de-la-rama
                        ```
                        
                    - Restaurar archivos específicos
                        
                        ```bash
                        git checkout HEAD archivo.txt
                        ```
                        
                    - Ir a commits específicos
                        
                        ```bash
                        git checkout abc1234
                        
                        # Sin estar en alguna rama 
                        ```
                        
            - switch
                - Es más moderno y está para simplificar el trabajo con ramas
                - Este puede:
                    - Cambiar de rama
                    - Crear rama
                - No puede:
                    - Restaurar archivos (para eso checkout o restore)
                    - Ir a commits específicos (para eso solo checkout)
                    - Restaurar archivos desde un commit (para eso checkout o restore -- source)
                    - Descartar cambios en archivos (para eso checkout o restore)
            
            | Acción | `checkout` | `switch` |
            | --- | --- | --- |
            | Cambiar de rama | ✅ | ✅ |
            | Crear y cambiar a nueva rama | ✅ | ✅ (`-c`) |
            | Restaurar archivos individuales | ✅ | ❌ |
            | Ir a un commit específico (detached HEAD) | ✅ | ❌ (por diseño) |
        - **Crear Rama (con checkout)**
            - Para agregar una nueva funcionalidad:
                
                ```bash
                git branch nueva-funcionalidad  #crea la rama pero no cambia a ella 
                git checkout nueva-funcionalidad  #cambia a la rama ya creada
                
                git checkout -b nueva-rama  #crea y cambia a la rama 
                ```
                
                El “checkout” es el que actualiza al puntero HEAD diciendo “ahora ponme aquí para trabajar” para que los siguientes commits se guarden en esa rama y ya no en la main
                
        - **Crear Rama (con switch)**
            - Para crear la rama:
                
                ```bash
                git branch mi-primera-rama # o para crear y dirigirse a la rama
                git switch -c mi-primera-rama # te avisa si ya existe la rama (-c = create)
                ```
                
            - Para cambiar a otra rama:
                
                ```bash
                git switch mi-primera-rama
                ```
                
    - Fusionar Ramas
        - Las bifurcaciones tienen dos destinos
            - Quedar en el olvido
            - Ser fusionados a otra rama
        - Para fusionar lo hecho a otra rama
            
            ```bash
            git checkout main  # cambia a la rama main
            git merge nueva-funcionalidad # fuciona la rama a la rama main
            ```
            
            “merge” es quien fusiona la rama en la que estamos actualmente con la que le indicamos (debemos estar en la rama donde queremos recibir los cambios)
            
        - **“git merge --edit” y “git merge -- no-commit”**
            - git merge --edit
                - Este comando nos permite modificar el mensaje del merge por uno que querramos nosotros
                    - Para describir el merge (un mejor historial)
            - git merge -- no-commit
                - Indica a merge que NO haga el commit automáticamente
                    - Para revisar los archivos fusionados, hacer cambios, agregar, etc. y hacer nosotros manualmente el commit cuando creamos que está listo
                    - Modificar (si es necesario) el resultado del merge
                    
                    <aside>
                    💡
                    
                    No suele ser muy necesario, solo cuando se requiere de mayor control
                    
                    </aside>
                    
    - Eliminar Ramas
        - Es buena práctica borrar ramas para:
            - Mantener el repositorio limpio y en orden
                - Para que no se llene de ramas que no se usen
                - Evitar el ruido o confusiones con los colaboradores
            - Evitar errores
                - Para que no se trabaje con una rama que ya no es útil por confusión o accidente
            - Indicar que la “tarea” ya está terminada
                - Esto hace alusión a un control de actividades
            - Mejorar el rendimiento del repositorio
        
        <aside>
        💡
        
        Al momento de fusionar una rama a otra, la que ya no queremos queda igual que antes de fusionarla, sin embargo, como su trabajo ya fue integrado, ya no tiene propósito
        
        </aside>
        
        - **Cómo borrar una rama**
            - Para borrar una rama se añade el parámetro “delete” o “d”
                
                ```bash
                git branch --d rama-prueba
                ```
                
                Este comando sólo funciona correctamente si la rama fue previamente fusionada
                
            - Para borrar una rama NO fusionada, usamos el parámetro “D” que indica que estamos seguros de borrar esta rama
                
                ```bash
                git branch --D rama-prueba2
                ```
                
    - Más comandos para ramas
        - **git branch**
            - Muestra una lista de todas las ramas locales del repositorio
            - Resultado:
                
                ```bash
                  main
                * nueva-funcionalidad
                ```
                
                El asterisco indica en qué rama estás
                
        - **git branch -a**
            - Muestra todas las ramas, tanto locales como remotas
            - Resultado:
                
                ```bash
                  main
                  mi-rama
                  remotes/origin/main
                  remotes/origin/otra-rama
                ```
                
        - **git rebase**
            - Reescribe el historial de una rama
                - Mueve los commits de una rama replicándolos sobre otra como si estos hubieran sido creados en esa otra rama originalmente
            - Sirve para:
                - Tener un historial más limpio (sin tantos commits de merge)
                - Integrar cambios a otra rama antes de fusionar
                - Para reorganizar commits
            - Diferencia con git merge
                - Mientras merge mantiene un historial con bifurcaciones y commits de la fusión, rebase es un historial limpio sin commits de merge
- **Conflictos**
    - Cuando sucede un conflicto, al arreglarlo manualmente tenemos 3 alternativas
        - Nos quedamos con los cambios de rama 1
        - Nos quedamos con los cambios de rama 2
        - Modificamos los cambios para hacer una mezcla personalizada (fusionamos)
            - El mensaje nos mostrará primero el contenido que ya existía y después el que queremos incorporar
    1. Conflictos al fusionar (git merge)
        - Cuando 2 ramas han editado las mismas líneas de un archivo
        - Solución:
            - git nos marca para escoger con cuál nos quedamos o si mezclamos ambas
        - Para evitarlo:
            - Actualizar nuestra rama frecuentemente, incluso antes de trabajar (para tener todos los últimos cambios)
            - Si estamos en otra rama, traer regularmente los cambios que ya hay en la rama main
            - Trabajar en ramas con objetivos específicos y pequeños
            - Coordinar qué líneas va a trabajarlo quién
    2. Conflictos al rebase (git rebase)
        - Al reescribir el historial de una rama compartida, podemos estar tratando de reescribir el historial de otro y eso genera un conflicto (y puede que el historial que queremos reescribir ya haya cambiado, sea porque ya no existe el archivo o este fue modificado)
        - Solución:
            - git nos dice cuál escogemos o si mezclamos ambos
        - Para evitarlo:
            - Hacer pull con el parámetro rebase regularmente
            - De preferencia no hacer rebase en ramas compartidas
            - Usar rebase -i (interactivo) para revisar los cambios que se aplicarán
    3. Conflictos al hacer pull
        - Cuando estamos en la rama local y hacemos pull sin hacer antes push, git intentará fusionar lo remoto con lo local y habrá un conflicto
        - Solución:
            - Lo mismo que con merge
        - Para evitar:
            - Los mismo que con merge
    4. Conflictos al cambiar de rama
        - Pasa cuando hay cambios no confirmados en los archivos y cambiamos de rama
        - Solución:
            - Hacer un commit antes de cambiar de rama
        - Para evitar:
            - Hacer un commit antes de cambiar de rama o un stash
    5. Conflictos al aplicar un stash
        - Al hacer git stash, se guardan los cambios no confirmados en una “caja temporal” llamada stash
            
            Esos cambios se aplican con:
            
            ```bash
            git stash pop 
            ```
            
            Al igual que con merge y otros conflictos que ya vimos, si se hacen cambios en lo que ya tenía cambios guardados en un stash (hacemos cambios olvidando que hay cambios en la caja pendientes por aplicar con pop) git no sabe cuál mantener, si los de la caja o los que hicimos actualmente
            
        - Solución:
            - Elegir uno o fusionarlos y finalizar el stash con un commit
            
            <aside>
            💡
            
            `stash pop` automáticamente elimina el stash *si no hay conflicto*. Si **hay conflicto**, **no se elimina**, así que puedes recuperarlo con `git stash list`.
            
            </aside>
            
        - Para evitarlo:
            - Revisar lo que hay en el stash con:
                
                ```bash
                git stash show -p
                ```
                
            - Hacer stash pop antes de hacer nuevos cambios
            - Si ya hay cambios confirmados, hacer commit de estos y después hacer un stash si es necesario
            - Usar stash apply en vez de pop, tal que este aplica los cambios pero sin borrar lo que está en el stash
                - Para limpiar el stash si ya no se necesita su contenido:
                    
                    ```bash
                    git stash drop stash@{0} # de uno específico
                    git stash clear # todos los stashes 
                    ```