# **Mini Proyecto 2: Procesamiento De Lenguaje Natural Usando Transformers**
## **Diseñado por:**
* *Carlos Arbey Mejia Martinez*
    * **Código:** 2210549
* *Andres Felipe Guerra Vargas* 
    * **Código:** 2211058

# **Introducción**
El lenguaje es una herramienta de expresión que nos permite tener relación en nuestra vida social y profesional. Es un medio para transmitir ideas, información, opiniones, sentimientos, entre otras acciones. 

El Procesamiento del Lenguaje Natural o NLP es una disciplina que se encuentra en la intersección de varias ciencias, tales como las ciencias de la computación, la inteligencia artificial y la psicología cognitiva. Su idea central es la de darle a las máquinas la capacidad de leer y comprender los idiomas que hablamos los humanos.

# **Marco Teórico** ##

* **DataSet:** Directorio donde se registró todos los archivos para el proyecto.

* **Natural Language Processing:** La PNL es un campo de la lingüística y el aprendizaje automático centrado en comprender todo lo relacionado con el lenguaje humano. El objetivo de las tareas de PNL, no es solo comprender palabras individuales, sino también poder comprender el contexto de esas palabras, por ejemplo:

  * **Clasificación de oraciones completas:** Obtener el sentimiento de una revisión, detectar si un correo electrónico es spam, determinar si una oración es gramaticalmente correcta o si dos oraciones están relacionadas lógicamente o no.

  * **Clasificar cada palabra en una oración:** Identificar los componentes gramaticales de una oración (sustantivo, verbo, adjetivo) o las identidades nombradas (persona, ubicación, organización).

  * **Generación de contenido de texto:** Completar un mensaje con texto generado automáticamente, completar los espacios en blanco en un texto con palabras enmascaradas.

  * **Extraer una respuesta de un texto:** Dada una pregunta y un contexto, extraer la respuesta a la pregunta en función de la información proporcionada en el contexto.

  * **Generar una nueva oración a partir de un texto de entrada:** Traducir un texto a otro idioma, resumir un texto.


# **Descripción del problema a solucionar (Punto 1)**

Realice un prototipo de aplicación en colab con la API del modelo GPT-3 recientemente liberado por Open AI (https://openai.com/). Algunas
instrucciones de uso en el siguiente video:
https://www.youtube.com/watch?v=C1eOiOkD_8A (La mejor INTELIGENCIA
ARTIFICIAL Generadora de TEXTO (y la puedes USAR) | GPT-3)

**Nuestro problema:**

Nuestro problema o solución será utilizar un modelo preentrenado de **OpenAI**, el cual nos permita dada una información de un cliente o producto, poder generar un anuncio para Instagram, el cual puede utilizar el cliente en su red social.

## **Planteamiento de la solución (Punto 1)**

Inicialmente buscamos el modelo que nos puede ayudar en los ejemplos que ofrece **OpenAI** en su repositorio, el cual se puede encontrar https://beta.openai.com/playground/p/default-ad-product-description?model=davinci-instruct-beta
Este es un modelo **davinci** tipo instruct, el cual dada unas instrucciones iniciales nos genera la salida que necesitamos.

En nuestro caso la instrucción que siempre tendrán nuestras peticiones será:
```python
"Escribe un anuncio creativo para el siguiente producto para que se publique en Instagram:"
```

Para nuestro modelo se debe también establecer una cadena de finalización la cual será:
```python
"\"\"\"\"\"\""
```

Por lo que un ejemplo de nuestra instrucción de llamado a la api de **OpenAI** se verá de la siguiente manera:
```python
response = openai.Completion.create(
  engine="davinci-instruct-beta",
  prompt="Escribe un anuncio creativo para el siguiente producto para que se publique en Instagram:\n\"\"\"\"\"\"\n!Chelitos con mucho amor!, es una empresa que se dedica a la creación de deliciosos pasteles y postres.\n\"\"\"\"\"\"\n""",
  temperature=0.5,
  max_tokens=60,
  top_p=1,
  frequency_penalty=0,
  presence_penalty=0,
  stop=["\"\"\"\"\"\""]
)
```
Como primer paso de nuestra solución, lo que hicimos fue probar el modelo que nos ofrece **OpenAI** en su opción de **playgorund** para validar si el modelo es capaz de solucionar nuestro problema y si es también capaz de soporte nuestro lenguaje **Español**.

<p align="center">
<img src="img/open_1.png" alt="" style="height: 300px; width:400px;"/><img src="img/open_2.png" alt="" style="height: 300px; width:400px;"/>
</p> 

Validada la solución en el sitio de **OpenAI** procedimos a utilizar el código que se nos ofrece, donde implementamos una función python que nos permite utilizar las cadenas de entrada del cliente para así procesarlas y retornar el anuncio. Esta función dinámicamente integra la instrucción respectiva del modelo para que así pueda devolvernos la salida esperada, concatenando al final de la información del cliente nuestro carácter de finalización.

Nuestro modelo fue limitado a un total de 100 tokens dado que el cobro que se realiza se da por cantidad de tokens y modelo seleccionado.

A continuación, se muestra un ejemplo de llamado de nuestro prototipo:
<p align="center">
<img src="img/open_3.png" />
</p> 

## **Resultados (Punto 1)**

Después de implementar nuestro prototipo y generar diferentes iteraciones de este sobre la misma información ingresada, se pudo evidenciar que nos daba diferentes resultados, algunos coherentes, algunos muy originales y también en algunos casos pudimos evidenciar anuncios en el idioma inglés.

A continuación, mostramos diferentes salidas que nos mostró el prototipo por la misma información proporcionada como parámetro:

<p align="center">
<img src="img/open_4.png" />
</p> 

# **Descripción del problema a solucionar (Punto 2)**

Seleccione un data set para una aplicación de PLN o de otra fuente y realice lo siguiente:

* Explique el problema o la aplicación que se va a resolver
* Entrene un modelo basado en Deep Learning para el problema seleccionado. Este modelo puede ser entrenado desde cero o usando un modelo pre-entrenado haciendo uso de transfer learning o fine tuning (puede usar la librería Hugging Face)
* Valide el funcionamiento del modelo obtenido.

## **Planteamiento de la solución (Punto 2)**

* **Problema a Resolver:** Se utilizará la librería **FLAIR** de la empresa **Zalando Research**, para acceder a funcionalidades de procesamiento de lenguaje natural utilizando **HuggingFace ModelHub** en tres ejemplos:

1. Análisis Morfo - Sintáctico: Etiquetador de Lenguaje Universal.

2. Reconocimiento de Identidades: Reconoce un grupo de clases.

3. Análisis de Opinión: Frases si son positivas o negativas.

## **Resultados (Punto 2)**
 ...

# **Conclusiones**

* Después de explorar las diferentes opciones de ejemplos que nos ofrece **OpenAI** con esta liberación de su api GPT3, se puede reafirmar el gran potencial que tienen estos modelos para dar solución a estos problemas como los NLP, en nuestro prototipo utilizamos nuestro lenguaje español y aunque se pudo evidenciar buenos resultados, encontramos que en algunas ocasiones se generaban información sin coherencia o en el idioma inglés, lo que nos puede demostrar que por ahora estos modelos pueden llegar a ser más precisos en el idioma inglés. En la exploración del api se pudo evidenciar una muy interesante **Python to natural language** la cual permite explicar código python en lenguaje natural y no técnico, lamentablemente es una opción privada a aun no liberada que sería interesante explorar en el futuro.

* Al utilizar los mecanismos **NLP**, observamos que, dependiendo de la capacidad de entrenamiento de nuestros modelos, estos se hacen más eficientes cuando se genera un dataset más dinámico y su arquitectura de aprendizaje, contiene más argumentos de valoración y extensión de sus argumentos programados. Depende mucho de la experiencia del profesional encargado de satisfacer los requerimientos del modelo optimo.

* Cuando se utilizan los Embedding, observamos que de manera independiente dan buenos resultados, pero, cuando se manejan de forma binaria con otros embedding, se vuelven modelos muy eficientes, porque aprovechan la virtud de cada uno en el procesamiento de su arquitectura de aprendizaje.

## **Referencias:** ##
* [OpenAI](https://beta.openai.com/overview)
* [Huggingface-upos](https://huggingface.co/flair/upos-multi-fast)
* [Huggingface-ner](https://huggingface.co/flair/ner-english-fast)
* [fasttext](https://fasttext.cc/docs/en/supervised-tutorial.html)
* [flairNLP-tut1](https://github.com/flairNLP/flair/blob/master/resources/docs/TUTORIAL_3_WORD_EMBEDDING.md)
* [flairNLP-tut4](https://github.com/flairNLP/flair/blob/master/resources/docs/TUTORIAL_4_ELMO_BERT_FLAIR_EMBEDDING.md)
* [iaarbook](https://iaarbook.github.io/procesamiento-del-lenguaje-natural/)