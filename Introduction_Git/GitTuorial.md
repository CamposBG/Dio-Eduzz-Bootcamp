# GitHub e Git

## git

##### CLI (command line interface)

### comandos básicos do terminal (bash)

- ```ls``` - listar + flags  

- ```cd / ```- mudar diretório root  

- ```cd ..``` - retrocede um nível de navegação  

- ``` clear ```- limpa tela (ou Ctrl + L)  

- ```mkdir nome-da-pasta``` - cria uma pasta  

- ```touch arquivo.extencao``` - cria um arquivo  

- ```echo nome-do-arquivo > nome-do-arquivo.extencao``` - também cria uma um arquivo  
  -``` rm -rf``` - rm para remover flags "r" pois fará isso recursivamente (entra em subpastas) flag "f" é de force, para forçar essa remoção e não me perguntar nada.  

### instalando git

#### Windows

[Site oficial do git](https://git-scm.com/)  
Durante a instalação na parte de "Select Components" conferir se as opções estão **marcadas** :  

- Git Bash Here  
- Git GUI Here  

Durante a instalação na parte "Choosing the default editor used by Git":  

- uma boa opção é deixar o vim mesmo. Eventualmente o git vai te mandar responder ou interagir de alguma forma usando esse editor de texto.  

Na tela "Adjusting the name of the initial branch in new repositories":  

- Ao se criar um repositório no git ele cria a branch padrão e principal como a ***main***. Antigamente essa branch principal era a "master". Como muitos lugares ainda nao se atualizaram é melhor deixar o git escolher. Então selecionar a opção:  
- Let git decide  

Na tela "Adjusting your PATH environment"  

- (recommended) Git from the command line and also from 3rf-party software  

Na tela "Choosing the SSH executable"  

- Use boundled OpenSSH  

Na tela "Choosing HTTOS transporter backend"  

- Use the OpenSSL Library  
- Na tela "Configuring the line ending conversions" ele pergunta sobre as quebras de linha  
- Se usar Windows escolher ***windows style***  
- Se usar linux ou mac escolher ***Unix style***  

Vai dando next até chegar na tela "***Choose a credential helper***"  

- Selecionar ***Git credential Manager Core***  

depois dar next e prosseguir com a instalação padrão.  

#### [Linux](https://git-scm.com/download/linux)

- fazer download para a distribuição que usa

### Como funciona o git

#### SHA1

Algorítimo de encriptação que gera um conjunto de 40 dígitos de caracteres únicos. Git usa o SHA1 para representar o estado de uma arquivo e para identificar os arquivos e para identificar se eles sofreram modificação.
O git tbm roda o SHA1 para objetos internos do git

#### Objetos internos do git

- Blobs
  
  - Os arquivos no git ficam guardados dentro de objetos chamados blobs. E esse objeto contem metadados dentro deles (tipo,  tamanho, \0 conteúdo do arquivo) --> estrutura básica de um blob. Ex: ``"blob 90\conteudo"``
    - o Git armazena o arquivo que vc quer + os metadados relacionados a ele, então o SHA1 é gerado a partir disso
    - não contem o nome do arquivo, apenas seu conteúdo
    - possuem o SHA1 do arquivo

- Trees
  
  - Armazenam e apontam para blobs diferentes. também tem metadados 
  - Responsável por montar toda a estrutura de onde estão localizados os arquivos
  - Podem apontar para outras arvores (Um objeto recursivo)
  - estrutura de uma arvore:
    - ``Tree <tamanho> bloob sa4d9s texto.txt``
    - Tem um SHA1 dos metadados da Arvore (tree), logo se mudar alguma coisa em algum arquivo dessa arvore o SHA1 vai mudar e o Git vai ter esse controle. 
      ![image info](https://git-scm.com/book/en/v2/images/data-model-1.png)

- Commits 
  
  - aponta para uma arvore, para um parente (último commit realizado antes dele), para um autor, e aponta para uma mensagem
  - commits tbm possuem SHA1 dos seus metadados (ou seja se vc alterara uma bloob, é alterado o SHA1 do próprio blob, da arvore e do commit)
    - Dessa forma vc monta uma linha do tempo, das alterações
    - indica q não teve interferência de outras pessoas (o histórico de commits aponta para o usuário)
      ![image info](https://git-scm.com/book/en/v2/images/data-model-3.png)

### Chaves SSH e Tokens

 Quando vc joga seu código para o gitHub vc tem que se autenticar.

#### Chave SSH

 Uma forma de estabelecer uma conexão segura e encriptada entre dua maquinas, através de chaves, uma publica e uma privada. Vamos pegar a chave ***publica*** e colocar ela no github. A partir dai o github vai conhecer nossa máquina, a assinatura da nossa máquina. 

##### 1) comandos para se criar uma chave SSH  [documentação](https://docs.github.com/pt/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

```shell
$ ssh-keygen -t ed25519 -C "your_email@example.com"
```

2) Ele responde falando os locais em que as chaves vão ficar e vc da um Enter para confirmar o local que ele automaticamente escolheu

3) Após isso ele pede uma senha, e vc entra com uma senha. 

E ele gera a chave publica e privada. 

4) Então vc deve navegar até a pasta .ssh onde foram criadas as chaves e com o comando `` cat nomde-chave.pub`` você acessa o conteúdo e copia essa chave para colocar lá no git-hub (normalmente o nome da chave é "id_ed25519.pub"

5) No CLI  agora temos que iniciar o SSH agent, que vai ficar responsável por pegar as chaves e lidar com elas. digitar o seguite comando:
   
   ```shell
   $ eval $(ssh-agent -s)
   ```

6) agora temos que entregar nossas chaves ***privada*** ao agente digitando ssh-add mais o caminho onde a chave está.Se vc tiver dentro da pasta .ssh pode passar direto, se não tem q passar o caminho. 
   
   ```shell
   $ ssh-add ~/.ssh/id_ed25519
   ```
   
   em seguida ele pede a senha e adiciona a identidade ao agent

### Token de acesso pessoal

Uma outra forma de validar a comunicação que toda hora tem q dar o token... nao é tão prática. 

## Comandos básicos do git

```
git init
git add
git commit
```

na pagina onde vc quer começar sua aplicação digitar:
``git init``
então o git cria um repositório vasio com o nome da pasta e fala que esse repo é main 

> ps: Na primeira vez que vc usar o git ele vai pedir um username e um email, para ele associar um autor aos commits, para isso tem que rodar o seguinte comando:

```shell
git config --global user.email "email@gmail.com"
git config --global user.name nomeDoUser
```

###### git init

Esse comando cria um repositorio no diretório que estamos 

![image info](https://git-scm.com/book/en/v2/images/lifecycle.png)

- untraked sao os arquivos que o git ainda não tem ciência 

- Staged - arquivos preparados para ser commitados 

*git add* muda os arquivos untracked para **staged**, se o arquivo já estava assistido pelo git , no momento em que vc modifica ele, ele ve oq teve modificação (pelo sha1) e vai para modified, e se ele já estava modified ele vai para staged ao se dar add

O comit tira um snapshot do arquivo/codigo e das modificações que foram feitas no commit e volta o artigo para unmodified 

###### O Git é um sistema distribuido, no servidor tem o gitHub e em nossas maquinas tem a versão de desenvolvimento que é o git.

O ambiente de desenvolvimento é comporto por:

- Working directory

- Staging Area (area de staging)

- Local repository (após o comit o arquivo integra o repositorio local) que daqui pode ser dado o push para o repositorio remoto

## Para ver e mudar algumas configurações do GIT

``git config --list``  lista as configurações do git

Para mudar alguma coisa tipo o email:

`git config --global --unset user.email ` aqui ele removeu o seu email

AI você tem q criar de novo o email coloando o novo:

`git config --global user.email "email@gmail.com"`

Para linkar seu repositoro local para o github e dar push

1. Criar o repositório no Github

2. copiar o caminho do seu repositório (URL)

3. Dentro da pasta onde está seu repositorio local digite:
   
   1. apontar o repositorio local para o remoto, para isso temos que add a origem:
   
   2. ``git remote add origin git@github.com:CamposBG/Git_teste.git``
   
   3. `Para checar a lista de repositórios remotos cadrastados:
   
   4. `git remote -v`
   
   5. Agora temos q mudar para a branch main (defoult no gitHub) e damos push do repositorio local para o remoto

```bash
git branch -M main
git push -u origin main
```

### Para pegar a versão do repositorio remoto para o local:

`git pull`

Se as duas versões conter alterações vai ocorrer um conflito de Marge
