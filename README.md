## Consumo de una API

# Cocktail API<br>

<p align="center"> 
  <img src="https://github.com/FranSSZZ/apiCocktail/blob/main/img/logo.png" width="200" height="30">
</p><br>

### Contenido<br>

* Proceso para encontrar una API funcional.
* Sobre la API.
* Uso.
* HTML.
* JAVASCRIPT.
* Resultado.
---

### Proceso para encontrar una API funcional<br>

Para encontrar una API que pudiera utilizar en el ejercicio de [Consumo de una API](https://simplonline.co/briefs/c388b174-6780-4dbf-be9a-b2d0e0912a1d) fue necesario revisar las opciones de un par de listas [Public APIs](https://github.com/public-apis/public-apis) y [API list](https://apilist.fun/), en ambos casos con muchísimos enlaces muy diferentes, a partir de aquí comenzó el proceso de descarte, revise tres APIs buscando aquella que me permitiera ver el el contenido y que el enlace no requiriera una "KEY", pago o alguna configuración maligna para funciona, y sobretodo, lo más importante que tuviera una documentación que pudiera entender y la posibilidad de un vídeo tutorial. Las tres primeras no cumplieron con los dos primeros criterios (y ya no digo con el resto porque todo muy terrible). Luego de investigar en algunos chats, documentación y sugerencias de personas 

### Sobre la API<br>

La **API Cocktail** es una base de datos abierta de bebidas y cócteles de todo el mundo. Ofrece una API JSON gratuita de acceso libre. 
Tiene un sistema de contribución de pequeños aportes que da acceso a una API más amplia y con más detalles.<br><br>
Para más detalle de la API y el método pueden consultar [TheCocktailDB](https://www.thecocktaildb.com/). <br><br>

### Uso<br>

En cuanto a su uso, la API tiene opciones de enlaces/métodos con diferentes tipos de búsquedas. Tiene un conjunto de enlaces de acceso libre con una "KEY" pública y tiene una opción de contribución con un fee de 2$ para acceder a enlaces y métodos más completos y detallados. Pueden ver la lista en [TheCocktailDB](https://www.thecocktaildb.com/api.php). Para el ejercicio use el método que me permite hacer una búsqueda por nombre de cóctel en este caso [Search cocktail by name](www.thecocktaildb.com/api/json/v1/1/search.php?s=). En un próximo sprint quisiera agregar un filtro que permita agregar otras opciones de búsqueda: letra, ingrediente, una opción random. Así se ve el APIs [Search cocktail by name](www.thecocktaildb.com/api/json/v1/1/search.php?s=):

<p align="center"> 
  <img src="https://github.com/FranSSZZ/apiCocktail/blob/main/img/metodoApi.png" width="650" height="400">
</p><br><br>

<p align="center"> 
  <img src="https://github.com/FranSSZZ/apiCocktail/blob/main/img/metodoApi2.png" width="650" height="400">
</p><br><br>

### HTML<br>

El HTML contiene:<br>

    <div class="container">
        <div class="search-container">
            <input type="text" placeholder="Escribe un nombre de cóctel..." id="user-inp" value="">
            <button id="search-btn">Buscar</button>
        </div>
        <div id="result"></div>
    </div>

    <script src="script.js"></script>

* Una Clase "container" que alberga toda la tarjeta donde se hace la busca y se muestran los datos de los cócteles.<br><br>
* Una Clase "search-container" que incluye un <input> para la búsqueda por el id "user-inp" y con un mensaje para el usuario "Escribe un nombre de cóctel...". Y un <button> con id "search-btn" que será declarada como una variable que iniciará una búsqueda usando el enlace de la API y el contenido de los Array.<br><br>
* Un id "result" que hace referencia a un elemento en la página web donde se mostrará el resultado de la búsqueda de información sobre cócteles.<br><br>
 
<p align="center"> 
  <img src="https://github.com/FranSSZZ/apiCocktail/blob/main/img/html.jpeg" width="700" height="400">
</p><br>

### JAVASCRIPT<br>

Sobre el JAVASCRIPT:<br>
  
<p align="center"> 
  <img src="https://github.com/FranSSZZ/apiCocktail/blob/main/img/js3.jpeg" width="450" height="400">
</p><br>

En las primeras líneas de código se declaran tres variables utilizando **`let`**:

- **`result`**: el resultado de la búsqueda se mostrará en este elemento HTML, que tiene el ID "result".
- **`searchBtn`**: se refiere al botón de búsqueda, que tiene el ID "search-btn". **Que está definido en el html.**
- **`url`**: **es la URL de la API** de [TheCocktailDB](https://www.thecocktaildb.com/) que se utilizará para buscar información sobre bebidas alcohólicas. Contiene el detalle de 31 cocteles.

Define **`getInfo`** utilizando una función flecha (**`=>`**). Esta función se encarga de buscar y mostrar información sobre una bebida en particular. Se almacena en una variable llamada **`userInp`**. Que está definida como id de input en el HTML, es un área de entrada (en este caso es una barra de búsqueda que revisa los array usando el nombre de las bebidas).

Verifica si el valor de **`userInp`** es cero. Si es así, muestra un mensaje de error en **`result`**, mostrando que el campo de entrada no puede estar vacío.

Si **`userInp`** no está vacío, se realiza una solicitud **`fetch`** a la URL de la API con el valor de **`userInp`** como parámetro de búsqueda. Si la solicitud es exitosa, la información de la bebida se convierte en formato JSON y se muestra en la página utilizando diferentes elementos HTML. Si la solicitud no es exitosa, se muestra un mensaje de error en **`result`**. 

La función **`fetch(url + userInp)`** realiza una solicitud HTTP GET a la URL especificada en la variable **`url`** junto con el valor ingresado por el usuario en el campo de entrada. La respuesta a la solicitud HTTP se pasa como argumento a la primera función **`.then()`**. La función **`.then((response) => response.json())`** convierte la respuesta de la solicitud HTTP en un objeto JSON que se puede usar en JavaScript. La función **`.json()`** llama al objeto **`response`** como argumento y devuelve una promesa con un objeto JSON.

La segunda función **`.then((data) => {...}`**) recibe el objeto JSON que se ha convertido en el primer **`.then()`**. Dentro de esta función, revisa los datos del objeto JSON para extraer la información relevante sobre la bebida buscada y la muestra en la página.
  
Con los **`console.log`** se imprime: el nombre del cóctel **`(myDrink.strDrink)`**, la imagen **`(myDrink.strDrinkThumb)`** a partir de la URL que proporciona la API y las instrucciones para preparar el cóctel **`(myDrink.strInstructions)`**. Esto es útil para verificar que la información correcta y que se imprime en la pantalla.

Si la solicitud HTTP no se puede completar por alguna razón, la función **`.catch()`** captura el error que se produzca y muestra un mensaje en la página.

Al final se agregan dos eventos de escucha al objeto **`window`** y al objeto **`searchBtn`** utilizando el método **`addEventListener().`** El evento de carga **`load`** se utiliza para llamar a la función **`getInfo`** cuando se carga la página. El evento de clic **`click`** se utiliza para llamar a **`getInfo`** cuando el usuario hace clic en el botón de búsqueda.<br><br>

### RESULTADO<br>

<p align="center"> 
  <img src="https://github.com/FranSSZZ/apiCocktail/blob/main/img/web1.jpeg" width="650" height="400">
</p><br><br>
  
<p align="center"> 
  <img src="https://github.com/FranSSZZ/apiCocktail/blob/main/img/web2.jpeg" width="650" height="400">
</p><br><br>

### Más...<br><br>
  
Comparto un enlace a Notion con un cuaderno de notas sobre [APIs](https://www.notion.so/APIs-843f9ea9c25d4f6bbaa4c06e4d5c7e6d?pvs=4) y el uso de esta en particular [Cocktail API](https://www.notion.so/APIs-843f9ea9c25d4f6bbaa4c06e4d5c7e6d?pvs=4), ambos los iré actualizando para mi uso y como referencia para la persona que lo necesite.
