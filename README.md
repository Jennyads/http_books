<h3>HTTP: entendendo a web por baixo dos panos</h3>

Wireshark captura o protocolo de texto e lê o seu conteúdo. Desse modo, é possível observer os dados passados na request. Para resolver, pode introduzir a versão segura do HTTP: o HTTPS.

Para realizar essa modificação, o primeiro passo é gerar uma entidade e uma chave de criptografia para o site. Digitando o seguinte comando no Terminal, na pasta "api-alurabooks":
```
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout server.key -out server.crt
```
Depois é necessário modificar a linha que inicia o servidor:
```
https.createServer({
  key: fs.readFileSync('server.key'),
  cert: fs.readFileSync('server.crt')
}, server).listen(8000, () => {
   console.log("API disponível em https://localhost:8000")
})
```
Existe outro comando baseado no programa OpenSSL capaz de decodificar o conteúdo do certificado: "openssl x509 -in server.crt -text" | openssl rsa -in server.key -text -noout

*Para configurar o HTTP/2 no servidor do nosso frontend, fazemos da seguinte forma.

Primeiro, precisamos do certificado digital e da chave privada (note que nós já geramos esses itens para o backend, mas para o frontend ainda não).
```
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout server.key -out server.crtCOPIAR CÓDIGO
Depois, instalamos o pacote que dá suporte ao HTTP/2 no NodeJS:

npm install spdyCOPIAR CÓDIGO
Agora, geramos uma versão de produção da nossa aplicação React:

npm run buildCOPIAR CÓDIGO
Esse comando vai disponibilizar o nosso frontend pronto para deploy em uma pasta chamada build.

Criamos então o arquivo server_http2.js, que vai servir o nosso frontend com o HTTP/2 usando a biblioteca spdy:

const spdy = require("spdy")
const express = require("express")
const fs = require("fs")

const app = express()

app.use(express.static("build"))

spdy.createServer(
  {
    key: fs.readFileSync("./server.key"),
    cert: fs.readFileSync("./server.crt")
  },
  app
).listen(3002, (err) => {
  if(err){
    throw new Error(err)
  }
  console.log("Listening on port 3002")
})
```
