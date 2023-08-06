<h3>HTTP: entendendo a web por baixo dos panos</h3>

Wireshark captura o protocolo de texto e lê o seu conteúdo. Desse modo, é possível observer os dados passados na request. Para resolver, pode introduzir a versão segura do HTTP: o HTTPS.

Para realizar essa modificação, o primeiro passo é gerar uma entidade e uma chave de criptografia para o site. Digitando o seguinte comando no Terminal, na pasta "api-alurabooks":
```
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout server.key -out server.crt
```
