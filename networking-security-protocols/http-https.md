# Conceitos de HTTP e HTTPS
O Protocolo de transferência de hipertexto seguro (HTTPS) é a versão segura do HTTP, que é o principal protocolo usado para enviar dados entre um navegador web e um site. O HTTPS é criptografado para aumentar a segurança da transferência de dados. Isso é particularmente importante quando usuários transmitem dados sensíveis, como quando fazem login. Todos os sites, especialmente os que requerem credenciais de login, devem usar HTTPS.            

### Como funciona o HTTPS
- O HTTPS usa um protocolo de criptografia para criptografar as comunicações. O protocolo é chamado de Transport Layer Security (TLS), embora anteriormente fosse conhecido como Secure Sockets Layer (SSL). Esse protocolo protege as comunicações usando o que é conhecido como infraestrutura de chave pública assimétrica. Este tipo de sistema de segurança usa duas chaves diferentes para criptografar as comunicações entre duas partes:
    - A chave privada - esta chave é controlada pelo proprietário de um site e é mantida, como o leitor pode imaginar, privada. Essa chave reside em um servidor web e é usada para descriptografar informações criptografadas pela chave pública.
    - A chave pública - esta chave está disponível para todos que desejam interagir com o servidor de forma segura. As informações criptografadas pela chave pública só podem ser descriptografadas pela chave privada.

### Por que o HTTPS é importante.
- O HTTPS evita que os sites tenham suas informações transmitidas de uma maneira que seja facilmente visualizada por qualquer pessoa que esteja espionando na rede.

***Antes da criptografia***
```
Esta é uma sequência de texto que é completamente legível
```

***Depois da criptografia***
```
ITM0IRyiEhVpa6VnKyExMiEgNveroyWBPlgGyfkflYjDaaFf/Kn3bo3OfghBPDWo6AfSHlNtL8N7ITEw
```

### Qual porta o HTTPS usa?
- O HTTPS usa a porta 443. Isso diferencia o HTTPS do HTTP, que usa a porta 80.

### Como usar HTTPS em um site?
- É preciso comprar um certificado na cloud onde você hospeda seu site ou em outra certificadora e importar no seu webserver, loadbalance, cloudfront ou na solução que disponibiliza seu site.
