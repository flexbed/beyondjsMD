# Notas

> Tener presente que hay mezcla de idiomas (partes en inglés y partes en castellano).  

Al crear una nueva app (_Aplicación en blanco_) en un directorio vacío el dashboard crea los siguientes archivos en el PWD:
- beyond.json
- :open_file_folder: __title__ (reemplazando los espacios por guiones bajos)
- - :page_facing_up: application.json
- - :open_file_folder: __template__
- - - :memo: custom-properties.scss
- - - :memo: styles.scss
- - - :page_facing_up: template.json

Es decir, el setup de la aplicación (los JSONs) y los archivos de estilos globales.  

---
> En la vista del listado de módulos de la aplicación, seleccionando cualquier cosa que no sea "application", muestra el dialogo para crear el primer módulo (incluso selecctionando "all")   

Con la creación de un nuevo mósulo (_Módulo en blanco_ con textos y estilos) el dashboard se encarga de la creación de la siguiente estructura:
- :open_file_folder: __nombre__ (reemplazando los espacios por guiones bajos)
- - :page_facing_up: module.json
- - :page_facing_up: tsconfig.json
- - :open_file_folder: __scss__
- - - :memo: styles.scss
- - :open_file_folder: __ts__
- - - :scroll: page.ts
- - - :page_with_curl: view.tsx
- - :open_file_folder: __txt__
- - - :page_facing_up: texts.json

---
