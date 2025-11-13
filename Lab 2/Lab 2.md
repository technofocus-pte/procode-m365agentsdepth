# Cree un agente de juego de geolocalización basado en instrucciones utilizando Microsoft 365 Agents Toolkit

**Tiempo estimado: 30 minutos**

## Objetivo

El objetivo de este laboratorio es capacitar a los participantes para
crear un agente declarativo para Microsoft 365 Copilot utilizando
Microsoft 365 Agents Toolkit. Al completar el laboratorio, los
participantes habrán desarrollado un juego de geolocalización que ofrece
una pausa divertida y educativa durante la jornada laboral. El
laboratorio se centra en comprender la estructura de los agentes
declarativos, configurarlos mediante instrucciones e integrarlos en el
ecosistema de Microsoft 365 para habilitar interacciones personalizadas
con Copilot.

## Solución

Los participantes instalarán Microsoft 365 Agents Toolkit en Visual
Studio Code y configurarán su entorno de desarrollo. Utilizando una
plantilla, crearán la estructura de un agente declarativo llamado **Geo
Locator Game**. Personalizarán las instrucciones del agente y
actualizarán sus archivos de configuración, como **instruction.txt** y
**manifest.json**. El laboratorio también guía a los participantes para
mejorar el agente con identificadores únicos, íconos personalizados y
funcionalidades de prueba. El resultado será una aplicación
completamente funcional e interactiva de Copilot, diseñada para ofrecer
pistas sobre ciudades e integrarse sin inconvenientes con Microsoft 365.

## Ejercicio 1: Configurar el entorno de desarrollo para Microsoft 365 Copilot

### Tarea 1: Instalar Microsoft 365 Agents Toolkit

1.  Abra **Visual Studio Code** y seleccione el botón **Extensions** en
    la barra de herramientas.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image1.png)

2.  Busque +++**Microsoft 365 agents**+++ y localice la extensión
    **Microsoft 365 Agents Toolkit.**

	![image](./media/image2.png)

3.  Seleccione **Install**.

	![image](./media/image3.png)

4.  Una vez completada la instalación, el ícono de **Microsoft 365
    Agents Toolkit** aparecerá en la barra de navegación lateral.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

	[!Nota] **Nota:** Microsoft 365 Agents Toolkit es una evolución de
Teams Toolkit. Actualmente se encuentra en una fase de transición, por
lo que en algunos lugares aparece como ***Teams Toolkit*** y en otros
como ***Microsoft 365 Agents Toolkit***.

## Ejercicio 2: Primer agente declarativo

En este laboratorio se creará un agente declarativo sencillo utilizando
Microsoft 365 Agents Toolkit para Visual Studio Code. El agente está
diseñado para ofrecer una pausa divertida y educativa durante la jornada
laboral, ayudando a explorar diferentes ciudades del mundo. Presentará
pistas abstractas para adivinar una ciudad, otorgando menos puntos a
medida que se utilizan más pistas. Al final, mostrará la puntuación
final.

En este ejercicio se aprenderá a:

- Comprender qué es un agente declarativo para Microsoft 365 Copilot.

- Crear un agente declarativo utilizando la plantilla del Microsoft 365
  Agents Toolkit.

- Personalizar el agente para convertirlo en un juego de geolocalización
  mediante instrucciones.

- Aprender a ejecutar y probar la aplicación.

- (Ejercicio adicional) Usar un sitio de SharePoint Teams.

**Introducción**

Los agentes declarativos aprovechan la misma infraestructura escalable y
la misma plataforma que **Microsoft 365 Copilot**, adaptándose
específicamente para abordar un área o necesidad concreta. Funcionan
como expertos temáticos en un dominio específico o en una necesidad
empresarial, permitiendo utilizar la misma interfaz de chat que un
Copilot estándar de Microsoft 365, pero centrándose exclusivamente en la
tarea para la cual fueron diseñados.

Bienvenido a la creación de su propio agente declarativo.  
¡Comencemos y hagamos que su Copilot trabaje con un toque de magia!

En este laboratorio se iniciará la construcción de un agente declarativo
utilizando **Microsoft 365 Agents Toolkit** con una plantilla
predeterminada disponible en la herramienta, para facilitar el punto de
partida. Posteriormente, se modificará el agente para enfocarlo en un
**juego de geolocalización**.

El objetivo de esta IA es ofrecer un descanso entretenido del trabajo
mientras ayuda a aprender sobre distintas ciudades del mundo.
Proporcionará pistas abstractas para identificar una ciudad: cuanto más
pistas se necesiten, menos puntos se obtendrán. Al finalizar el juego,
se mostrará la **puntuación final**.

![A screenshot of a chat AI-generated content may be
incorrect.](./media/image5.png)

También se proporcionarán al agente algunos archivos de referencia: un
**diario secreto 🕵🏽** y un **mapa 🗺️**, con el fin de añadir más
desafíos al jugador.

Así que, **comencemos**.

**Anatomía de un agente declarativo**

A medida que se desarrollen más extensiones para Copilot, se observará
que, en última instancia, lo que se construye es un conjunto de archivos
contenidos en un archivo **.zip**, al que se denomina **paquete de
aplicación (app package)**, que posteriormente se instala y utiliza.

Por ello, es importante comprender la estructura básica de un paquete de
aplicación. El **paquete de aplicación de un agente declarativo** es
similar al de una aplicación de Teams (si se ha creado una
anteriormente), pero incluye **elementos adicionales**.

La siguiente tabla presenta los **componentes principales** que
conforman dicho paquete. Además, el proceso de implementación del agente
es **muy similar al de una aplicación de Teams**.

|	Elemento|	Descripción|	Nombre del archivo|
|:-----|:--------|:---------|:---------|
|Manifiesto de la aplicación	|Describe la configuración de la aplicación, sus capacidades, los recursos necesarios y los atributos importantes.	|manifest.json	|
|Íconos de la aplicación	|Requiere un ícono en color (192x192) y un ícono con contorno (32x32) para el agente declarativo.	|	icon.png, color.png|
|Manifiesto del agente declarativo	|	Describe la configuración del agente, las instrucciones, los campos requeridos, las funcionalidades, los iniciadores de conversación y las acciones.|declarativeAgent.json	|

**Nota:** Es posible agregar datos de referencia desde SharePoint,
OneDrive, búsquedas web, entre otros, así como extender las
funcionalidades de un agente declarativo mediante complementos (plugins)
y conectores. En los próximos laboratorios de este recorrido se
aprenderá cómo agregar un complemento.

**Capacidades de un agente declarativo**

Es posible mejorar el enfoque del agente en el contexto y los datos no
solo mediante instrucciones, sino también especificando la base de
conocimiento a la que debe acceder. Estas se denominan capacidades y
existen tres tipos compatibles:

- **Microsoft Graph Connectors:** Permite pasar las conexiones de los
  conectores de Graph al agente, de modo que pueda acceder y utilizar el
  conocimiento proporcionado por dichos conectores.

- **OneDrive y SharePoint:** Proporciona al agente las direcciones URL
  de archivos y sitios para permitirle acceder a su contenido.

- **Búsqueda web:** Habilita o deshabilita el acceso a contenido web
  como parte de la base de conocimiento del agente.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

**OneDrive y SharePoint  
**Las direcciones URL deben ser rutas completas hacia los elementos de
SharePoint (sitio, biblioteca de documentos, carpeta o archivo). Es
posible obtener la ruta completa de archivos y carpetas mediante la
opción “Copiar vínculo directo” en SharePoint. Para hacerlo, haga clic
con el botón derecho sobre el archivo o carpeta y seleccione Detalles.
Luego, navegue hasta Ruta y haga clic en el ícono de copiar.  
Si no se especifican las URL, el agente utilizará todo el contenido
disponible en OneDrive y SharePoint para el usuario que haya iniciado
sesión.

**Microsoft Graph Connector  
**Si no se especifican las conexiones, el agente utilizará todo el
contenido disponible de los conectores de Graph asociados al usuario que
haya iniciado sesión.

**Búsqueda web  
**Actualmente no es posible definir sitios web o dominios específicos;
esta funcionalidad actúa únicamente como un interruptor para habilitar o
deshabilitar el uso de contenido web.

## Ejercicio 3: Generar un agente declarativo a partir de una plantilla

Es posible utilizar cualquier editor para crear un agente declarativo,
siempre que se conozca la estructura de los archivos que componen el
paquete de la aplicación mencionada anteriormente. Sin embargo, el
proceso resulta más sencillo utilizando una herramienta como **Microsoft
365 Agents Toolkit**, que no solo genera automáticamente dichos
archivos, sino que también facilita la implementación y publicación de
la aplicación. Por lo tanto, para simplificar el procedimiento, se
utilizará **Microsoft 365 Agents Toolkit**.

### Tarea 1: Usar Microsoft 365 Agents Toolkit para crear una aplicación de agente declarativo

1.  Vaya a la extensión **Microsoft 365 Agents Toolkit** en el editor
    **Visual Studio Code** y seleccione **Create a New App.**

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

2.  Se abrirá un panel en el cual será necesario seleccionar **Agent**
    de la lista de tipos de proyecto disponibles.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image8.png)

3.  Se solicitará seleccionar la característica de la aplicación para el
    agente de Copilot. Elija **Declarative Agent**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image9.png)

4.  A continuación, se le pedirá elegir si desea crear un agente
    declarativo básico o uno con un complemento de API. Seleccione la
    opción **No Plugin**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image10.png)

5.  Luego, seleccione la opción **Default folder** para especificar la
    ubicación donde se creará la carpeta del proyecto.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image11.png)

6.  A continuación, asigne el nombre de la aplicación +++**Geo Locator
    Game**+++ y presione **Enter**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image12.png)

	El proyecto se creará en unos segundos dentro de la carpeta especificada
y se abrirá en una nueva ventana de proyecto en Visual Studio Code. Esta
será su carpeta de trabajo.

7.  Si aparece un mensaje solicitando confirmar la confiabilidad del
    origen, seleccione **Yes, I trust the authors.**

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image13.png)

	![A screenshot of a computer AI-generated content may be incorrect.](./media/image14.png)

	¡Bien hecho! Ha configurado correctamente el agente declarativo base.
Ahora, continúe revisando los archivos incluidos para poder
personalizarlo y convertirlo en la aplicación **Geo Locator Game**.

### Tarea 2: Configurar las cuentas en Microsoft 365 Agents Toolkit

1.  Ahora seleccione el ícono de **Microsoft 365 Agents Toolkit** en el
    panel izquierdo. En la sección **Accounts**, haga clic en **Sign in
    to Microsoft 365** e inicie sesión con sus credenciales de **User1**
    dentro de la sección **Azure Portal**, ubicada en la pestaña
    **Resources.**

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image15.png)

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image16.png)

2.  Se abrirá una ventana del navegador que le permitirá iniciar sesión
    en Microsoft 365.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

3.  Seleccione **Allow access** en el cuadro de diálogo de **Security
    Alert**.

	![A screenshot of a computer security alert AI-generated content may be
incorrect.](./media/image18.png)

4.  Cuando la ventana del navegador muestre el mensaje “**You are signed
    in now and close this page**”, ciérrela.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image19.png)

5.  Verifique que el indicador **Custom App Upload Enabled** muestre una
    marca de verificación en color verde.

	![image](./media/image20.png)

### Tarea 3: Comprender los archivos de la aplicación

Así es como se ve el proyecto base:

|	Carpeta/Archivo|Contenido	|
|:-----|:-------|
|	.vscode|Archivos de VSCode para depuración.	|
|appPackage	|Plantillas para el manifiesto de la aplicación de Teams, el manifiesto de GPT y la especificación de la API.	|
|env	|Archivos de entorno con un archivo predeterminado .env.dev.	|
|	appPackage/color.png|	Imagen del logotipo de la aplicación.|
|	appPackage/outline.png|	Imagen del contorno del logotipo de la aplicación.|
|appPackage/declarativeAgent.json	|Define la configuración y los ajustes del agente declarativo.	|
|appPackage/instruction.txt	|	Define el comportamiento del agente declarativo.|
|appPackage/manifest.json	|Manifiesto de la aplicación de Teams que define los metadatos de su agente declarativo.	|
|teamsapp.yml	|	Archivo principal del proyecto de Microsoft 365 Agents Toolkit. Este archivo define dos elementos principales: las propiedades y las definiciones de las etapas de configuración.|


1.  El archivo de interés para este laboratorio es principalmente
    **appPackage/instruction.txt**, que contiene las directrices
    principales necesarias para su agente. Es un archivo de texto sin
    formato en el que se pueden escribir instrucciones en lenguaje
    natural.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image21.png)

2.  Otro archivo importante es **appPackage/declarativeAgent.json**, que
    contiene un esquema que debe seguirse para ampliar **Microsoft 365
    Copilot** con el nuevo agente declarativo. Veamos qué propiedades
    incluye el esquema de este archivo:

    - **$schema**: referencia al esquema.

    - **version**: versión del esquema.

    - **name**: representa el nombre del agente declarativo.

    - **description**: proporciona una descripción.

    - **instructions**: indica la ruta al archivo **instructions.txt**,
      que contiene las directrices que determinarán el comportamiento
      operativo. También es posible incluir las instrucciones
      directamente como texto en esta propiedad, pero para este
      laboratorio se utilizará el archivo **instructions.txt**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image22.png)

3.  Otro archivo importante es **appPackage/manifest.json**, que
    contiene metadatos esenciales, como el nombre del paquete, el nombre
    del desarrollador y las referencias a los agentes de Copilot
    utilizados por la aplicación. El siguiente fragmento del archivo
    **manifest.json** ilustra estos detalles:

	```
	"copilotAgents": {
			"declarativeAgents": [            
				{
					"id": "declarativeAgent",
					"file": "declarativeAgent.json"
				}
			]
		},

	```

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image23.png)

4.  También es posible actualizar los archivos de logotipo **color.png**
    y **outline.png** para que coincidan con la identidad visual de su
    aplicación. En el laboratorio de hoy, se modificará el ícono
    **color.png** del agente para hacerlo más destacado.

## Ejercicio 4: Actualizar instrucciones e ícono

### Tarea 1: Actualizar íconos y manifiestos

1.  Primero, se reemplazará el logotipo. Sustituya la imagen
    **color.png** del proyecto por una nueva.  
    Copie la imagen **color.png** ubicada en **C:\LabFiles** y
    reemplácela por la imagen del mismo nombre en la carpeta
    **appPackage** dentro del directorio raíz de su proyecto.  
    (La ruta debe ser **C:\Users\Student\TeamsApps\Geo Locator
    Game\appPackage**).

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image24.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image25.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image26.png)

2.  A continuación, abra el archivo **appPackage/manifest.json** en el
    directorio raíz del proyecto y localice el nodo **copilotAgents**.  
    Actualice el valor de **id** en la primera entrada del arreglo
    **declarativeAgents**, cambiándolo de **declarativeAgent** a
    **+++dcGeolocator+++**, con el fin de que este identificador sea
    único.

	```
	"copilotAgents": {
			"declarativeAgents": [            
				{
					"id": "dcGeolocator",
					"file": "declarativeAgent.json"
				}
			]
		},

	```

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image27.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image28.png)

3.  A continuación, abra el archivo **appPackage/instruction.txt** y
    copie y pegue la siguiente instrucción para sobrescribir el
    contenido existente del archivo.

	```
	System Role: You are the game host for a geo-location guessing game. Your goal is to provide the player with clues about a specific city and guide them through the game until they guess the correct answer. You will progressively offer more detailed clues if the player guesses incorrectly. You will also reference PDF files in special rounds to create a clever and immersive game experience.

	Game play Instructions:

	Game Introduction Prompt

	Use the following prompt to welcome the player and explain the rules:

	Welcome to the Geo Location Game! I’ll give you clues about a city, and your task is to guess the name of the city. After each wrong guess, I’ll give you a more detailed clue. The fewer clues you use, the more points you score! Let’s get started. Here’s your first clue:

	Clue Progression Prompts

	Start with vague clues and become progressively specific if the player guesses incorrectly. Use the following structure:

	Clue 1: Provide a general geographical clue about the city (e.g., continent, climate, latitude/longitude).

	Clue 2: Offer a hint about the city’s landmarks or natural features (e.g., a famous monument, a river).

	Clue 3: Give a historical or cultural clue about the city (e.g., famous events, cultural significance).

	Clue 4: Offer a specific clue related to the city’s cuisine, local people, or industry.

	Response Handling

	After the player’s guess, respond accordingly:
	If the player guesses correctly, say:

	That’s correct! You’ve guessed the city in [number of clues] clues and earned [score] points. Would you like to play another round?

	If the guess is wrong, say:

	Nice try! [followed by more clues]

	PDF-Based Scenario

	For special rounds, use a PDF file to provide clues from a historical document, traveler's diary, or ancient map:

	This round is different! I’ve got a secret document to help us. I’ll read clues from this [historical map/traveler’s diary] and guide you to guess the city. Here’s the first clue:

	Reference the specific PDF to extract details:
	Traveler's Diary PDF,Historical Map PDF.
	Use emojis where necessary to have friendly tone. 
	Scorekeeping System

	Track how many clues the player uses and calculate points:

	1 clue: 10 points

	2 clues: 8 points

	3 clues: 5 points

	4 clues: 3 points

	End of Game Prompt

	After the player guesses the city or exhausts all clues, prompt:

	Would you like to play another round, try a special challenge?

	```

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image29.png)

4.  Observe esta línea en **appPackage/declarativeAgent.json**:

	"instructions": "$[file('instruction.txt')]",

	Esto incorpora las instrucciones desde el archivo **instruction.txt**.
Si se desea modularizar los archivos del paquete, puede utilizarse esta
técnica en cualquiera de los archivos JSON dentro de la carpeta
**appPackage**.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image30.png)

### Tarea 2: Agregar iniciadores de conversación

Es posible mejorar la interacción del usuario con el agente declarativo
agregando iniciadores de conversación.

Algunos de los beneficios de incluir iniciadores de conversación son los
siguientes:

- **Interacción:** Ayudan a iniciar la comunicación, generando comodidad
  en el usuario y fomentando la participación.

- **Establecimiento de contexto:** Los iniciadores definen el tono y el
  tema de la conversación, orientando al usuario sobre cómo proceder.

- **Eficiencia:** Al comenzar con un enfoque claro, reducen la
  ambigüedad y permiten que la conversación avance con fluidez.

- **Retención del usuario:** Los iniciadores bien diseñados mantienen el
  interés del usuario, promoviendo interacciones repetidas con la IA.

1.  Abra el archivo **declarativeAgent.json** y, justo después del nodo
    **instructions**, agregue una coma, presione **Enter** y pegue el
    siguiente código.

	```
	"conversation_starters": [
		{ 
				"title": "Getting Started",
				"text":"I am ready to play the Geo Location Game! Give me a city to guess, and start with the first clue." 
			},
			{
				"title": "Ready for a Challenge",
				"text": "Let us try something different. Can we play a round using the travelers diary?"
			},
			{ 
				"title": "Feeling More Adventurous",
				"text": "I am in the mood for a challenge! Can we play the game using the historical map? I want to see if I can figure out the city from those ancient clues."
			}
		]

	```

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image31.png)

Ahora que se han realizado todos los cambios en el agente, es momento de
probarlo.

2.  Vaya a **Files** en la barra superior y seleccione **Save All.**

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

### Tarea 3: Probar la aplicación

1.  Para probar la aplicación, vaya a la extensión **Microsoft 365
    Agents Toolkit** en Visual Studio Code. Esto abrirá el panel
    izquierdo. En la sección **LIFECYCLE**, seleccione **Provision**.
    Aquí podrá observar el valor de **Microsoft 365 Agents Toolkit**, ya
    que simplifica significativamente el proceso de publicación.

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image33.png)

	![A screenshot of a computer AI-generated content may be
	incorrect.](./media/image34.png)

2.  Si se le solicita, inicie sesión con sus credenciales.

	![A screen shot of a computer AI-generated content may be
incorrect.](./media/image35.png)

3.  En este paso, **Microsoft 365 Agents Toolkit** empaquetará todos los
    archivos dentro de la carpeta **appPackage** como un archivo
    **.zip** e instalará el agente declarativo en su propio catálogo de
    aplicaciones.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image36.png)

4.  Abra un navegador y navegue a
    +++https://m365.cloud.microsoft/chat/+++ logged con sesión
    iniciada en su entorno de desarrollo. Desde el panel izquierdo, abra
    **Geo Locator Game**.

	![image](./media/image37.png)

5.  Una vez iniciada, se mostrará la ventana de chat enfocada con el
    agente, donde se visualizarán los iniciadores de conversación
    indicados a continuación:

	![image](./media/image38.png)

6.  Seleccione uno de los iniciadores de conversación y este completará
    el cuadro de redacción del mensaje con el prompt correspondiente,
    quedando a la espera de que presione "Enter". El asistente
    permanecerá inactivo hasta que se realice esta acción.

	![A screenshot of a computer AI-generated content may be
incorrect.](./media/image39.png)

7.  Pruebe responder la pregunta y explore el juego que ha desarrollado.

## Resumen:

En este laboratorio, se aprendió a crear un agente declarativo mediante
**Microsoft 365 Agents Toolkit** y a comprobar su funcionalidad.
