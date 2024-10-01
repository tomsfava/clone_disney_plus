# Modulo 21 - Projeto 4
## Notas
### Aula 1 - Inicie o projeto
#### **Sobre a aula**
* compreender a estrutura do projeto;
* configurar um abiente de desenvolvimento;
* iniciar o controle de versão e colaboração
#### **Anotações**
O projeto é uma landing page, será um clone do site da Disney+;  
Uma página relativamente simples, vamos utilizar HTML, CSS e Javascript (para uma seção com abas e outra com accordions);  
não seguiremos a risca o HTML do site da Disney+ já que tem algumas práticas que o professor considera que não fazem muito sentido, como a criação de div vazias para espaçamento e o excesso de uso da tag br;  
nesse projeto vamos utilizar o gulp para compilação do sass e para minificação das imagens;  
podemos rodar instalações subsequentes com o comando npm i --save-dev, assim sendo rodamos npm i --save-dev gulp gulp-sass sass;  
assim no gulpfile.js vamos importar primeiro o gulp com **const** gulp = require('gulp'); depois o sass com **const** sass = require('gulp-sass')(require('sass'));  
em seguida vamos programar a função styles que vai ter como retorno gulp.src('./src/styles/*.scss').pipe(sass({outputStyle:'compressed})).pipe(gulp.dest('./dist/styles'));  
essa função encadeia através do pipe, 3 tarefas, primeiro com gulp.src selecionamos os arquivos fonte, em seguida com sass({outputStyle: 'compressed'}), compilamos o sass de forma comprimida e por fim com gulp.dest definimos a pasta de destino da compilação;  
para definir uma tarefa como default no gulp utilizamos a semântica exports.default = tarefa; essa tarefa precisa ter sido definida como função anteriormente, no caso usamos a tarefa styles;  
em seguida definimos também a tarefa watch através de exports.watch = function() {
    gulp.watch('./src/styles/*.scss', gulp.parallel(styles));
};  
a função gulp.watch recebe dois argumentos, o diretório a ser observado e a função que vai rodar caso aconteça alguma mudança, importante notar que essa função precisa ser chamada dentro de gulp.parallel() ou dentro de gulp.series(), não podendo ser chamada dentro de uma array com simplesmente o nome da tarefa;  
depois de configurado o sass e o watch, criamos o arquivo index.html definimos sua linguagem para pt-br damos um título e linkamos main.css dentro da pasta dist;  
nesse projeto estaremos realizando o versionamento, ou seja a cada aula vamos subir nosso progresso para o repositório no github;
a mensagem do primeiro commit será 'setup do projeto';
### Aula 2 - Crie o hero
#### **Sobre a aula**
* compreender a estrutura de um componente HTML;
* dominar o uso de classes e estilos CSS;
* praticar a criação de seletores CSS avançados.
#### **Anotações**
Vamos fazer uma estilização diferente, vamos criar componentes no CSS;  
mas a primeira coisa que vamos fazer é configurar o gulp para que ele minifique as imagens, primeiro instalamos o gulp-imagemin na versão 7.1.0, depois fazemos o downgrade do gulp para a versão 4.0.2, dai importamos o imagemin criando a **const** imagemin e criamos a função images que segue a lógica gulp.src().pipe(imagemin()).pipe(gulp.dest);  
feito isso extraímos a cor de fundo do site da Disney+ e criamos a variável no scss corDeFundo;  
em seguida analisamos os font-sizes para poder componentezar os elementos, dessa forma notamos que todo texto tem o line-height 10px maior que font-size, então criamos um mixin para isso (text);  
dai críamos um segundo mixin para title que inclui o mixin text mas altera a cor para corTextoSecundaria;  
por fim criamos as classes text e text--variações e title e title--variações (small e big), cada uma delas vai incluir o mixin com o tamanho da fonte como parametro;  
agora vamos ligar o watch com o script que configuramos no package.json, npm run dev;  
vamos agora criar o hero, um hero é um banner, sempre que a gente tem uma imagem de fundo com uma chamada com texto e botões, é um hero;  
criamos um arquivo adicional dentro de styles com o nome _hero.scss, dentro dele estilizamos a classe hero para ter o padding de 5.6vw, o min-height: 80vh e o background-image com url apontando para a imagem adequada;  
o do professor ficou bem configurado, o meu cortou a imagem;  
em seguida criamos a seção .hero, dentro dela uma div .hero__content que contem um h1 .hero__content__brand que contem a imagem do logo;  
logo abaixo do h1 criamos um h3 . title--small seguido de um p com um a .link-text e um span .text;  
no arquivo _hero.scss estilizamos com max-width: 640px; também o hero__content através do &;  
dentro de hero__content através do & estilizamos hero__content__brand, definindo sua largura e suas margens;  
ainda dentro de hero__content adicionamos o margin-bottom para .title--small e para o p;  
agora criamos uma ul para os botões com os combos, cada li possui uma imagem, um botão e um span, o span possui a classe .text; o li possui a classe hero__content__combos__combo e a ul a classe hero__content__combos; (um colega ressaltou que essa é a maneira incorreta de usar o BEM, o correto seria hero__content, hero__combos, hero__combo);  
em seguida em um p . text--small falando que o preço pode variar de acordo com a plataforma;  
dai para poder usar nossas variáveis na estilização criamoso arquivo _variaveis.scss e transferimos nossas variáveis para ele;  
por fim, importamos a fonte avenir que já estava salva no material de apoio através da sintaxe @font-face {font-family: Avenir; src url(); font-weight: 400}, repetimos o processo para o font-weight: 700;  
adicionamos a fonte ao body;  
por fim nós configuramos o background-size do hero para cover, dessa forma a imagem de fundo vai ser ampliada e o css tentara usar ela de forma completa, porem, isso funcionou para o professor mas não funcionou para mim, a escala só fica correta no meu navegador alterando o zoom para 80%;  
um colega resolveu isso removendo 20% de todas as medidas, é isso que eu vou fazer agora;  
finalmente meu site cabe na tela do navegador;  
### Aula 4 - Crie a seção de atrações
#### **Sobre a aula**
* aprender a criar uma seção de atrações em um site;
* desenvolver habilidades de manipulação de eventos em JavaScript;
* praticar estilização CSS para destacar a aba ativa.
#### **Anotações**
Vamos criar a seção de atrações, nela temos um grid com as atrações e um menu de navegação por abas;  
a seção tem a classe .shows, dentro dela uma ul .shows__list e dentro dela 6 li .shows__list__item;  
dai estilizamos, dessa vez já estou fazendo os cálculos de -20% para já ajeitar para minha tela;  
em seguida, acima do ul criamos o nav . shows__tabs e dentro dele 3 button .shows__tabs__button;  
repetimos a estrutura da ul mais 2 vezes para termos 3 listas de programas, uma para cada botão, vamos agora adicionar atributos aos botões e as uls para que possamos acessá-los através do JS;  
para os botões criamos o atributo data-tab-button, cada qual com o seu valor, e para as uls o atributo data-tab-id cada um com seu valor respectivo;  
agora vem a programação, a primeira coisa é adicionar um eventListener para o document com 'DOMContentLoaded' e uma função, dentro da função criamos a const buttons que será um querySelectorAll apontando para o atributo data-tab-button;  
dai vamos iterar todos os botões dentro da const e vamos adicionar um eventListener para buttons[i] com 'click' e uma função(botao);  
dentro da função criamos a const targetTab que vai ser igual a botao.target.dataset.tabButton (dataset.tabButton acessa o valor de data-tab-button);  
em seguida criamos outra const tab que será document.querySelector (\`\[data-tab-id=${targetTab}\]\`), essa const contem o elemento ao qual vamos adicionar a classe --is-active, mas antes disso precisamos remover o --is-active da aba atual, para isso criamos a função hideAllTabs;  
essa função contem a const tabsContainer que é igual a document.querySelectorAll('\[data-tab-id\]);  
dai iteramos entre os elementos da const e com classList.remove, removemos a classe --is-active;  
assim sendo, dentro do primeiro laço, ao clicar o botão rodamos hideAllTabs e em seguida com tab.classList.add, adicionamos a classe --is-active a aba selecionada;  
precisamos agora repetir o processo para o botão em si, para isso criamos a função removeActiveButton, que funciona da mesma forma que hideAllTabs, criamos a const buttons que é o querySelectorAll para o atributo data-tabs-button e em seguida iteramos dentro da const removendo a classe --is-active de todos os botões;  
dai chamamos removeActiveButton dentro do primeiro eventListener para o click do botão e por fim através de botao.target.classList.add, adicionamos a classe --is-active;  
para remover o comportamento de mudança no box-model por causa da borda, adicionamos a todos os elementos uma borda inferior de 4px solida transparente, ou seja, quando o botão estiver ativo, a borda será somente pintada da cor e assim não mudará o tamanho do elemento;  
vamos fazer o terceiro commit agora;  
### Aula 5 - Crie a listagem de planos
#### **Sobre a aula**
* criar uma seção de listagem de planos em um site;
* estilizar elementos de acordo com as diretrizes de design;
* utilizar seletores CSS e classes.
#### **Anotações**
Agora vamos fazer a seção escolha seu plano, onde vamos ter 3 colunas, cada uma com um plano, o preço do plano, uma descrição e um botão para assinar, abaixo das colunas um disclaimer;  
o professor está chamando a atenção de que não faz muito sentido usar a tag h3 para o preço nessa seção, já que não é semanticamente um título;  
primeiro criamos a seção .plans, dentro dela um h2 .title--big Escolha seu plano, em seguida uma ul . plans__list e 3 lis .plans__list__item, dentro deles uma img, um strong (ao invés de um h3) com a classe title--small, seguido de um p . text--big com a descrição do plano seguido de um botão com a classe button ASSINE AGORA, aplicamos também essa classe button aos botões do hero, já que os botões de ambas as seções possuem a mesma estilização adicionamos essa estilização ao arquivo main.scss, dessa forma os botões da aba na seção shows não recebem essa estilização;  
na estilização do arquivo _plans.scss adicionamos o padding a seção toda, definimos o text-align center para o h2 dai definimos que a ul tem display: flex; e justify-content: space-around; adicionamos também uma margem superior de 40px;  
todos os itens terão text-align: center; o padding, o max-width: 304px; e o width: 100%;  
estilizamos o item do meio através do pseudo seletor :nth-child(2) e adicionamos a imagem de fundo adequada além de definir o background-size para contain;  
definimos também a altura máxima da imagem além da largura para 100%, assim todos os itens aparecem dentro do container, que é menor que o viewport;  
definimos que o display do strong é block, para que ele ocupe sua propria linha e adicionamos uma margem superior a ele;  
por fim, depois da ul adicionamos um p .text--small que vai ter também o text-align center;  
subimos aqui o quarto commit.  
### Aula 6 - Crie a seção "Assista do seu jeito"
#### **Sobre a aula**
* criar uma seção de conteúdo com imagem e texto;
* aplicar estilos CSS para formatar a seção.
#### **Anotações**
essa seção é super simples, é uma imagem a esquerda com um titulo e um texto a direita;  
então criamos a seção .watch-anywhere, dentro dela uma img e uma div .watch-anywhere__content;  
definimos para .watch-anywhere o padding padrão e o display grid com 2 colunas e align-items: center;  
em seguida definimos o max-width da img para 100%, para que ela respeite a proporção do display;  
em seguida estilizamos a div, que tem um padding lateral e dentro dela estilizamos o h2 que tem um margin-bottom;  
o quinto commit vai somente até ai.


