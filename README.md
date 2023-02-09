# **Introduccion a graphql desde las bases hasta crear apis**
<img style="margin:auto;" width=450 height=160 src="./assets/images/graphql-logo.png"/>

## _**¿Que es GraphQL? 1/135**_
Es un lenguaje de consulta, que permite especificar los campos que queremos.
Desarrollado por Facebook en 2012, fue lanzado en 2015.

### _Funciones principales_
- Eficiencia.
  - Multiples consultas con solo una request.
  - Soporta para datos relacionales.
  - No se da overfetching ni underfetching.
    - overfetching: busqueda excesiva, solo los datos necesarios que se necesitan.
    - underfetching: busqueda de datos insuficientes, si queremos mas información debemos cambiar el backend.
- Sistema de tipos.
  - Describe la forma que se puede enviar o recibir los datos.
  - Contrato entre cliente / servidor.
  - Validación en el lado del servidor.
  - Seguridad adicional.
- Un único endpoint.
  - Sin problemas de endpoints
  - Desarrollo de nuevas funcionalidades sin romper compatibilidad hacia atrás.
  - Versionless API, no se versionara el api.
- Trabaja con cualquier cosa.
  - Bases de datos existentes.
  - Base de código existente.
  - Se puede construir sobre otra API.

## _**GraphQL vs REST 2/135**_
|REST|GraphQL|
|----|-------|
|Una ULR = un recurso|Una URL = Toda la información|
|No podemos elegir lo que vamos a recibir en el JSON|Podemos elegir lo que queremos recibir en el JSON|
|Versionado|No existe versionamiento|
|No autodocumentado|Autodocumentado|
|Almacenamiento en caché|No tiene almacenamiento en cache|

_Ejemplo con REST_

Se tienes que hacer 3 llamados al servidor para obtener todos los datos que necesitamos.
* **Serie**: https:www.api.com/series/1
* **Capitulos**: https:www.api.com/series/1/episodios/1
* **Autor**: https:www.api.com/series/1/autor


_Ejemplo con GraphQL_

Con una sola petición accedemos a todos los valores que necesitamos, sin incurrir en overfetching o underfetching.
```graphql
{
    serie (id: "1") {
        id
        nombre
        author {
            nombre
            apellido
        }
        episodes {
            id
            title
        }
    }
}
```

### Versionado
|**REST**|**GraphQL**|
|--------|-----------|
| - Necesitamos versionar cualquier cambio | - No hay necesidad de versionamiento |
| - Más endpoints | - Añadir campos o tipos sin modificar o romper las consultas existentes |
| - Más problemas al usarlo | - Uso de "deprecated" para asignar un campo como obsoleto |
| - Más mantenimiento mas costo ||
| - Duplicidad del codigo ||

### Documentación
|**REST**|**GraphQL**|
|--------|-----------|
| - Documentación no autodocumentada cuando se construye | - Autodocumentado aprovechando su naturaleza fuertemente tipada |
| - Habra que usar recursos externos: Postman, Swagger...etc. | - Funciones de autocompletado y documentación se autogeneran |

### Almacenamiento en cache
|**REST**|**GraphQL**|
|--------|-----------|
| - Implementado mediando HTTP | - No tiene un sistema de almacenamiento en caché |
| - El cliente puede usar el almacenamiento en caché para evitar volver a buscar recursos | - El cliente tiene la responsabilidad de encargarse del almacenamiento en caché |