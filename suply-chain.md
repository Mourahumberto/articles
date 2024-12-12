## Software suply chain
- em sumo é a cadeia de dependências de nossas apps

## O que são CVEs?
- Common vulnerabilities and Exposures
- existem alguns frameworks de vulnerabilidades, CVSS framework.
- CVE scanners: grype e trivy, podem ser usados para detectar pacotes.
- imagem base importante, alpine, wolfi,chainguard
- wolfi é um "mini linux" baseado no apk do alpine
- essas imagens minimalistas só irão rodar a aplicação, você precisará fazer multi staging build e ter uma imagem que build o projeto.
- usar usuário na imagem sem muitos privilégios.
- usar o .dockerignore para ignorar arquivos sensíveis ou algo do tipo.