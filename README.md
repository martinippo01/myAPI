# TP1 - HTTP
El siguiente repositorio es un esqueleto basico para la implementeacion de una API utilizando express.js. 

## Instalar
Previamente, se necesitaran los siguiente programas para el desarrollo del TP
- Visual Studio Code (O cualquier otro editor de codigo)
- Postman
- Node.js
- Git
  
La instalacion de cada uno de estos (sobre todo Node.js y Git) dependen del Sistema Operativo. Consultar
al docente en caso de duda.

## Prerequisitos
En caso de hace un fork y clonar este repositorio, para poder levantar la API debe primero correr los siguientes comandos
```bash
npm install
```
En caso de querer crear el repositorio desde cero, se debe: (Utilizar las configuraciones default.)
```bash
npm init
```
Luego
```
npm install express
npm install cors
npm install body-parser
```
Tener cuidado de que el puerto configurado en el archivo index.js no este en uso. En dicho caso, modificar el puerto o terminar el otro proceso que utilice el puerto.

Asegurarse tener el archivo .gitconfig con lo siguiente:
```
# Dependency directories
node_modules/

# OS-specific files
.DS_Store
Thumbs.db

# Environment variables file
.env

# Log files
logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Editor files
.vscode/
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw*

# IDE folders
.idea/
```

En caso de no poder realizar commits desde Visual Studio Code, abrir la terminal y ejecutar los siguientes comandos, remplazando el mail y usuario por los de su cuenta de GitHub:
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## Ejecutar la API
Para ejecutar la API, luego de haber cumplido los requisitos, se hace simplemente con el comando:
```bash
node .
```

## Modificar la API
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
