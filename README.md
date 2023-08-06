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
