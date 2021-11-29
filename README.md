# **Mini Proyecto 2: Procesamiento De Lenguaje Natural Usando Transformers**
## **Diseñado por:**
* *Carlos Arbey Mejia Martinez*
    * **Código:** 2210549
* *Andres Felipe Guerra Vargas* 
    * **Código:** 2211058

# **Introducción**

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

En nuestro caso la instrucción que siempre tendran nuestras peticiones será:
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

Validada la solución en el sitio de **OpenAI** procedimos a utilizar el código que se nos ofrece, donde implementamos una función python que nos permite utilizar las cadenas de entrada del cliente para así procesarlas y retornar el anuncion. Esta funcion dinámicamente integra la instrucción respectiva del modelo para que así pueda devolvernos la salida esperada, concatenando al final de la información del cliente nuestro caracter de finalización.

Nuestro modelo fue limitado a un total de 100 tokens dado que el cobro que se realiza se da por cantidad de tokens y modelo seleccionado.

A continuación se muestra un ejemplo de llamado de nuestro prototipo:
<p align="center">
<img src="img/open_3.png" />
</p> 

## **Resultados (Punto 1)**

Despues de implementar nuestro prototipo y generar diferentes iteraciones de este sobre la misma información ingresada, se pudo evidenciar que nos daba diferentes resultados, algunos coherentes, algunos muy originales y también en algunos casos pudimos evidenciar anuncios en el idioma ingles.

A continuación mostramos diferentes salidas que nos mostro el prototipo por la misma información proporcionada como parámetro:
<p align="center">
<img src="img/open_4.png" />
</p> 

## **Referencias:** ##
* [OpenAI](https://beta.openai.com/overview)