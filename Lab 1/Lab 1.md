# Laboratorio 1: Creación de un agente declarativo RepairService con definición en TypeSpec mediante Microsoft 365 Agents Toolkit

**Objetivo**

En este laboratorio se construirá un agente declarativo con definición
en **TypeSpec** utilizando **Microsoft 365 Agents Toolkit**. Se creará
un agente denominado **RepairServiceAgent**, el cual interactuará con
datos de reparaciones mediante un servicio API existente para ayudar a
los usuarios a gestionar los registros de reparaciones de automóviles.

**Agentes declarativos**

Los agentes declarativos son un tipo de agente para **Microsoft 365**.
Es posible crear uno ampliando las funcionalidades de **Microsoft 365
Copilot**. En este proceso se definen conocimientos y acciones
personalizadas con el fin de crear agentes adaptados a un escenario
específico.

Los agentes declarativos utilizan la misma infraestructura, orquestador,
modelo base y controles de seguridad que **Microsoft 365 Copilot**, lo
que garantiza una experiencia de usuario coherente y familiar.

![Declarative agent architecture diagram. At the very basis there is the
foundational model of Microsoft 365 Copilot, as well as the same
orchestrator. The agent provides also custom knowledge and grounding
data, and custom skills as actions, triggers, and workflows.. The user
experience is available in Microsoft 365 Copilot.](./media/image1.png)

**Importancia de TypeSpec para los agentes declarativos**

**¿Qué es TypeSpec?**

TypeSpec es un lenguaje desarrollado por Microsoft para diseñar y
describir contratos de API de manera estructurada y con tipado seguro.
Puede considerarse como un plano que define cómo debe verse y
comportarse una API, especificando qué datos acepta, qué devuelve y cómo
se conectan las distintas partes de la API y sus acciones.

**¿Por qué utilizar TypeSpec para los agentes?**

Si se aprecia cómo TypeScript impone estructura en el código de frontend
o backend, TypeSpec ofrece un beneficio similar al aplicar estructura a
los agentes y a los servicios API que utilizan, como las acciones. Se
integra perfectamente en flujos de trabajo de desarrollo con enfoque de
diseño inicial (*design-first*), compatibles con herramientas como
Visual Studio Code.

- Comunicación clara: proporciona una fuente única de verdad que define
  cómo debe comportarse el agente, evitando confusiones al trabajar con
  múltiples archivos de manifiesto, como en el caso de los agentes
  declarativos.

- Consistencia: garantiza que todas las partes del agente como acciones,
  capacidades, entre otros elementos se diseñen siguiendo un patrón
  uniforme.

- Compatibilidad con la automatización: genera automáticamente
  especificaciones OpenAPI y otros manifiestos, lo que ahorra tiempo y
  reduce errores humanos.

- Validación temprana: permite detectar problemas de diseño antes de
  escribir el código real, como tipos de datos incompatibles o
  definiciones poco claras.

- Enfoque basado en diseño: fomenta la reflexión sobre la estructura del
  agente y los contratos de API antes de la implementación, lo que
  contribuye a una mejor mantenibilidad a largo plazo.

## Ejercicio 1: Configurar el entorno de laboratorio

En este ejercicio se configurará el entorno de desarrollo necesario para
compilar, probar e implementar los agentes de **Copilot**, los cuales
permitirán ofrecer asistencia de IA personalizada mediante **Microsoft
365 Copilot**.

### Tarea 1: Instalar Agents Toolkit

El **Agents Toolkit** para **Visual Studio Code** requiere tener
instalado **Visual Studio Code**. En este ejercicio se instalará el
toolkit en dicho entorno.

1.  Abra **Visual Studio Code** desde la máquina virtual (VM).
    Seleccione **Extensions** en el menú lateral izquierdo.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

2.  Busque y seleccione **Microsoft 365 Agents Toolkit**, luego haga
    clic en **Install**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image3.png)

3.  Verifique que el **toolkit** se haya instalado correctamente.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

4.  Cree una nueva carpeta denominada **ServiceAgent** en su escritorio.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image5.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image6.png)

## Ejercicio 2: Crear el agente base con TypeSpec utilizando Microsoft 365 Agents Toolkit

En este ejercicio se construirá un **agente declarativo**, se definirá
su estructura, se actualizarán las acciones y se realizará una prueba
del agente.

### Tarea 1: Generar el proyecto base del agente utilizando Microsoft 365 Agents Toolkit

En esta tarea se construirá un agente declarativo con definición en
**TypeSpec** mediante **Microsoft 365 Agents Toolkit**. Se creará un
agente denominado **RepairServiceAgent**, el cual interactuará con datos
de reparaciones a través de un servicio API existente para ayudar a los
usuarios a gestionar registros de reparaciones de automóviles.

1.  Ubique el ícono de **Microsoft 365 Agents Toolkit** en el menú
    lateral de **Visual Studio Code** y selecciónelo. Se abrirá una
    barra de actividades. En dicha barra, seleccione el botón **Create a
    New Agent/App**, lo que abrirá la paleta con una lista de plantillas
    de aplicaciones disponibles en **Microsoft 365 Agents Toolkit**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

2.  Seleccione **Declarative Agent** de la lista de plantillas.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image8.png)

3.  A continuación, seleccione **Start with TypeSpec for Microsoft 365
    Copilot** para definir el agente utilizando **TypeSpec**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

4.  A continuación, seleccione la carpeta **ServiceAgent** desde el
    escritorio. Esta será la ubicación donde **Agents Toolkit** generará
    la estructura del proyecto del agente.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

5.  A continuación, ingrese el nombre de la aplicación como
    +++**RepairServiceAgent**+++ y presione **Enter** para completar el
    proceso. Se abrirá una nueva ventana de **Visual Studio Code** con
    el proyecto del agente precargado.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

6.  Será necesario iniciar sesión en **Microsoft 365 Agents Toolkit**
    para poder cargar y probar el agente directamente desde la
    herramienta.

7.  En la ventana del proyecto, seleccione nuevamente el ícono de
    **Microsoft 365 Agents
    Toolkit **![m365atk-icon](./media/image13.png) en el menú lateral
    izquierdo. Esto abrirá la barra de actividades del toolkit, con
    secciones como **Accounts**, **Environment**, **Development**, entre
    otras.

8.  En la sección **Accounts**, seleccione **Sign in to Microsoft 365**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image14.png)

9.  Se abrirá un cuadro de diálogo en el editor con las opciones **Sign
    in**, **Create a Microsoft 365 developer sandbox** o **Cancel**.
    Seleccione **Sign in** e inicie sesión con sus credenciales.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image15.png)

10. Una vez iniciada la sesión, **cierre** el navegador y regrese a la
    ventana del proyecto.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

### Tarea 2: Definir el agente

El proyecto de agente declarativo generado por **Agents Toolkit**
proporciona una plantilla que incluye código para conectar un agente con
la API de GitHub y mostrar incidencias de repositorios. En este
laboratorio, se construirá un agente propio que se integrará con un
servicio de reparaciones de automóviles, admitiendo múltiples
operaciones para administrar los datos de reparación.

En la carpeta del proyecto se encontrarán dos archivos **TypeSpec:
main.tsp** y **actions.tsp.**

El archivo **main.tsp** define el agente, incluyendo su metadato,
instrucciones y capacidades.

El archivo **actions.tsp** se utiliza para definir las acciones del
agente. Si el agente incluye acciones, como la conexión a un servicio
API, deberán especificarse en este archivo.

Abra el archivo **main.tsp** y revise el contenido de la plantilla
predeterminada, el cual se modificará para adaptarlo al escenario del
servicio de reparaciones.

Actualizar los metadatos e instrucciones del agente.

En el archivo **main.tsp** se encuentra la estructura básica del agente.
Revise el contenido proporcionado por la plantilla del **Agents
Toolkit**, que incluye:

- **Nombre** y **descripción del agente** 1️⃣

- **Instrucciones** básicas 2️⃣

- Código de marcador de posición para **acciones** y **capacidades**
  (comentado) 3️⃣

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

1.  Identifique los bloques de código **@agent** e **@instructions**
    (desde la línea 10 hasta la 17).

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image18.png)

2.  Comience definiendo el agente para el escenario de reparaciones.
    Reemplace las definiciones de **@agent** e **@instruction** con el
    siguiente fragmento de código.

    ```
    @agent(
    "RepairServiceAgent",
    "An agent for managing repair information"
    )

    @instructions("""
    ## Purpose
    You will assist the user in finding car repair records based on the information provided by the user. 
    """)

    ```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image19.png)

3.  A continuación, agregue un iniciador de conversación para el agente.
    Justo debajo de las instrucciones, se encontrará un bloque de código
    comentado correspondiente al **conversation starter**. Reemplace el
    bloque **@conversationStarter** (de las líneas 22 a 25) con el
    siguiente código.

    ```
    @conversationStarter(#{
    title: "List repairs",
    text: "List all repairs"
    })

    ```

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image20.png)

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image21.png)

### Tarea 3: Actualizar la acción del agente

En esta tarea se definirá la acción del agente abriendo el archivo
**actions.tsp**. Posteriormente, se volverá al archivo **main.tsp** para
completar los metadatos del agente con la referencia a dicha acción,
pero primero será necesario definir la acción en sí.

El código de marcador de posición en **actions.tsp** está diseñado para
buscar incidencias abiertas en un repositorio de **GitHub**. Este código
sirve como punto de partida para comprender cómo definir una acción de
agente, incluyendo sus metadatos, la URL del host de la API y las
operaciones o funciones con sus respectivas definiciones. Todo este
contenido se reemplazará con la información correspondiente al servicio
de reparaciones.

1.  Abra el archivo **actions.tsp**. Reemplace el código que inicia con
    **@service** hasta **const SERVER_URL** (aproximadamente entre las
    líneas 7 y 25) con el siguiente bloque de código.

	Esta actualización introduce los metadatos de la acción y establece la
URL del servidor. Además, observe que el **namespace** se ha cambiado de
**GitHubAPI** a **RepairsAPI**.

    ```
    @service
    @server(RepairsAPI.SERVER_URL)
    @actions(RepairsAPI.ACTIONS_METADATA)
    namespace RepairsAPI{
    /**
    * Metadata for the API actions.
    */
    const ACTIONS_METADATA = #{
        nameForHuman: "Repair Service Agent",
        descriptionForHuman: "Manage your repairs and maintenance tasks.",
        descriptionForModel: "Plugin to add, update, remove, and view repair objects.",
        legalInfoUrl: "https://docs.github.com/en/site-policy/github-terms/github-terms-of-service",
        privacyPolicyUrl: "https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement"
    };

    /**
    * The base URL for the  API.
    */
    const SERVER_URL = "https://repairshub.azurewebsites.net";

    ```

2.  A continuación, reemplace la operación del código de la plantilla,
    cambiando **searchIssues** por **listRepairs**, que corresponde a
    una operación destinada a obtener la lista de reparaciones.
    Reemplace todo el bloque de código que comienza justo después de la
    definición de **SERVER_URL** y finaliza antes de las llaves de
    cierre con el siguiente fragmento de código. Asegúrese de dejar
    intactas las llaves de cierre. (Las líneas aproximadas van de la 27
    a la 37).

    ```
    /**
    * List repairs from the API 
    * @param assignedTo The user assigned to a repair item.
    */

    @route("/repairs")
    @get  op listRepairs(@query assignedTo?: string): string;

    ```

    ![A screenshot of a computer program AI-generated content may be incorrect.](./media/image22.png)

3.  Regrese ahora al archivo **main.tsp** y agregue la acción que acaba
    de definir al agente. Después del bloque de **conversation
    starters**, reemplace todo el bloque de código con el siguiente
    fragmento.

    ```
    namespace RepairServiceAgent{  
    // Uncomment this part to add actions to the agent.
    @service
    @server(global.RepairsAPI.SERVER_URL)
    @actions(global.RepairsAPI.ACTIONS_METADATA)
    namespace RepairServiceActions {
        op listRepairs is global.RepairsAPI.listRepairs;   
    }
    }
    ```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image23.png)

### Tarea 4: (Solo lectura) Comprender los decoradores

Esta tarea tiene como objetivo comprender lo que se ha definido en el
archivo **TypeSpec**. Solo es necesario leer y analizar el contenido. En
los archivos **main.tsp** y **actions.tsp** se encontrarán
**decoradores** (que comienzan con **@**), **namespaces**, **modelos** y
otras definiciones relacionadas con el agente.

A continuación, se describen algunos de los decoradores utilizados en
estos archivos:

- **@agent –** Define el namespace (nombre) y la descripción del agente.

- **@instructions –** Define las instrucciones que determinan el
  comportamiento del agente. Deben tener un máximo de 8000 caracteres.

- **@conversationStarter –** Define los iniciadores de conversación del
  agente.

- **op –** Define una operación. Puede utilizarse para describir las
  capacidades del agente, como **op GraphicArt** o **op
  CodeInterpreter**, o para definir operaciones de API, como **op
  listRepairs**.

- **@server –** Define el punto de conexión (endpoint) del servidor de
  la API y su nombre.

- **@capabilities –** Cuando se utiliza dentro de una función, permite
  definir adaptive cards simples con estructuras concisas, por ejemplo,
  una tarjeta de confirmación para una operación.

### Tarea 5: Probar el agente

En esta tarea se realizará la prueba del **Repair Service Agent** recién
creado.

1.  Seleccione el ícono de la extensión **Agents Toolkit** para abrir la
    barra de actividades dentro del proyecto.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image24.png)

2.  En la barra de actividades de **Agents Toolkit**, dentro de la
    sección **LifeCycle**, seleccione **Provision**. Esta acción
    generará el paquete de la aplicación, que incluirá los archivos de
    manifiesto e íconos creados, y cargará la aplicación en el catálogo
    únicamente para su prueba.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image25.png)

3.  Abra su navegador web y vaya a
    +++<https://m365.cloud.microsoft/chat+++> para abrir la aplicación
    **Copilot**.

4.  Seleccione **RepairServiceAgent** de la lista de agentes disponibles
    en la interfaz de **Microsoft 365 Copilot**. Este proceso puede
    tardar unos minutos, y se mostrará un mensaje emergente indicando el
    progreso de la tarea de aprovisionamiento.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image26.png)

5.  Seleccione el iniciador de conversación **List repairs** y envíe el
    *prompt*.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

6.  Esto iniciará la conversación con el agente y se podrá visualizar la
    respuesta generada, que mostrará la lista de reparaciones.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image28.png)

## Ejercicio 3: Ampliar las capacidades del agente

En este ejercicio, mejorará el agente añadiendo más operaciones,
habilitando respuestas con **Adaptive Cards** e incorporando capacidades
de intérprete de código. Analice cada una de estas mejoras paso por
paso. Regrese al proyecto en **VS Code.**

### Tarea 1: Modificar el agente para añadir más operaciones

En esta tarea se modificará el agente para incorporar operaciones
adicionales, tales como **createRepair**, **updateRepair** y
**deleteRepair.**

1.  Vaya al archivo **actions.tsp** y copie y pegue el siguiente
    fragmento de código justo después de la operación **listRepairs**
    para agregar las nuevas operaciones **createRepair**,
    **updateRepair** y **deleteRepair**. En este bloque también se
    define el modelo de datos del elemento **Repair**.

    ```
    /**
    * Create a new repair. 
    * When creating a repair, the `id` field is optional and will be generated by the server.
    * The `date` field should be in ISO 8601 format (e.g., "2023-10-01T12:00:00Z").
    * The `image` field should be a valid URL pointing to the image associated with the repair.
    * @param repair The repair to create.
    */
    @route("/repairs")  
    @post  op createRepair(@body repair: Repair): Repair;

    /**
    * Update an existing repair.
    * The `id` field is required to identify the repair to update.
    * The `date` field should be in ISO 8601 format (e.g., "2023-10-01T12:00:00Z").
    * The `image` field should be a valid URL pointing to the image associated with the repair.
    * @param repair The repair to update.
    */
    @route("/repairs")  
    @patch  op updateRepair(@body repair: Repair): Repair;

    /**
    * Delete a repair.
    * The `id` field is required to identify the repair to delete.
    * @param repair The repair to delete.
    */
    @route("/repairs") 
    @delete  op deleteRepair(@body repair: Repair): Repair;

    /**
    * A model representing a repair.
    */
    model Repair {
        /**
        * The unique identifier for the repair.
        */
        id?: string;

        /**
        * The short summary or title of the repair.
        */
        title: string;

        /**
        * The detailed description of the repair.
        */
        description?: string;

        /**
        * The user who is assigned to the repair.
        */
        assignedTo?: string;

        /**
        * The optional date and time when the repair is scheduled or completed.
        */
        @format("date-time")
        date?: string;

        /**
        * The URL of the image associated with the repair.
        */
        @format("uri")
        image?: string;
    }
    ```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image29.png)

2.  Ahora, abra el archivo **main.tsp** y agregue estas nuevas
    operaciones dentro de las acciones del agente. Pegue el siguiente
    fragmento de código después de la línea **op listRepairs is
    global**.**RepairsAPI.listRepairs;**  
    dentro del *namespace* **RepairServiceActions**.

    ```
    op createRepair is global.RepairsAPI.createRepair;
    op updateRepair is global.RepairsAPI.updateRepair;
    op deleteRepair is global.RepairsAPI.deleteRepair;
    ```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image30.png)

3.  Agregue también un nuevo iniciador de conversación para la creación
    de un nuevo elemento de reparación, colocándolo justo después de la
    primera definición de **conversation starter**.

    ```
    @conversationStarter(#{
    title: "Create repair",
    text: "Create a new repair titled \"[TO_REPLACE]\" and assign it to me"
    })
    ```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image31.png)

### Tarea 2: Agregar una Adaptive Card a la referencia de la función

En esta tarea se mejorarán las tarjetas de referencia o tarjetas de
respuesta utilizando **Adaptive Cards**. Se tomará como ejemplo la
operación **listRepairs** para agregar una tarjeta adaptable que muestre
la información de cada elemento de reparación.

1.  En la carpeta del proyecto, cree una nueva carpeta denominada
    +++**cards**+++ dentro de la carpeta **appPackage.**

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

2.  Cree un archivo denominado +++**repair.json**+++ dentro de la
    carpeta **cards** y pegue en él el fragmento de código proporcionado
    a continuación, sin realizar modificaciones.

    ```
    {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
        "type": "AdaptiveCard",
        "version": "1.5",
        "body": [
    {
        "type": "Container",
        "$data": "${$root}",
        "items": [
        {
            "type": "TextBlock",
            "text": "Title: ${if(title, title, 'N/A')}",
            "weight": "Bolder",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Description: ${if(description, description, 'N/A')}",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Assigned To: ${if(assignedTo, assignedTo, 'N/A')}",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Date: ${if(date, date, 'N/A')}",
            "wrap": true
        },
        {
            "type": "Image",
            "url": "${image}",
            "$when": "${image != null}"
        }
        ]
    }
    ],  
        "actions": [
        {
            "type": "Action.OpenUrl",
            "title": "View Image",
            "url": "https://www.howmuchisit.org/wp-content/uploads/2011/01/oil-change.jpg"
        }
        ]
    }

    ```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image33.png)

3.  A continuación, regrese al archivo **actions.tsp** y ubique la
    operación **listRepairs**. Reemplace la línea de definición de la
    operación  
    **@get op listRepairs(@query assignedTo?: string): string;**  
    por las dos líneas de código que se indican a continuación.

    ```
    @card(#{ dataPath: "$", title: "$.title",   url: "$.image", file: "cards/repair.json"})
    @get op listRepairs(@query assignedTo?: string): Repair[];

    ```

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image34.png)

4.  La tarjeta de respuesta anterior será enviada por el agente cuando
    se solicite información sobre un elemento de reparación o cuando el
    agente muestre una lista de elementos como referencia.

5.  Dado que el agente ahora admite funcionalidades adicionales,
    actualice las instrucciones para reflejar esta mejora.

6.  En el mismo archivo **main.tsp**, modifique la definición de
    **@instructions** para incluir las nuevas directivas del agente.
    Reemplace el bloque de código existente de **@instructions** con el
    siguiente fragmento.

```
@instructions("""
  ## Purpose
You will assist the user in finding car repair records based on the information provided by the user. When asked to display a report, you will use the code interpreter to generate a report based on the data you have.

  ## Guidelines
- You are a repair service agent.
- You can use the actions to create, update, and delete repairs.
- When creating a repair item, if the user did not provide a description or date , use title as description and put todays date in format YYYY-MM-DD
- Do not show any code or technical details to the user. 
- Do not use any technical jargon or complex terms.

""")
```

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image35.png)

### Tarea 3: Aprovisionar y probar el agente

En esta tarea se probará el agente actualizado, que ahora también actúa
como analista de reparaciones.

1.  Seleccione el ícono de la extensión **Agents Toolkit** para abrir la
    barra de actividades dentro del proyecto.

2.  En la barra de actividades del toolkit, dentro de la sección
    **LifeCycle**, seleccione **Provision** para empaquetar y cargar el
    agente actualizado con el fin de realizar las pruebas.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image36.png)

3.  Verifique que el proceso de aprovisionamiento se complete
    correctamente.

	![A screenshot of a computer program AI-generated content may be
incorrect.](./media/image37.png)

4.  Regrese a la sesión del navegador que permanece abierta y
    **actualice** la página.

5.  En **RepairServiceAgent**, comience utilizando el iniciador de
    conversación **Create repair**. Modifique las partes del *prompt*
    para agregar un título y luego envíelo al chat para iniciar la
    interacción. Por ejemplo:

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image38.png)

6.  Reemplace **\[TO REPLACE\]** por +++**rear camera issue**+++ y
    asígnelo a usted mismo.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

7.  El cuadro de confirmación, como podrá observar, incluye más
    metadatos de los que se enviaron originalmente, gracias a las nuevas
    instrucciones incorporadas.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image40.png)

8.  Continúe agregando el elemento **confirm** el cuadro de diálogo.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image41.png)

9.  El agente responderá mostrando el elemento creado en una **Adaptive
    Card** enriquecida.

	![A screenshot of a chat AI-generated content may be
incorrect.](./media/image42.png)

10. A continuación, verifique nuevamente el funcionamiento de las
    tarjetas de referencia. Envíe el siguiente *prompt* en la
    conversación.

	+++**List all my repairs**+++.

	En el cuadro de confirmación, seleccione **Always allow**.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image43.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image44.png)

11. El agente responderá con la lista de reparaciones asignadas a usted,
    donde cada elemento estará representado mediante una **Adaptive
    Card**. En este caso, solo debería aparecer el registro
    correspondiente al crear **camera issue** que acaba de agregar.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image45.png)

12. A continuación, pruebe la nueva capacidad analítica del agente. Abra
    un nuevo chat seleccionando el botón **New chat** ubicado en la
    esquina superior derecha del agente.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

13. A continuación, copie el prompt que se muestra a continuación,
    péguelo en el cuadro de mensajes y presione **Enter** para enviarlo.

14. **Classify repair items based on title into three distinct
    categories:**

15. **Routine Maintenance, Critical, and Low Priority.**

16. **Then, generate a chart displaying the percentage representation of
    each category.**

	![A screenshot of a phone AI-generated content may be
incorrect.](./media/image47.png)

17. Deberá obtener una respuesta similar a la que se muestra en la
    pantalla de ejemplo; los resultados pueden variar ligeramente.

	![A screenshot of a data box AI-generated content may be
incorrect.](./media/image48.png)

**Resumen**

En este laboratorio se realizaron las siguientes actividades:

- Se utilizó **TypeSpec** para describir las API y vincularlas con las
  acciones de **Copilot**.

- Se configuraron **Adaptive Cards** para mostrar los registros de
  reparación con un diseño visual enriquecido.

- Se creó un escenario completo que permite a los usuarios interactuar
  de manera natural con **Copilot** para gestionar datos de
  reparaciones.

Este laboratorio demostró cómo los **agentes declarativos** aprovechan
la orquestación, los modelos base y los controles de seguridad de la
plataforma **Copilot** para ofrecer una experiencia de usuario coherente
y familiar, al tiempo que se integran con datos empresariales y flujos
de trabajo personalizados.
