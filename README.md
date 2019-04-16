# How to use Git with Git Flow
### Utilizando o Git
1. Inicialmente iremos trabalhar com o Git localmente;
* Para baixar o GitBash clique [aqui](https://git-scm.com/downloads).
2. Configure os dados para identificação do usuário;
````
git config --global user.name "Seu Nome"
git config --global user.email "seu@email"
````
3. Crie um diretório de trabalho (Working directory);
````
mkdir meuProjeto
````
* Caminhe pra o diretório criado
````
cd meuProjeto
````
4. Inice o Git no diretório do projeto (criação do Git directory, oculto .git);
````
git init
````
5. Crie um arquivo fonte no diretório do projeto
* Calculo.java	(com um cálculo de fatorial sem uso de recursão);
	* **Linux:** `touch Calculo.java` 
	* **Windows:** `notepad Calculo.java`
>Isso varia de acordo com o editor de texto do sistema operacional. 
6. Consulte o estado dos arquivos do projeto;
````
git status
````
> Observe que o novo arquivo está marcado como Untracked
7. Leve o arquivo para a área de preparação;
````
git add Calculo.java
````
> Consulte novamente estado dos arquivos.
> Observe que o mesmo encontra-se "to be committed".
8. Leve o arquivo para o estado committed, ou seja, confirmado no Git directory;
````
git commit -m "comentário do commit aqui"
````
> Por exemplo: `git commit -m "Criação da classe de Cálculos."`
> Observe o **SHA1**, na verdade seus 7 primeiros dígitos: **identificador do commit**
9. Para renomear ou remover um arquivo que está versionado você deverá utilizar o git na operação:
	* Para renomear: `git mv -f nome-arquivo-original novo-nome-arquivo`
	* Para  remover: `git rm nome-arquivo`
10. Modifique o arquivo Calculo.java, colocando um comentário, por exemplo;
11. Adicione o arquivo de interface texto CalculoTui.java;
* Implemente esta classe com o _System.out.println();_ do resultado do método.
> Consulte o status do arquivo e observe os estados dos arquivos.
12. Verifique a diferença entre os arquivos versionados (comparação com a última versão):
````
git diff
````
13. Leve os arquivos para a área de stage;
* Este passo pode ser feito de duas formas: 
 `git add Calculo.java` e depois `git add CalculoTui.java`
  Ou só `git add .`
> Na segunda forma o **ponto** após o **add** diz para levar todos os arquivos do diretório para **área de stage**.
> Não recomendado para diretórios com arquivos indesejáveis (veremos a frente isso) e diretórios com muitos arquivos.
14.  Commite os arquivos;
````
git commit -m "mensagem descritiva"
````
15. Veja o histórico de commits;
````
git log
git log --oneline
````
> O segundo simplifica as informações que aparecerão no log.
16. É possível comparar as verões entre mais de uma versão;
````
git diff HEAD@{2} HEAD@{0}
````
> O **HEAD** é a posição da pilha que se encontra o commit.
> Lembre-se da definição de pilhas para  entender a funcionalidade do comando.
* Para saber apenas os dos arquivos, utilize a opção --name-only
````
git diff HEAD@{2} HEAD@{0} --name-only
````

17. Para saber os commits associados aos HEAD@{ };
````
git reflog
````

18. Você pode desistir das mudanças feitas num arquivo
* Modifique aleatoriamete a classe Calculo.java;
* Desfaça a modificação
````
git checkout Calculo.java
````
* Verifique que a modificação do arquivo foi desfeita

19. Compile o arquivo. A depender do projeto, certos tipos de arquivo não devem ser versionados, por exemplo, **.class**;
	* Para informar ao git que você não deseja ter que controlar determinados tipos de arquivos, utilize o **.gitignore**

20. Crie o arquivo .gitignore;
	* O arquivo **.gitignore** geralmente também é versionado;
	* Você pode fazer essa criação de duas formas:
	`touch .gitignore` -> Cria o arquivo
````
*.class
*.jar
*.zip
...
````
	* Ou você pode utilizar a ferramenta [gitignore.io](https://www.gitignore.io/). Apenas dizendo SO, Linguagem ou IDE que deseja ignorar os arquivos.
	>Adicione o arquivo em stage e commite!
	
21. Verifique quem fez o que e quando em dado arquivo;
````
git blame Calculo.java
````

#### Trabalhando com branches (ramificações)
	- Manutenção evolutiva
	- Experimentação
	- Correção de bug
	
22. Liste os branches existentes
````
git branch -a
````

23. Crie uma branch;
````
git branch funcionalidade1
````
> Liste novamente as branches
24. Mude para o novo branch;

````
git checkout funcionalidade1
````
> Observe que o branch não nasce vazio

25. Atualize o projeto, substituindo o código do cálculo do fatorial para que o mesmo seja recursivo;

26. Adicione um arquivo **README.md**;
	* Este arquivo normalmente é composto pelo menos com a descrição do projeto, mas você pode sempre complementar ele com novas informações e tópicos.
	>Neste no _how to_ deste projeto não foi criado o arquivo pois este arquivo escrito é o nosso README.md.
	>Mas no seu exercício, não pule este passo!
	>O README é escrito com a sintaxe do [Markdown](https://www.markdownguide.org/).
	
27. Faça o commit da modificação e do novo arquivo;
````
git add Calculo.java
git add README.md
git commit -m "mensagem curta e descritiva"
````
* Verifique o histórico de commits

28. Volte para o master _(checkout)_ e verifique como ficaram os arquivos _(o conteúdo deles)_;
	* Volte para o funcionalidade1 e verifique como ficaram os arquivos
	* Verifique a diferenças entre os branches, origem funcionalidade1 e destino em master _(diff)_.
##### Dando Merge

29. Leve as mudanças feitas na funcionalidade1 para o master;
````
git merge funcionalidade1
````
> Lembre de dar checkout para o master antes do merge.
> Se for dar merge de uma branch para a outra, esteja na que receberá o merge.
* Mas para garantir origem e destino pode usar esta sintaxe:
````
git merge origin/destination -> sintaxe
git  merge funcionalidade1 master
````
* Verifique o histórico após o merge.
````
git log
git log --oneline
git reflog
````
##### Voltando no tempo🕒
30. Volte para um ponto arbitrário do tempo;
````
git checkout HEAD@{5}
````
> Caso você deseje fazer commits neste ponto, crie um branch `git checkout -b nome-branch`
* Volte para o master
31. Crie o ramo para a funcionalidade2;
* Implemente tratamento de entrada de dados para não permitir números negativos.
 > Adicione para _**stage**_ e _**commite**_ as alterações. 
 
32. Crie o ramo para a funcionalidade3;
* Novo calculo para números primos.
 > Adicione para _**stage**_ e _**commite**_ as alterações. 
* Verifique como os branches se relacionam;
````
git log --graph --online --decorate --date=relative --all
````
> Neste comando, é exibido um gráfico da árvore de commits e branches na linha de comando.

33. Após as duas alterações faça o merge das mesmas para o master;
	* **LEMBRE-SE DE VOLTAR PARA O MASTER!**
	* OU UTILIZAR **origin/master**
	* Verifique como os branches se relacionam
	##### Conflitos 💥
	* Nesta etapa vamos demonstrar quando e como ocorrem conflitos durante o processo de versionamento.
34. Crie o branch funcionalidade4
	* Altere o arquivo CalculoTui.java e altere a mensagem de entrada de dados.
 	> Adicione ao stage e Commite o arquivo
 35. Crie o branch funcionalidade5
 	* Altere o arquivo CalculoTui.java e altere, de uma forma diferente, a mensagem de entrada de dados.
 	> Adicione ao stage e Commite o arquivo
 36. Faça o merge das _branches_ **funcionalidade4** e **funcionalidade5** para o _master_;
 	* Verifique o retorno do git e o conteúdo do arquivo CalculoTui.java
 	> O arquivo CalculoTui.java mostrará onde há o conflito, para resolver o conflito basta escolher qual das modificações será a definitiva.
 37. Remova os branches que não são mais necessários
 ````
git branch -d funcionalidade1
git branch -d funcionalidade2
git branch -d funcionalidade3 
````

#### Adicionando repositório remoto
* Observe que tudo foi feito localmente e os dados ficaram armazenado apenas nas máquinas locais;
* Crie uma conta no [GitHub](https://github.com/login)/[GitLab](https://gitlab.com/users/sign_in).
> Remova os arquivos da área de **stage** 
````
git rm --cached nome-do-arquiv
````
38. Adicione seu projeto a um repositório remoto;
````
git remote -> listar os repositórios remotos existentes
git remote add [nomecurto] [url] 
ex: git remote add origin https://github.com/cezargfilho/how-to-use-git-flow.git
````
39. Suba seu projeto para o repositório remoto;
````
 git push [nome-remoto] [branch]
 ex: git push -u origin master
 ````
> Lembre que neste caso a master é a branch que eu quero subir para o repositório.
> A depender de qual branch eu estrou trabalhando, nem sempre eu irei subir a master.
40. Referências:
> Lembrando que este roteiro foi idealizado pelo meu professor Antonio Claudio Neiva e que fiz apenas pequenas adaptações;
* [Documentação Git](https://git-scm.com/doc)
* [Livro do Git (Grátis) - Git Book/EN](https://git-scm.com/book/en/v2)
* [GIT CHEAT SHEET](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)