### O que é o Git?
É importante perceber só porque é que relevante utilizar Git de todo. Muito simples:
- Eu não quero mandar zips por Discord: é a maneira mais fácil que eu conheço de partilhar código
- Eu não quero perder trabalho, seja de ontem ou de há uma semana
- Se há algo a funcionar, eu quero guardar essa versão, e saber exatamente em que circunstâncias é que funciona ou não
- Isto deixa-nos fazer **desenvolvimento incremental** - vai haver sempre um sítio com coisas a funcionar, e se as coisas deixarem de funcionar, podemos só voltar atrás - e **colaborativo**, em que várias pessoas podem trabalhar no mesmo projeto ao mesmo tempo, o que é crucial neste projeto e em muitos outros

## O que é o GitHub?
- O GitHub e o Git não são a mesma coisa, mas são muito relacionados
- O GitHub é uma **plataforma** colaborativa **online** onde podemos pôr os nossos repositórios Git. Existem outras, como o GitLab, por exemplo
- Pode-se dar clone de repositórios e adicionar chaves ssh, que já vou explicar, e mais coisas como fazer pull requests e abrir issues - issues para o nosso contexto não é muito relevante; pull requests essencialmente são pedidos para fazer merge de um branch para outro (geralmente o main), e são muito úteis para colaboração
- O Git é uma **ferramenta** de controlo de versões (**version control**) que dá track às mudanças que acontecem a ficheiros ao longo do tempo. É software que se instala no nosso PC, em contraste com o GitHub, que é uma plataforma online onde podemos pôr os nossos repositórios Git
- Portanto, o Git é a ferramenta ideal para:
  - Conseguir recuperar se se perder um ficheiro
  - Se se quiser voltar atrás nalguma coisa (está tudo guardado)
  - Se se se quiser ver o que é que mudou

## Conceitos chave
- **Sandbox (Working Directory):** Não é nada mais do que a pasta local onde estamos a trabalhar e editar ficheiros, e os ficheiros e subdiretorias que ela contém
- **Staging Area:** Assim que um ficheiro atinge determinados objetivos, é útil colocá-lo numa **waiting zone** para eventualmente guardar essas alterações permanentemente. A staging area é, então, um armazenamento temporário para as mudanças que queremos guardar no próximo commit
- **Repository**: Assim que efetivamente damos commit aos ficheiros que estavam pendentes na **staging area**, precisamos de algum local para ficarem permanentemente guardados. É isso que é um repositório - eles guardam as alterações permanentes durante o tempo, chamadas **commits**. Podem ser locais ou remotos.
    - **Local Repository**: Os locais encontram-se no nosso PC
    - **Remote Repository**: Os remotos encontram-se num servidor (GitHub, GitLab...)

- **Untracked Files:** São os ficheiros que existem no diretório de trabalho, mas que o Git não está a seguir
- **Tracked Files:** São os ficheiros que existem e estão a ser seguidos pelo Git (adicionados via `git add`)
- **HEAD:** A HEAD é algo que aponta; no caso, aponta para o estado atual do repositório, a minha **posição atual** - se estivermos num branch, aponta para o último commit desse branch, para saber onde adicionar o próximo commit. Podemos pensar nele como uma referência ao commit atual em que estamos a trabalhar (ou seja, o último commit do branch em que estamos) 
- **Commits:** São salvaguardas do estado atual da árvore de ficheiros num dado momento (identificado por um hash)

## Comandos importantes
- Aqui está uma coletânea de comandos que são bastante úteis para começar a usar Git. Pode-se utilizar a interface gráfica que está built-in no VSCode, mas é importante saber os comandos que estão por detrás, porque é o que vai permitir-nos perceber o que é que está a acontecer e resolver problemas

`git add`: Coloca os ficheiros que indicarmos na staging area
`git rm`: Remove ficheiros que adicionámos à staging area
`git status`: Vemos o estado do working directory e da staging area. É boa prática correr este comando antes de fazer um commit das primeiras vezes (e não só, eu costumo fazer muito frequentemente), só para garantir que estamos a adicionar o que queremos
`git commit`: Guarda as mudanças dos ficheiros que estão na staging área no repositório local, e cria um novo commit (com um hash único). Há comandos para alterar commits e reverter commits, mas não vou falar deles por agora, se quiserem saber ou fazê-lo, falem comigo.
  - `git commit -m "mensagem"`: Faz commit com uma mensagem. Por favor, façam commits com mensagens descritivas, é muito importante para perceber o que é que cada commit faz. Há convenções para estas mensagens, podem usá-las e perguntar-me que eu dou um link relevante, mas para já senso comum é suficiente
`git push`: Envia as alterações do nosso repositório local para o repositório remoto
  - Se acabámos de criar um repositório localmente, possivelmente não existe um repositório remoto para enviar as alterações, mas podemos criar um no GitHub e depois fazer push. Se ouvirem o nome **origin**, é o nome que damos ao repositório remoto por defeito - podem pensar nisso como aquilo que está no GitHub
  - Além disso, se acabámos de criar um branch **localmente**, temos de especificar que queremos "fazer push desse branch", com `git push -u origin branchname`. o -u é para dizer, queremos mandar deste branch local para o branch remoto com o mesmo nome

---
  
`git log`: Serve para ver o histórico de commits num branch num dado instante
`git pull`: Faz um fetch e um merge do repositório remoto para o repositório local
  - `git fetch` faz o download das alterações do repositório remoto para o repositório local, mas não faz merge (podem ignorar este, façam `git pull` e lidem com os conflitos como gente crescida)
  - `git pull` faz o download das alterações do repositório remoto para o repositório local e faz merge

Geralmente fazemos só `git pull` e depois se houver conflitos lidamos com eles, mas achei relevante que saibam que há outro comando. Podem ignorar e focar-se no `git pull` por agora

Por fim, para começar um projeto, usamos `git init` se quisermos começar um repositório do zero, numa pasta à nossa escolha, ou `git clone` se quisermos fazer clone de um repositório remoto para o nosso PC.

Há uma série de outros comandos/conceitos que não irei elaborar agora (como **tags**) e um método melhor de fazer merge chamado rebase, mas se tiverem curiosidade ou quiserem saber mais, falem comigo (ou leiam a documentação, apesar de ser horrível de se ler).

## Git Workflow
Uma enorme utilidade do Git é a capacidade de fazer desenvolvimento paralelo. O comando **branch** permite criar um ramo para desenvolvimento paralelo. Este ramo permite fazer experiências que podem, ou não, vir a ser úteis. Várias pessoas podem fazer desenvolvimento paralelo ao mesmo tempo, e o workflow mais comum é o seguinte:
**Main Branch, main (master em antigos):** A linha principal de desenvolvimento. É **crucial** que só vá para o main código que foi **testado** e está a funcionar corretamente e **finalizado**
**Feature Branches:** utilizados para desenvolver funcionalidades isoladas. Cada pessoa que está a trabalhar numa feature cria um branch novo, e quando a feature está pronta, faz um merge para o main.
- `feat/Pedal`
- `test/VESC`

### Comandos importantes para saber
**Criar um branch novo:** git branch branch-name
**Trocar para o branch:** git checkout branch-name
- `git checkout -b branch-name` faz as duas coisas ao mesmo tempo
**Merge de um branch para o main:** git merge branch-name

Geralmente depois de acabarmos uma feature, o que acontece é o seguinte:
- (Estamos no branch feat/X)
`git checkout main: vamos para o branch “main”`

- (Agora estamos no branch main)
`git merge feat/X`: damos merge do branch “feat/X” no branch “main”, ou seja, acrescentamos os commits da nova feature ao main

`git log`: podemos ver que os commits que o branch “feat/X” tinha a mais foram para o main!
Assim que a funcionalidade está pronta, faz-se um **merge** para o main.

- Podem acontecer merge conflicts, que são situações em que o Git não consegue decidir sozinho o que fazer. Nesse caso, é necessário resolver manualmente os conflitos, e depois fazer commit das alterações. Se houverem conflitos, o Git vai dizer-vos que há conflitos e onde estão, e vocês têm de resolver manualmente. Se fizerem `git status` vão ver que há ficheiros com conflitos, e podem abri-los e resolver os conflitos manualmente. Depois de resolverem, têm de fazer `git add` e `git commit` para resolver os conflitos. A parte prática simula um conflito e a sua resolução
