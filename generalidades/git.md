# El commit perfecto
1. Agregar los cambios correctos
    - Hacer que lo que se agrega tengan sentido
    - Tengan un solo proposito o tema
    - El que un commit tenga muchos temas, hace que sea más dificil entenderlo tanto para el equipo como para si mismo
    - El area de stagign es muy util, permite seleccionar archivos especificos o partes de eso archivos
    ## Ejemplo
    ```sh
    git add css/general.css //Agrega un archivo al staging
    git diff index.html // Muestra los cambios que tiene el archivo
    git add -p index.html // Permite agregar partes del archivo al staging
    ```
2. Crear un buen mensaje de commit
    - Subject: Resumen conciso de que se hizo < 80 caracteres
    - Body: Más detalles que lo explican
        - Qué es diferente ahora de lo que estaba?
        - Por qué se hizo ese cambio
        - Hay algo con lo que se deberia tener cueidado o algo particularmente destacable
    - Si es muy complicado colocar un subject es posible que sea porque se abordan muchos temas en el commit 
# Estrategias de branching
El tipo de estrategia depende de las necesidades y los requerimientos de el equipo y el proyecto
## Integrando cambios y estrurando entregas
1. Desarrollo principal (Siempre esta integrado)
    - Pocas ramas
    - Commits relativamente cortos
    - Debe tener Alta calidad pruevas y QA estandas

2. State, Release, and Feature Branches
    - Diferentes tipos de ramas, producción, desarrollo, testing, documentación etc
    - Realizar diferentes tipos de trabajos
    Estan conformados por:
    - Long-runnig Branches: 
        + Existen a travez de todo el ciclo de vida del proyectos (main, develop, etc)
        + Las ramas reprensentan el estado de desarrollo del ciclo de vida
        + No se hace commits directos, para garantizar la calidad
    - Short-lived Branches:
        + Para crear una nueva feature, bug fixes, refatorings, experimentar
        + Deben ser eliminadas despues de la integración
    ## Ejemplos de Strategies Branching
        1. GitHub Flow
            Tiene un flujo extremadamente limpio y simple, solo existe un rama de largo recorrido
        2. GitFlow
            Tiene más estructura y más reglas   
    La mejor modelo de ramificación
    - Depende del proyecto, el ciclo de liberación, y el equipo
    - Tomar como base alguno de los modelos existentes
    - y crear un modelo propio
3. Pull requests
    - Comunicar sobre la revición de codigo, cuando los cambios son más complejos o muy importantes, es util tener una segunda revisión de codigo por parte de otra persona y obtener retroalimentación
    - Contribuir codigo a otros repositorios
4. Merge conflictos
- Cuando ocurren?
    Cuando se integran commits de diferentes fuentes, no solo ocurren cuando se hace merge sino tambien cuando se hace rebase, cherry-pick, pull o se aplica un stash
- Donde estan?
- Como resolverlos?

