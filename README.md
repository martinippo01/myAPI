# TP1 - HTTP
El siguiente repositorio es un esqueleto basico para la implementeacion de una API utilizando express.js. 

## Prerequisitos
En caso de hace un fork y clonar este repositorio, para poder levantar la API debe primero correr los siguientes comandos
```bash
npm install
node .
```
En caso de querer crear el repositorio desde cero, se debe: (Utilizar las configuraciones default.)
```bash
npm init
```
Luego
```
npm install express
npm install cors
node .
```
Tener cuidado de que el puerto configurado en el archivo index.js no este en uso. En dicho caso, modificar el puerto o terminar el otro proceso que utilice el puerto.

## API
Abrir el archivo index.js.

Para modificar/crear los diversos endpoints de la API, utilizar el siguiente formato:
```javascript
app.get('/path', async (req, res) => {
  try{
    //...
    res.status(200).send({...});
  }catch(e){
    res.status(500).send({'error': 'Internal server error'})
  }
})

app.put('/path', async (req, res) => {
  try{
    //...
    res.status(200).send({...});
  }catch(e){
    res.status(500).send({'error': 'Internal server error'})
  }
})

app.post('/path', async (req, res) => {
  try{
    //...
    res.status(200).send({...});
  }catch(e){
   res.status(500).send({'error': 'Internal server error'}) 
  }
})
```
Donde req hace referencia al request HTTP entrante, donde desde aqui podremos acceder a los headeres y body.
res hace referencia al response HTTP saliente, donde se configurara HTTP status code, headers, body, etc.

Por ejemplo, en el siguiente caso accedemos al body, headers y query params del request entrante. Luego configuramos el body del response saliente junto a un status code.


```javascript
app.get('/players', async (req, res) => {
  try{
    const acceptHeader = req.get('Accept');
    const page = parseInt(req.query.page) || 1; // Default to page 1 if not specified
    const limit = parseInt(req.query.limit) || 10; // Default to 10 items per page if not specified
    //...
    if (acceptHeader !== null && acceptHeader !== undefined && acceptHeader.includes('text/html')) {
      // Return HTML response
      let base_html = `
      <!DOCTYPE html>
      <html lang="en">
        <head>
          <meta charset="UTF-8">
          <meta name="viewport" content="width=device-width, initial-scale=1.0">
          <title>Premier League Players</title>
        </head>
        <body>
          //....
        </body>
      </html>`
      res.status(200).send(base_html);
    } else {
      // Return plain text response
      res.status(200).send({...});
    }    
  }catch(e){
    res.status(500).send({'error': 'Internal server error'})
  }
});
```

## Pagina web
Para modificar el sitio web que se puede ver desde el root de la API, abrir el archivo public/index.html
