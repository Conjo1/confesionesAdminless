# DCConfesionesBot

Código usado para el bot de confesiones.

## Desarrollo
Este repositorio maneja su `virtualenv` y dependencias con [`pipenv`](https://github.com/kennethreitz/pipenv).

* Clonar repositorio
* Ejecutar `pipenv install`
* Activar el `virtualenv` con `pipenv shell`
  * Esto carga las variables en tu archivo `.env` local automáticamente
* Desactivar con `exit`

> Más información en la [documentación](http://pipenv.org/) de pipenv.

## Deploy

* `/newbot` al [@BotFather](https://t.me/botfather) para obtener el TOKEN
* Telegram API /setWebhook a la url del bot  
* Se puede hacer gratis en [pythonanywhere](https://www.pythonanywhere.com) (requiere hacer click en un botón cada 3 meses)
  * [A telegram no le gustan los certificados para https como los hace pythonanywhere gratis](https://blog.pythonanywhere.com/148/), así que puede ser necesario usar algo que reenvíe el contenido al bot en pythonanywhere. Un cloudflare worker sirve (también gratis), con algo como el siguiente código (gracias ChatGPT):  
 
 ```javascript  
 addEventListener('fetch', event => {
  event.respondWith(handleRequest(event.request))
})

async function handleRequest(request) {
  const url = new URL(request.url)

  // Replace "example.com" with the target domain
  url.hostname = "example.com"
  url.pathname = "/Bot" // Set the path to "/bot"

  // Create a new request object with the same method, headers, and body as the original request
  const newRequest = new Request(url, {
    method: request.method,
    headers: request.headers,
    body: request.body
  })

  // Forward the request to the target URL and return the response
  const response = await fetch(newRequest)

  return response
}
 ```
