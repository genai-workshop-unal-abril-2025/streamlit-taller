# Taller practico sobre Streamlit.

Este taller tiene como objetivo crear una aplicación de Streamlit en donde se pueda interactuar con modelos de inteligencia artificial generativa alojados en WatsonX, con una base de datos vectorial de ChromaDB y crear un RAG que permita consultar los documentos guardados en la base de datos vectorial.

## Prerrequisitos.
- Tener instalado Python. (La versión recomendada es **Python 3.11.9**. Esto debido a que en las versiones 3.12 y 3.13 se requiere descargar las Visual Studio Build Tools para poder instalar las dependencias de la app)
- (Opcional pero muy recomendable) Tener instalado Visual Studio Code.


## Paso 0: Preparación e Instalación de Streamlit.

### Paso 0.1: Crear una carpeta para almacenar el código de la aplicación.

![Carpeta Creada](./MultimediaREADME/Paso0/CarpetaCreada.png)

### Paso 0.2: Abrir la carpeta con un editor de código (Se recomienda Visual Studio Code).

![Carpeta Abierta VSC](./MultimediaREADME/Paso0/CarpetaAbiertaVSC.png)

### Paso 0.3: Abrir una consola ubicada en la carpeta del proyecto.

![Primera Consola Proyecto](./MultimediaREADME/Paso0/PrimeraConsolaProyecto.png)

### Paso 0.4: Verificar las versiones de Python instaladas en el computador.

Para listar las versiones de Python se puede ejecutar el siguiente comando en la consola.

```console
py --list
```

En la consola se deberia ver una lista de las versiones de Python instaladas. Por ejemplo, esta seria la respuesta en caso de tener instaladas las versiones 3.11 y 3.12:

![Lista Versiones Python](./MultimediaREADME/Paso0/ListaVersionesPython.png)

### Paso 0.5: Crear un entorno virtual de Python.

Un entorno virtual de python es una carpeta donde se tiene una versión de Python y paquetes instalados de forma aislada a la instalación principal de Python que se tiene en todo el sistema.

Para crear un entorno virtual que tenga nombre _.venv_ se debe usar el siguiente comando, donde la X se debe remplazar por la versión de Python con la que se quiere crear el entorno virtual

```console
py -3.X -m venv .venv
```

Por ejemplo, en caso de crear un entorno virtual de Python 3.11 (que es la version recomendada) se usaria el comando:

```console
py -3.11 -m venv .venv
```

Tras ejecutar el comando se debio crear una carpeta llamada _.venv_ en el proyecto, esta carpeta corresponde al entorno virtual que se usará para el proyecto:

![Entorno Virtual Creado](./MultimediaREADME/Paso0/EntornoVirtualCreado.png)

### Paso 0.6: Activar el entorno virtual en la terminal

En la terminal ubicada en la carpeta del proyecto se debe ejecutar alguno de los siguientes comandos para activar el entorno virtual.

En caso de tener una terminal de Powershell utilizar el comando:

```console
.\.venv\Scripts\activate.ps1
```

En caso de tener una terminal de comandos de Windows (CMD) utilziar el comando: 
```console
.\.venv\Scripts\activate.bat
```

Tras ejecutar el comando, en la parte izquierda de la terminal deberia verse el nombre del entorno virtual que fue activado:

![Imagen entorno activado](./MultimediaREADME/Paso0/EntornoActivado.png)

Al tener el entorno virtual activado en la terminal, todos los paquetes que se instalen desde la terminal unicamente serán almacenados en el entorno virtual, no en la instalación de Python de todo el sistema.

### Paso 0.7: Instalar Streamlit en el entorno virtual

Para instalar Streamlit se debe utilizar el siguiente comando en la terminal que tiene el entorno virtual activado:

```console
pip install streamlit==1.44.1
```

Tras ejecutar el comando empezarán a descargarse e instalarse todas las librerias necesarias para Streamlit. Este proceso puede tardar unos minutos.

## Paso 1: Crear un Hola Mundo en Streamlit.

### Paso 1.1: Crear el archivo _hola_mundo.py_

Las aplicaciones de Streamlit se basan en archivos de Python. Es por ello que lo primero que se debe hacer para crear una aplicación de Streamlit es crear un archivo Python. Para este taller se debe crear un archivo llamado _hola_mundo.py_ dentro de la carpeta del proyecto:

![CreadoArchivoHolaMundo](./MultimediaREADME/Paso1/CreadoArchivoHolaMundo.png)

### Paso 1.2: Agregar el mensaje _Hola Mundo_ a la aplicación

Para que la aplicación muestre el mensaje _Hola Mundo_ se deben escribir las siguientes lineas de código en el archivo _hola_mundo.py_

```python
import streamlit as st

st.write("Hola Mundo")
```

La primera linea del código se encarga de importar la libreria streamlit y permite utilizarla bajo el nombre _st_. La segunda linea utiliza el elemento [st.write()](https://link-url-here.org) de Streamlit. Este elemento permite mostrar en la pantalla de la aplicación el texto que recibe como argumento.

Tras escribir este código se debe guardar el archivo _hola_mundo.py_

### Paso 1.3: Ejecutar la aplicación _hola_mundo.py_

Para ejecutar la aplicación se debe utilizar el siguiente comando en la terminal que tiene activado el entorno virtual:

```console
streamlit run hola_mundo.py
```

Al ejecutar el comando debio abrirse una ventana del navegador en la URL http://localhost:8501 

Dentro de esta ventana deberia verse el mensaje 'Hola Mundo':

![CapturaHolaMundo](./MultimediaREADME/Paso1/CapturaHolaMundo.png)

En la parte superior de la pantalla aparece el boton _Deploy_ y un botón de opciones. Estos [botones](https://docs.streamlit.io/develop/concepts/architecture/app-chrome) son creados automaticamente por Streamlit y tienen funcionalidades más avanzadas que no se van a cubrir en este taller.

Con estos pasos se ha creado un Hola Mundo en Streamlit.

## Paso 2: Crear una aplicación para saludar con un boton.

### Paso 2.1: Agregar un boton a la aplicación.

Para agregar un boton a la aplicación se debe usar el elemento [st.button()](https://docs.streamlit.io/develop/api-reference/widgets/st.button). Este elemento permite dibujar un botón en la pantalla y cada vez que dicho boton sea oprimido la función st.button() retornará el valor True.

Para incluir en la aplicación un botón que muestre el mensaje _Hola Mundo_ al ser presionado se debe modificar el código del archivo _hola_mundo.py_ de la siguiente forma:

```python
import streamlit as st

boton_saludar = st.button("Saludar")

if boton_saludar:
    #Esta parte del código se ejecuta cuando se presiona el boton
    st.write("Hola Mundo")
```

En esta modificación se ha incluido un st.button. El primer argumento del st.button es el texto que se quiere mostrar sobre el botón.

El botón creado se ha asignado a la variable _boton_saludar_. La variable _boton_saludar_ tomará el valor True cuando el botón sea presionado por el usuario, y cuando esto pase se ejecutará el código dentro de la sentencia _if_, lo cual hará que se escriba el mensaje _Hola Mundo_ en la pantalla.

Una vez se han guardado estos cambios en el archivo _hola_mundo.py_ se puede ir nuevamente a la dirección http://localhost:8501 en el navegador.

Al entrar se deberia seguir viendo unicamente el mensaje _Hola Mundo_, esto ocurre debido a que el navegador aún no ha vuelto a ejecutar la aplicación con los ultimos los cambios realizados en el archivo _hola_mundo.py_.

Para que el navegador vuelva a ejecutar la aplicación y refleje los ultimos cambios del código se tienen dos opciones:

1. Oprimir la tecla R dentro del navegador.

2. Ubicar el cursor sobre el logo _i_ que aparece en la esquina superior derecha de la pantalla y luego dar click al boton _Rerun_:

https://github.com/user-attachments/assets/3c6c8a82-aa81-4837-b97a-b40cf16dea6d

Tras esto, en el navegador se ven los ultimos cambios realizados en la aplicación y ahora aparece el botón _Saludar_ en la pantalla. Cuando se oprime el boton se muestra el mensaje _Hola Mundo_:

https://github.com/user-attachments/assets/79f6f154-012d-4daa-966b-42e6cb7f01a1

### Paso 2.2: Agregar un campo de texto para escribir un nombre

Ahora vamos a modificar el código de la aplicación para que se pueda recibir el nombre del usuario y se puede escribir un mensaje saludandolo tras oprimir un boton.

Para esto debemos modificar el código dentro del archivo _hola_mundo.py_ para que se vea de la siguiente manera:

```python
import streamlit as st

nombre_usuario = st.text_input("Escribe tu nombre")

boton_saludar = st.button("Saludar")

if boton_saludar:
    #Esta parte del código se ejecuta cuando se presiona el boton
    st.write(f"Hola {nombre_usuario}")
```

En este caso se ha agregado un elemento de tipo [st.text_input()](https://docs.streamlit.io/develop/api-reference/widgets/st.text_input) al inicio de la aplicación. Este elemento dibuja una caja de texto donde el usuario puede escribir. El primer argumento del st.text_input() corresponde al mensaje que se quiere mostrar en pantalla sobre la caja de texto.

La variable _nombre_usuario_ va a almacenar el texto que se escriba en la caja de texto dibujada por el elemento st.text_input. 

Por otra parte, ahora el mensaje que se escribe en pantalla con st.write va a incluir el _nombre_usuario_ que se haya escrito en la caja de texto.

Para visualizar todos estos elementos se deben guardar los cambios del archivo _hola_mundo.py_ y se debe ir al navegador. Tras dar click al boton _Rerun_ se deberia ver la siguiente interfaz:















