# Trello

### 💻Proyecto: 
https://trello.com/es

En este proyecto se crea contenido en la herramienta Trello utilizando sus API REST, aplicando la técnica CRUD para validar las operaciones básicas de la aplicación web.

### 🔍Tipo de testing:
* API testing

### ⚙ Herramientas utilizadas:
* Postman

### ✅ Precondición

El usuario debe tener una cuenta registrada en Trello y debe tener creado un tablero.

### ⚙️ Set up

Workspace: TRELLO

Ambiente: TrelloAPI

Variables de ambiente:
* Key
* Token
* baseURL
* idBoard

### 📁 Contenido:
- Coleccion: Tablero
  - Carpeta: Workflow

    Test: Validar codigo de estado 200: se ejecuta al final de cada solicitud que se encuentra dentro de esta carpeta. 

    - Request:
      - POST | Crear nueva lista:

        Query Params:
        - Key: name. Valor: se ingresa el valor mediante la variable de coleccion {{nameLista}}
        
        Test:
        - Validar lista creada con el nombre correcto
        - Validar esquema JSON
        - Crear variable de coleccion {{idLista}}
        
      - POST | Crear nueva tarjeta

        Query Params:
        - Key: idList. Valor: se obtiene de la variable de coleccion {{idlista}} creado por el request anterior
        - Key: name. Valor: variable de coleccion {{nameTarjeta}}. Se obtiene el valor de forma aleatoria en el momento de la ejecucion a traves de la variable dinamica $randomFullName
            
        Test:
        - Validar tarjeta en la lista correcta
        - Validar tarjeta creada con el nombre correcto
        - Crear la variable {{idTarjeta}}
          
      - POST | Crear nuevo Checklist

        Query Params:
        - Key: name. Valor: se ingresa el valor mediante la variable de coleccion {{nameChecklist}}
     
        Path Variables:
        -   Key: id. Valor: se obtiene de la variable de coleccion {{idTarjeta}} creado por el request anterior
        
        Test:
        - Validar que la respuesta sea un objeto
        - Validar Checklist creado con el nombre correcto
        - Validar Checklist creado en la tarjeta correcta
        - Crear la variable {{idChecklist}}

    
      - POST | Crear nuevo Checkitem
        
        Query Params:
        - Key: name. Valor: se puede ingresar el valor de dos formas posibles:
        
            - mediante la variable de coleccion {{nameCheckitem}}
            - agregando datos de prueba con un archivo .CSV el cual se importa en Collection Runner
 
        Path Variables:
        -   Key: id. Valor: se obtiene de la variable de coleccion {{idChecklist}} creado por el request anterior
       
        Test:
        - Validar checkitem creado con el nombre correcto
        - Validar checkitem creado en el checklist correcto
        - Crear la variable {{idCheckitem}}
      
      - PUT | Modificar state en CheckItem
        
        Query Params:
        - Key: state. Valor: complete
          
        Path Variables:
        -   Key: id. Valor: se obtiene de la variable de coleccion {{idTarjeta}}
        -   Key: idCheckItem. Valor: se obtiene de la variable de coleccion {{idCheckitem}} creado por el request anterior.
       
      - GET | Validar state de CheckItem
        
         Path Variables:
        -   Key: id. Valor: se obtiene de la variable de coleccion {{idChecklist}}
        
        Test:
        - Validar checkitem con state "complete"
          
      - GET | Visualizar Checkitems
        
        Path Variables:
        -   Key: id. Valor: se obtiene de la variable de coleccion {{idChecklist}}
          
        Test:
        - Visualizar contenido en postman
          
        
      - DEL | Eliminar tarjeta
      - PUT | Archivar lista
      - GET | Validar lista archivada
