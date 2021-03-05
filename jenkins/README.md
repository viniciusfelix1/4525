# Jenkins

Este diretório armazena os passos e arquivos para a criação da pipeline final do Curso 525 da 4Linux.

## Aplicação PHP
A aplicação foi clonada do repositório `https://github.com/4linux/4542-php`

## Passo a passo

Clonar repositório

```bash
git clone https://github.com/4linux/4542-php.git
cd 4525
git remote rm origin
```

Após termos is arquivos da aplicação, é hora de criar um repositóŕio no [Gitea](http://172.27.11.10:3000) com o nome "php-login" e do tipo privado para simular o máximo um ambiente real.

Após a criação do repositório, é necessário adicionar o repositório remoto no diretório onde fizemos o clone anteriormente. Então voltaremos no terminal.

```bash
git remote add origin git@172.27.11.10:devops/php-login.git
```

Após termos adicionado o repositório remoto, podemos realizar a configuração para ele utilizar automaticamente a chave que incluimos no gitea nas aulas passadas.

> Caso vocẽ não tenha a chave adicionada, crie um par de chaves (`ssh-keygen -m PEM -N '' -f /root/keys/infra-agil`) e adicione a chave privada dentro do gitea e então rode o comando abaixo.

```bash
git config core.sshCommand "ssh -i /root/keys/infra-agil"
```

Depois da adição da chave, podemos commitar para nosso repositório remoto no gitea esses arquivos que serão utilizados pela esteira do Jenkins.

Vamos criar uma nova pipeline, para isso vamos ao dashboard do Jenkins.
- New Item;
- Nome: php-login
- Tipo: Pipeline
- Ok.
- Discard old build: 10 items
- Em Pipeline, selecionar pipeline script from SCM
- SCM: Git
- Repository URL: git@172.27.11.10:devops/php-login.git

Neste ponto, vamos precisar adicionar a chave pública do Jenkins dentro do Gitea. Após termos adicionado a chave, vamos voltar na criação a pipeline.

- Credentials: jenkins
- Script Path: jenkins/Jenkinsfile.groovy
