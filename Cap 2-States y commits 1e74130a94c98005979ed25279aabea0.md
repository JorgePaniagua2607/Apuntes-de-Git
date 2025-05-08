# States y commits

Estado: Listo

- **Estados de Git**
    
    Modified
    
    - El archivo tiene cambios que aún no han sido marcados como confirmados
    - Está “untraked” cuando solo se creó el archivo
    - Está “Modified” cuando se crea un segundo archivo (está con cambios no preparados)
    
    Staged
    
    - El archivo está marcado como preparado para ser confirmado
    - Está “staged” depués de un git add (listo para el commit)
    
    Commited
    
    - Se graba el archivo en el repositorio local (commit)
    - Está “committed” cuando ya se guardó en el historial después de hacer un git commit
    
    Resumen visual
    
    ```bash
    WORKING DIR (modificado)
       ↓ git add
    STAGING AREA (preparado)
       ↓ git commit
    REPO LOCAL (confirmado)
    ```
    
- **Commit**
    - Registros de cambios que se hicieron en los repositorios (estado en el momento en el que se hizo)
    - Hacer un commit
        - Para guardar en el área de stating:
            
            ```bash
            git commit
            ```
            
            Es para crear un commit una vez exista algo qué cambiar (hacer previamente un git add .)
            
            Si quiero darle un mensaje a este commit procedo así
            
            ```bash
            git commit -m “mensaje”
            
            // puedo poner varios mensajes más
            
            git commit -m “mensaje1” -m “mensaje2”
            ```
            
- **HEAD**
    - Es el puntero que nos dice en qué punto del historial estás trabajando
- **Ejercicio**
    
    Crear un repositorio local, agregar archivos, hacer commits, ver el estado, y observar el comportamiento de HEAD y el historial de commits
    
    1. Crear la carpeta de trabajo y entrar en ella 
        
        ```bash
        mkdir ejercicio1
        cd ejercicio1
        ```
        
    2. Iniciar el repositorio como git 
        
        ```bash
        git init
        ```
        
    3. Crear un archivo y ver el estado 
        
        ```bash
        echo "Este es un ejercicio con chatGPT" > ejercicio1.txt
        git status
        ```
        
    4. Agregar el archivo al staging area (nuestra bandeja de preparación, entre los archivos modificados y el historial)
        
        ```bash
        git add ejercicio1.txt
        git status
        ```
        
    5. Hacer un commit
        
        ```bash
        git commit -m "Primer commit: agrego ejercicio1.txt"
        git status 
        ```
        
    6. Ver en qué commit estoy
        
        ```bash
        git show HEAD
        ```
        
    7. Crear otro archivo
        
        ```bash
        echo "Segundo archivo de prueba" > ejercicio1-2.txt
        git add ejercicio1-2.txt
        git commit -m "Segundo commit: otrito más"
        ```
        
    8. Ver el historial de commits
        
        ```bash
        git log
        ```