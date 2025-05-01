### Escuela Colombiana de Ingeniería
### Arquitecturas de Software - ARSW

---

### Integrantes: Joan S. Acevedo Aguilar - Cesar A. Borray Suarez

---

## Escalamiento en Azure con Maquinas Virtuales, Sacale Sets y Service Plans

### Dependencias
* Cree una cuenta gratuita dentro de Azure. Para hacerlo puede guiarse de esta [documentación](https://azure.microsoft.com/es-es/free/students/). Al hacerlo usted contará con $100 USD para gastar durante 12 meses.
Antes de iniciar con el laboratorio, revise la siguiente documentación sobre las [Azure Functions](https://www.c-sharpcorner.com/article/an-overview-of-azure-functions/)

### Parte 0 - Entendiendo el escenario de calidad

Adjunto a este laboratorio usted podrá encontrar una aplicación totalmente desarrollada que tiene como objetivo calcular el enésimo valor de la secuencia de Fibonnaci.

**Escalabilidad**
Cuando un conjunto de usuarios consulta un enésimo número (superior a 1000000) de la secuencia de Fibonacci de forma concurrente y el sistema se encuentra bajo condiciones normales de operación, todas las peticiones deben ser respondidas y el consumo de CPU del sistema no puede superar el 70%.

### Escalabilidad Serverless (Functions)

1. Cree una Function App tal cual como se muestra en las  imagenes.

![](images/part3/part3-function-config.png)

![](images/part3/part3-function-configii.png)

Accedemos al potal de azure y creamos una Function App

![Image](https://github.com/user-attachments/assets/6b552f97-0314-4eef-a68c-2e582eb0432d)

Escogemos nuestro tipo de plan para la Function App 

![Image](https://github.com/user-attachments/assets/84e01ef8-a603-4714-ae18-691ad315ee34)

Aca ponemos las caracteristicas que se nos indicaba para crear la function app

![Image](https://github.com/user-attachments/assets/98078638-d4ec-44d7-9590-ad0a99354def)

![Image](https://github.com/user-attachments/assets/f1c606b7-5717-4c33-b404-3cb1d5e8c1a6)

![Image](https://github.com/user-attachments/assets/cfdd6e56-d1e3-457d-a20d-ddb5bc32bdbd)

Y finalmente tenemos nuestra function app creada

![Image](https://github.com/user-attachments/assets/308daa7f-7545-402c-b9f9-c54dbe4355d3)

2. Instale la extensión de **Azure Functions** para Visual Studio Code.

![](images/part3/part3-install-extension.png)

Buscamos en extensiones de Visual Studio Code y descargamos la exetension de Azure Functions

![Image](https://github.com/user-attachments/assets/b8e10c7f-e39d-46bf-a5b8-cca630b0b950)

3. Despliegue la Function de Fibonacci a Azure usando Visual Studio Code. La primera vez que lo haga se le va a pedir autenticarse, siga las instrucciones.

![](images/part3/part3-deploy-function-1.png)

![](images/part3/part3-deploy-function-2.png)

Teniendo la extencion vamos a desplegar la funcion del fibonacci 

![Image](https://github.com/user-attachments/assets/c116328e-23ba-4e73-9c6f-c7ad99d35310)

Seleccionamos la function App que creamos

![Image](https://github.com/user-attachments/assets/c49a8441-0a6c-4bde-9978-b32141bd1001)

Y finalmente verificamos que si se haya hecho el despliegue de forma correcta

![Image](https://github.com/user-attachments/assets/89f0a061-f913-4cae-a02f-12d19a3b3b1a)

4. Dirijase al portal de Azure y pruebe la function.

![](images/part3/part3-test-function.png)

Abrimos la funcion desplegada de Fibonacci dentro del portal y hacemos la prueba/ejecucion con su respectivo body de ejemplo y verificamos que nos devuelva el resultado

![Image](https://github.com/user-attachments/assets/a60f5fdf-6fa1-4f98-9c29-0fe7a0353b2d)

5. Modifique la coleción de POSTMAN con NEWMAN de tal forma que pueda enviar 10 peticiones concurrentes. Verifique los resultados y presente un informe.

Para esto dentro de postman hacemos una peticion a nuestra funcion desplegada en azure atraves de la URL que se nos da, guardamos la query en una coleccion y la exportamos

![Image](https://github.com/user-attachments/assets/87a6f303-8f5c-48ee-95df-daaf31e4caa9)

Despues usando newman vamos a realizar las 10 peticiones concurrentes 

![Image](https://github.com/user-attachments/assets/38227674-de46-4bfa-8f24-bf7a19d42236)

Y finalmente tenemos los resultados

![Image](https://github.com/user-attachments/assets/e3a59585-e03b-446e-8d7a-01b28c7fae3b)

6. Cree una nueva Function que resuleva el problema de Fibonacci pero esta vez utilice un enfoque recursivo con memoization. Pruebe la función varias veces, después no haga nada por al menos 5 minutos. Pruebe la función de nuevo con los valores anteriores. ¿Cuál es el comportamiento?.

Para esta nueva funcion creamos una nueva carpeta FibonacciMemo y en esta creamos nuestro index.js y implementamos la logiaca para resolver fibonacci de forma recursiva y con memorizacion

![Image](https://github.com/user-attachments/assets/b0f23d6e-84e4-49b5-9bfb-4f8582ef2943)

Hacemos el despliegue nuevamente y verificamos en el portal que tenemos la nueva funcion FibonacciMemo

![Image](https://github.com/user-attachments/assets/a53ce72c-f8ff-4973-bce9-a5412052c80f)

Y probamos que funcione con 2 valores no tan grandes 

![Image](https://github.com/user-attachments/assets/78620318-d9cc-4456-a140-98f8741286ad)

![Image](https://github.com/user-attachments/assets/40f125c9-bd1a-458b-8e9d-616206bfc0ae) 

**Preguntas**

* ¿Qué es un Azure Function?

  Una **Azure Function** es un servicio de computación sin servidor (serverless) de Microsoft Azure que permite ejecutar pequeñas porciones de código (funciones) en la nube sin necesidad de aprovisionar o gestionar infraestructura.

* ¿Qué es serverless?

  **Serverless**, o "computación sin servidor", es un modelo de ejecución en la nube donde el proveedor (como Azure, AWS, etc.) se encarga de la administración completa de la infraestructura: escalado, disponibilidad, mantenimiento y aprovisionamiento.

* ¿Qué es el runtime y que implica seleccionarlo al momento de crear el Function App?

  El **runtime** en Azure Functions es el entorno que ejecuta el código de las funciones. Al momento de crear un Function App, se debe seleccionar una versión específica del runtime (por ejemplo, v4), lo cual define la compatibilidad con ciertas versiones de lenguajes, bibliotecas, bindings y configuraciones. Elegir un runtime implica:

  * Compatibilidad con ciertas versiones del SDK o frameworks (Node.js, .NET, Python, etc.).

  * Soporte para determinadas extensiones y bundles.

  * Comportamiento del host (host.json) y estructura del proyecto.

  Seleccionar un runtime incorrecto puede ocasionar errores de compatibilidad o despliegue, como dependencias no soportadas.

* ¿Por qué es necesario crear un Storage Account de la mano de un Function App?

  Azure Functions requiere un **Azure Storage Account** obligatorio para almacenar:

  * Archivos de configuración y metadatos de la Function App.

  * Logs y archivos generados por ejecuciones.

  * Datos temporales necesarios por el runtime para el manejo del estado, como los de las funciones con bindings de colas, blobs o timers.

  * El runtime se apoya en el Storage incluso si la función no usa datos persistentes explícitamente.

  Sin una cuenta de almacenamiento asociada, el Function App no puede ejecutarse ni gestionarse correctamente.

* ¿Cuáles son los tipos de planes para un Function App?, ¿En qué se diferencias?, mencione ventajas y desventajas de cada uno de ellos.

  Existen tres tipos principales de planes en Azure Functions:

  1. **Consumption Plan (Plan de consumo)**
  * Escalado automático según demanda (de 0 a N instancias).
  * Solo se cobra por el tiempo de ejecución y recursos usados. 
  * Ideal para cargas eventuales o impredecibles.

    Ventajas:
    * Costos bajos para cargas intermitentes. 
    * No requiere gestión de infraestructura. 
    * Autoescalado inmediato.
        
    Desventajas:
    * Tiempo de arranque inicial (cold start). 
    * Limitaciones en tiempo máximo de ejecución (5 minutos por defecto). 
    * No se puede ejecutar código persistente o de larga duración.
        
  2. **Premium Plan**
  * Escalado automático pero con instancias precalentadas (no hay cold start). 
  * Soporte para redes virtuales (VNET), ejecución ilimitada y mayor capacidad.
      
    Ventajas:
    * Rendimiento constante sin cold start. 
    * Acceso a VNETs privadas. 
    * Escalado de forma más predecible y rápida.

    Desventajas:
    * Más costoso que el Consumption Plan. 
    * Requiere una configuración más avanzada.
    
  3. **App Service Plan**
  * Se usa infraestructura fija, como en una Web App tradicional. 
  * No escala automáticamente por ejecución, pero sí manualmente o por CPU/uso.

    Ventajas:
    * Puedes correr múltiples apps (Web, API, Functions) en el mismo plan. 
    * No tiene restricciones de ejecución o duración.

    Desventajas:
    * Pago fijo independientemente del uso. 
    * No es óptimo para cargas eventuales o impredecibles.

* ¿Por qué la memorization falla o no funciona de forma correcta?

  La memorización es una técnica de optimización que almacena los resultados de funciones costosas para evitar cálculos repetidos. Sin embargo, su efectividad puede verse limitada en entornos como Azure Functions por varias razones:

  1. **Pérdida del estado entre ejecuciones**:
  En el modelo serverless, cada ejecución de la función puede realizarse en una instancia diferente. Esto significa que cualquier estructura de datos almacenada en memoria (como el diccionario memo) se pierde entre invocaciones. 

  2. **Tiempo de vida corto del entorno de ejecución**:
  Las Azure Functions usan instancias efímeras que pueden ser terminadas por el sistema cuando no están en uso. Esto rompe la persistencia de la memoización y hace que los beneficios solo existan dentro de la misma ejecución o durante un tiempo muy limitado (el llamado "warm instance").
  
  3. **Uso intensivo de la pila**:
  En casos como el cálculo de Fibonacci con recursión profunda, incluso con memoization, el número de llamadas puede exceder la capacidad de la pila del entorno, resultando en errores como StackOverflow o tiempos de ejecución que superan los límites de Azure.

* ¿Cómo funciona el sistema de facturación de las Function App?

  El sistema de facturación en Azure Function Apps depende principalmente del plan de hospedaje que se seleccione. Los dos modelos más comunes son:

  1. Consumption Plan (Plan de Consumo)
     Facturación basada en:
     * Número de ejecuciones. 
     * Duración de cada ejecución (en GB-segundos). 
     * Memoria asignada automáticamente por Azure.
  
  2. Premium Plan
     Facturación por: 
     * Núcleos (vCPU) y memoria reservada. 
     * Tiempo en que las instancias están activas, incluso si no hay ejecuciones.

* Informe

### Informe de Pruebas de Carga Concurrente con Newman - Azure Function "Fibonacci"
#### Objetivo
El objetivo de esta prueba fue ejecutar 10 solicitudes concurrentes contra la Azure Function Fibonacci, utilizando la herramienta Newman (CLI para Postman), con el fin de analizar el comportamiento de la función bajo carga moderada y medir la latencia promedio, así como posibles fallos en el procesamiento.

#### Configuración de la Prueba
* Herramienta utilizada: Newman v6.2.1

* Función probada: https://functionprojectfibonacci.azurewebsites.net/api/Fibonacci

* Tipo de solicitud: POST

* Parámetro enviado en el body: nth = 1000000

* Número de iteraciones: 10

* Nivel de concurrencia: Controlado secuencialmente (una iteración tras otra, sin paralelismo explícito)

#### Resultados Obtenidos

| Iteración | Código HTTP | Tamaño respuesta | Tiempo de respuesta |
|-----------|-------------|------------------|----------------------|
| 1         | 200 OK      | 209.23 kB        | 20.3 segundos        |
| 2         | 200 OK      | 209.23 kB        | 13.3 segundos        |
| 3         | 200 OK      | 209.23 kB        | 13.6 segundos        |
| 4         | 200 OK      | 209.23 kB        | 15.0 segundos        |
| 5         | 200 OK      | 209.23 kB        | 16.6 segundos        |
| 6         | 200 OK      | 209.23 kB        | 14.7 segundos        |
| 7         | 200 OK      | 209.23 kB        | 13.6 segundos        |
| 8         | 200 OK      | 209.23 kB        | 13.4 segundos        |
| 9         | 200 OK      | 209.23 kB        | 13.8 segundos        |
| 10        | 200 OK      | 209.23 kB        | 13.1 segundos        |

#### Análisis
1. **Desempeño estable:** La función respondió correctamente a todas las solicitudes, sin errores ni caídas, lo cual es una buena señal de estabilidad funcional.

2. **Tiempo de respuesta elevado:** Un tiempo promedio de 14.7 segundos es considerablemente alto para una función computacional. Esto se puede atribuir a:

  * El cálculo del enésimo término de Fibonacci con números extremadamente grandes 

  * Uso de BigInt o bibliotecas externas como big-integer, que agregan sobrecarga de procesamiento.
  
  * Posible impacto de “cold starts” si alguna ejecución se realizó en una instancia recién activada.

3. **Falta de caching/memoization entre ejecuciones:** Dado que cada ejecución se maneja de forma aislada (stateless), no se aprovecharon los beneficios de la memoización entre llamadas, lo que redunda en tiempos similares para cada iteración.

#### Recomendaciones
1. **Implementar caching persistente** (Redis, Azure Cache, Blob Storage) si los valores de Fibonacci consultados son repetitivos y no requieren cálculo en tiempo real.

2. **Reducir la complejidad del cálculo** o aplicar técnicas de optimización (iterativo + reducción de precisión si es aceptable).

3. **Evaluar el uso de un plan Premium** si se requiere reducir el tiempo de cold start o tener menor latencia.

4. **Aumentar concurrencia real** para evaluar límites de escalabilidad real de la Function.