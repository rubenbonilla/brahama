# Rutas a ficheros/directorios

Son direcciones del sistema de fichero para crear, leer, modificar y/o eliminar ficheros, o almacenar ficheros de trazas o certificados.

## Reglas
    - Se definira la ruta absoluta a la raiz del proyecto en un unico lugar de la aplicación, accesible desde cualquier parte de la misma.
    - Todas las rutas se compondran con la ruta raiz del proyecto.
    - Todas las rutas que queden fuera del directorio raiz, seran definidas como rutas absolutas.

# Dependencias

Las dependencias, son todas esas funcionalidades que requiere una implementación y que estan definidas externamente.

## Reglas
    - Las dependencias se definiran e inyectaran a nivel de Aplicación (FrontController), garantizando que un posible futuro reemplazo se realice desde un solo lugar.


# Variables


## Reglas
    - Eliminar variables que no sean utilizadas.
    - Deben seguir la notación, minusculas y palabaras separadas por _(Notación C)

## A tener en cuenta
    - En python las variables de tipo lista o diccionario son pasadas por referencia.

# Trazas

Las trazas nos proveen una forma de comprobar la atomicidad de una operación completa. En caso de errores nos permiten tener constancia, poder corregirlos y tener justificaciones.
Permiten crear un sistema de alertas. Procesar la información para analisis y control del sistema y servicio.

## Reglas
    - Es importante registrar el mayor numero de trazas posibles, dentro de la coherencia.
    - Es importante indicar un nivel de traza adecuado.

## Implementación



Todas las trazas tendran:
    - Fecha y hora en microsegundos (DATETIME).
    - Nivel de traza (LEVEL). [DEBUG|INFO|NOTICE|WARNING|ERROR|CRITICAL]
    - Punto de registro (FILE:LINE): se indicara el fichero y la linea de codigo que lanza el registro de logs.
    - Responsable (NAMESPACE): Espacio de nombres de la modulo.clase.metodo o modulo.funcion
    - Identificador de operación (PARAMS[UUID]): permite unir con el resto de trazas de la operación, en nuestro caso un uuid versión 1.
    - Tipo (PARAMS[TYPE]): Tipo de traza, para indicar si es una traza sobre soap, http...

Las trazas tienen el siguiente formato:
    DATETIME - LEVEL - PARAMS - ARGS

## Niveles de traza

### Debug

Son trazas para depurar codigo.

#### Ambito
    - Desarrollo: para agilizar el proceso de implementación y la trazabilidad del codigo.
    - Pruebas: para comprobar el funcionamiento del codigo en un entorno real y solución de bugs.

#### Usos
    - Durante la implementación de nuevas funcionalidades.


### Info

Son trazas para registrar acciones e información sensible en caso de error, pero no generan alertas.

#### Ambito
    - Pruebas: para comprobar el funcionamiento del codigo en un entorno real.
    - Producción: para complementar la información en caso de error.

#### Usos
    - Registrar la información que se envia a un servidor antes de realizar la petición, para registrar las posibles perdidas de información.
    - Registrar la información que se envia a un cliente antes de realizar la respuesta, para registras las posibles perdidas de información.


### Notice

Sirven para registrar acciones correctas pero que quedan obsoletas en futuras versiones, obligan a refactorizar el codigo.

#### Ambito
    - Desarrollo: identificar partes del codigo obsoletas.
    - Pruebas: control de migraciones entre versiones.

#### Usos
    - Registrar funciones que posteriormente se eliminaran.
    - Partes de codigo que estan marcadas para refactorizar.
    - Comprobaciones que desapareceran en futuras implementaciones al realizar el versionado del codigo.


### Warning

Sirven para registrar acciones incorrectas o inesperadas que permiten continuar con la ejecución pero deben revisarse.

#### Ambito
    - Pruebas: comprobaciones de despliegue de nuevas funcionalidades y la correcta implementación de la misma.
    - Producción: mantenimiento de diferentes versiones del codigo

#### Usos
    - Util en la migración de versiones.
    - Versionado con retrocompatibilidad y registro de futuras incompatibilidades.
    - Acciones que pueden comprometer la seguridad.
    - Acciones que pueden ser fraudulentas.


### Error

Sirven para registrar acciones incorrectas o inesperadas que no permiten continuar con la ejecución del codigo, generando alertas.

#### Ambito
    - Desarrollo: sirven para mejorar la recuperación de errores.
    - Pruebas: comprobación de una buena implementación.
    - Producción: documentación de errores, tazabilidad, justificación.

#### Usos
    - Toda acción que no se comporta de forma esperada.
    - Inconsistencias de información.


### Critical

Sirven para registrar acciones incorrectas o inesperadas que no permiten continuar con la ejecución y son necesarias para el proposito del mismo.

#### Ambito
    - Desarrollo: sirven para mejorar la responsabilidad de dependencias.
    - Pruebas: comprobación de buena operabilidad del sistema.
    - Producción: generación de alertas para recuperación de caida.

#### Usos
    - Servicios con indisponibilidad recurrente.
    - Errores irrecuperables en la aplicación.
    - Perdida de información.
    - Fallos de seguridad.

