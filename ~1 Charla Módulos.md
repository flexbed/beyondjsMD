 ### Aclaraciones respecto de los módulos
Beyond está compuesto por módulos y los módulos tienen _bundles_ además de archivos estáticos.
Esto genera una confusión respecto de la terminología utilizada, porque es necesario diferenciar los módulos de Beyond que van a ser importados/exportados (internamente) en los bundles de los bundles en sí (que a su vez van a ser importados/exportados por otros bundles).

> **NOTA:** A los módulos de BeyondJS, los voy a llamar _BeyondModules_.

 ### Creación de módulo ANIMAL
Primero creamos el `module.json` dentro del directorio en el que vamos a programa el modulo y en el mismo, definimos
```json
{
  "developer": "docs",
  "name": "animals",
  "bundle": "ts",
  "files": "*"
}
```
Utlizamos `bundle: ts` ya que nuestro _BeyondModule_ sólo va a contener código TypeScript.  
Ahora vamos a crear los archivos _ts_  
**animal.ts**

```ecmascript6
export abstract class Animal {
    name: string

    constructor(name: string) {
        this.name = name;
    }

    abstract welcome(): string;
}
```
**dog.ts**
```ecmascript6
import {Animal} from "./animal";

export /*bundle*/
class Dog extends Animal {
    legs = 4;

    welcome(): string {
        return `Guau ${this.name}`;
    }
}
```
Si bien tanto en **animal.ts** como en **dog.ts** estoy haciendo `export`, la diferencia es que la clase Animal, va a ser importada por otros módulos **dentro del mismo _BeyondModule_ ("bundle") en cambio la clase Dog, quiero que se exponga para ser consumida por otros _BeyondModule_(s), entonces:
En animal.ts, hago simplemente  
`export`  
(es "interna"), pero en dog.ts (quiero exponerla hacia "afuera"), voy a hacer  
`export /*bundle*/`  
donde ese "comentario" `/*bundle*/` le va a indicar a los procesadores de BeyondJS que ese export se debe exponer en el _BeyondModule_.  

 ### Código Compilado
Nuestro directorio quedó de la siguiente forma:
```bash
model
  ╠ animal.ts
  ╠ dog.ts
  ╚ module.json 
```
El código compilado de nuestro _BeyondModule_ va a quedar "visible" en nuestro caso en:  
`localhost:8080/model/ts.js`  
Va a ser un código sincrónico CommonJS empaquetado por BeyondJS.

 ### Carga del _BeyondModule_ desde el browser
Para importar mi nuevo modulo desde una página, BeyondJS propone un modelo donde no se utiliza el path "físico" de los archivos, en cambio, se utiliza:      
`import {Dog} from "@dependencies/@docs/animals/ts"`  
De esta forma, el código puede ubicarse donde el desarrollador prefiera, ya que la definición de la dependencia está dada por el _developer_ y el _name_ y es resuelto por BeyondJS. La estructura de la ruta de importación es:
- **@dependencies** Para indicar que es una importación BeyondJS.
- **@\<developer\>** Definido en el `module.json`
- **\<name\>** Definido en `module.json`
- **\<bundle\>** Definido en `module.json`
 
> **DUDA** Los valores de _developer_ son únicos? 

<u>**@TODO:**</u> El dashboard de BeyondJS debería generar los archivos de declaraciones necesarias para que el IDE reconozca el import (en el directorio @dependencies local).  

 ### Visión general sobre los módulos
El objetivo es que los _BeyondModules_ estén "al alcance" de los desarrolladores al momento de crear sus proyectos, permitiendo de esa forma, cada uno pueda liberar sus propios _BeyondModules_ para que sean recogidos por la comunidad para reutilizarlos, refinarlos, perfeccionarlos, etc. y a su vez volver a compartirlos con la comunidad. Apuntando a un modelo abierto, sobre todo en lo que respecta a las interfaces gráficas.


