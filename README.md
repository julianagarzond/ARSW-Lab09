### Escuela Colombiana de Ingeniería
### Arquitecturas de Software - ARSW

## Escalamiento en Azure con Maquinas Virtuales, Sacale Sets y Service Plans

### Dependencias
* Cree una cuenta gratuita dentro de Azure. Para hacerlo puede guiarse de esta [documentación](https://azure.microsoft.com/en-us/free/search/?&ef_id=Cj0KCQiA2ITuBRDkARIsAMK9Q7MuvuTqIfK15LWfaM7bLL_QsBbC5XhJJezUbcfx-qAnfPjH568chTMaAkAsEALw_wcB:G:s&OCID=AID2000068_SEM_alOkB9ZE&MarinID=alOkB9ZE_368060503322_%2Bazure_b_c__79187603991_kwd-23159435208&lnkd=Google_Azure_Brand&dclid=CjgKEAiA2ITuBRDchty8lqPlzS4SJAC3x4k1mAxU7XNhWdOSESfffUnMNjLWcAIuikQnj3C4U8xRG_D_BwE). Al hacerlo usted contará con $200 USD para gastar durante 1 mes.

### Parte 0 - Entendiendo el escenario de calidad

Adjunto a este laboratorio usted podrá encontrar una aplicación totalmente desarrollada que tiene como objetivo calcular el enésimo valor de la secuencia de Fibonnaci.

**Escalabilidad**
Cuando un conjunto de usuarios consulta un enésimo número (superior a 1000000) de la secuencia de Fibonacci de forma concurrente y el sistema se encuentra bajo condiciones normales de operación, todas las peticiones deben ser respondidas y el consumo de CPU del sistema no puede superar el 70%.

### Escalabilidad Serverless (Functions)

1. Cree una Function App tal cual como se muestra en las  imagenes.

![](images/part3/part3-function-config.png)

![](images/part3/part3-function-configii.png)

2. Instale la extensión de **Azure Functions** para Visual Studio Code.

![](images/part3/part3-install-extension.png)

3. Despliegue la Function de Fibonacci a Azure usando Visual Studio Code. La primera vez que lo haga se le va a pedir autenticarse, siga las instrucciones.

![](images/part3/part3-deploy-function-1.png)

![](images/part3/part3-deploy-function-2.png)

4. Dirijase al portal de Azure y pruebe la function.

![](images/part3/part3-test-function.png)

5. Modifique la coleción de POSTMAN con NEWMAN de tal forma que pueda enviar 10 peticiones concurrentes. Verifique los resultados y presente un informe.

6. Cree una nueva Function que resuleva el problema de Fibonacci pero esta vez utilice un enfoque recursivo con memoization. Pruebe la función varias veces, después no haga nada por al menos 5 minutos. Pruebe la función de nuevo con los valores anteriores. ¿Cuál es el comportamiento?.

**Preguntas**

* ¿Qué es un Azure Function?
Se utiliza para ejecutar pequeños fragmentos de código en la nube,utiliza una multitud de nuevos triggers para poder ejecutarlo. Los tipos de triggers que se utilizan son Cosmos DB, Event Hub y WebHooks.

Axure Functios hace que el desarrollo sea más productivo, se puede codificar en diferentes lenguajes de programación,como C#, F#, Node,js, Java o PHP.

* ¿Qué es serverless?
Se refiere al modelo de computación que permita ejecutar durante un tiempo determinado de funciones sin necesidad de hacerse cargo de la infraestructura subyacente que se provisiona para dar el servicio, se encarga de ofrecer recursos de forma transparente, se escala de manera automática ,define una serie de restricciones referentes al procesamiento y un modelo pago por el consumo de los recursos.

* ¿Qué es el runtime y que implica seleccionarlo al momento de crear el Function App?
  - El runtime es una forma que ofrece Azure Functions para mayor simplicidad y flexibilidad del modelo de programación de Azure Functions en las instalaciones, este se implementa de manera local para proporcionar un servicio que sea muy similar al de la nube.

* ¿Por qué es necesario crear un Storage Account de la mano de un Function App?
  - Crear un storage account es necesario para almacenar todos los objetos de datos como blobs, archivos,colas,tablas,discos entr otros, esta proporciona un espacio de nombres único para los datos de Azure Storage, los cuales se pueden acceder mediante HTTP o HTTPS.Otra carateristica importante es que con esto los datos se vuelven duraderos y altamente disponibles, seguros y escalabes de froma masiva.
* ¿Cuáles son los tipos de planes para un Function App?, ¿En qué se diferencias?, mencione ventajas y desventajas de cada uno de ellos.
  - Plan de consumo: Las instancias que se encuentran en ell host de Azure Functions se agregan y eliminan dinámicamente teniendo en cuenta la cantidad de eventos que entren, este plan no contiene un servidor y hace un escalamiento automatico, los recursos se cobran únicamente cuando las funciones son ejecutados, si las funciones se encuentran en una misma región se puede asignar el mismo plan de consumo  
  El cobro se basa en la cantidad de ejecucuiones, tiempo de ejecución y la memoria que se utiliza.
  - Plan premium: Al utilizar el plan Premium , las instancias del host se agregan y eliminan en función de la cantidad de eventos que entran, este plan permite crear instancias perpetuamente calientes para así evitar los arranques frios, conectividad Vnet, ejecución limitada 60 minutos garantizados, varios tamaños de instancias como instancias de un núcleo, dos núcleos y cuatro núcleos.
  El cobro se basa en la cantidad de segundos centrales y la memoria utilizada en todas la instancias, al menos una de las instancias debe estar caliente.
  - Plan dedicado: Las functio app pueden ser ejecutadas en las maquinas virtuales dedicadas que otras aplicaciones de App Service, se debería usar para cuando se tienen maquinas virtuales subutilizadas que ta estén ejecutando otras instancias y si se desea proporcionar una imagen personalizada en la que se ejecuten las funciones.
  
* ¿Por qué la memorization falla o no funciona de forma correcta?
* ¿Cómo funciona el sistema de facturación de las Function App?
Al momento de realizar el registro de Azure se crea una cuenta de facturación , desde ahíse uede administrar facturas ,pagos y costos.Además se cuenta con diferentes cuentas de facturación como:

  - Microsoft Online Services Program: Esta se crea al momento de registrarse en el sitio web de Azure, la cuenta de facturación representa a un propietario único para una o varias suscripciones, un administrador de cuenta está autorizado para realizar varias tareas de facturación, como crear las suscripciones ,ver facturas o cambiar la facturación de las suscripciones.
  - Contrato Enterprise: Se crea una cuenta de facturación para un contrtato empresarial,representa una inscripcion de contrato enterpirse, la factura se genera en el ambito de la cuenta de facturacion, se estructura mediante el uso de cuentas de inscripción y departamentos.
  - Contrato de cliente de Microsoft: Se crea cuando una organización trabaja con un representate de Microsoft para firmamr un contrato de cliente de Microsoft, representa un contrato de cliente para varios productos y servicios de microsoft, la cuenta de facturación se estructura mediante el uso de perfiles de faturacion y las secciones de la factura
  
* Informe
- Creacion de Function App
![ARSW1](https://user-images.githubusercontent.com/43153078/79776242-14778200-82fb-11ea-8a03-c248503e945e.PNG)
![arsw2](https://user-images.githubusercontent.com/43153078/79776245-15101880-82fb-11ea-9246-36e45acf5a6f.PNG)
![arsw3](https://user-images.githubusercontent.com/43153078/79776247-15a8af00-82fb-11ea-9c76-257f90d700ef.PNG)
- Instalación Azure Function VSCode
![arsw4](https://user-images.githubusercontent.com/43153078/79776249-15a8af00-82fb-11ea-9f95-a47945e4d701.PNG)
- Instalación Power Shell
![image](https://user-images.githubusercontent.com/43153078/79777186-80a6b580-82fc-11ea-8a1f-8e5b82db03c6.png)
- Despliegue
![arsw5](https://user-images.githubusercontent.com/43153078/79776252-16d9dc00-82fb-11ea-9c4b-a1ca70d7b092.PNG)
