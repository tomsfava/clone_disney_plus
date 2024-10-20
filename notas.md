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
### Aula 7 - Crie a seção "Dispositivos disponíveis"
#### **Sobre a aula**
* restruturar uma seção de conteúdo com imagem e lista;
* aplicar estilos CSS para formatar a seção;
* resolver problemas de alinhamento e vazamento de conteúdo.
#### **Anotações**
essa seção não é muito diferente da seção anterior, porem, ao invés de uma imagem na esquerda e uma div na direita, o que temos é uma imagem no fundo e a div por cima, isso é feito através do position: absolute;  
Então copiamos a seção anterior e alteramos os valores necessários, já que existe essa repetição de estrutura de seção, podemos copiar o conteúdo do arquivo _watch-anywhere.scss para o arquivo main.scss e criamos um nome de classe mais generico .image-text-section, para isso é necessário fazer as alterações das classes dos elementos dentro do bloco também;  
para esse caso específico vamos criar um modificador para esse bloco no caso --image-full-width, assim dentro da estilização de image-text-section estilizamos &--image-full-width para ter display: block (isso inicialmente fará com que a imagem aparece acima do __content, resolveremos isso com o position absolute do __content);  
definimos que a width da img é 100%, para que essa ocupe a section inteira;  
agora estilizamos o __content para position absolute, o top igual ao padding, a altura de 100% o display flex para podermos alinhar de forma mais facil, mudamos a direção do flex para coluna e por fim justify-content center;  
dessa forma a div __content escapou do nosso container e foi lá pra cima no site, na seção hero;  
precisamos fazer com que nosso container prenda o __content, fazemos isso adicionando o position relative ao container (section .image-text-section--image-full-width);  
isso conteve o __content, porem precisamos reposicioná-lo, já que ele ficou na esquerda da imagem e nós queremos ele na direita;  
para isso adicionamos uma propriedade left: 50% assim o __content ficara na metade do container, porém, dessa forma ele escapa para fora, vamos resolver isso adicionando uma propriedade width: calc(50% - 4.4vw), lembrando que 4.4 vw é o valor do padding da seção;  
terminada essa seção, vamos fazer a próxima, que é uma lista horizontal dos dispositivos onde o disney+ está disponível;  
primeiro então criamos a seção que vai conter uma lista com 4 li, cada li vai conter uma imagem um h4.title--small e uma ul.text, cada ul vai conter o numero de lis de acordo com o site da disney;  
damos a seção a classe devices e criamos o arquivo _devices.scss, nesse estilizamos o padding da sessão em seguida o título da sessão, que possui a classe title, e vai ter o text-align center e um margin-bottom;  
em seguida estilizamos devices__list (ul) para ter display grid, o gap apropriado e o grid-template-columns para repeat 4 1fr;  
dentro desse estilizamos o devices__list__item para que tenha o text-align: center;  
o h4 dentro dele vai ter suas margens, o li tera list-styles: none;  
o img tera o max-width: 100% ou seja cada imagem ocupará todo o li;  
até aqui vai o sexto commit; 
### Aula 8 - Crie a FAQ
#### **Sobre a aula**
* compreender a estrutura e os componentes de uma seção de perguntas frequentes (FAQ);
* aprender a aplicar transições CSS para melhorar a experiência do usuário;
* praticar a criação de componentes reutilizáveis.
#### **Anotações**
vamos agora criar a seção de perguntas frequentes, que é composta de 4 accordions;  
cada accordion vai ser um li de uma ul, cada li vai conter uma div pra pergunta e outra div pra resposta, criamos essa estrutura e em seguida criamos o _faq.scss para estilizá-la, a ul vai ter a classe faq__questions a li vai ter a classe faq__questions__item, a pergunta vai ter a classe faq__questions__item__question e a resposta faq__question__item__answer;  
quanto a estilização é o padding padrão para a seção .faq, o h2 tem text-align center e uma margem inferior;  
as li vão ter background-color e margem inferior;  
estilizamos as perguntas para ter a cor branca, definimos o font-size, o padding, o display block e o cursor pointer;  
ao answer adicionamos a classe text--big e estilizamos um padding;  
agora vamos criar o + e o - do accordion através de um pseudo elemento css, temos dois o ::before e o ::after;  
nesse caso vamos estilizar o pseudo elemento ::after a div __question, então digitamos &::after e dentro do bloco de estilo definimos o content para '-' (já que a pergunta está aberta), definimos o position absolute (o que vai requerer que definamos o position relative para o elemento pai), top 0 right=padding height:100%; display flex align-items center e font-size 40px;  
por padrão as perguntas vem fechadas e com o sinal de +, vamos sumir com a resposta não com o display:none; mas sim com o height:0; o overflow:hidden e tambbém removendo o padding;  
faremos o conteúdo voltar a ser visível através de um modificador --is-open adicionado a classe do elemento pai, .faq__questions__item--is-open, na estilização simplesmente dentro do bloco do .faq__questions__item adicionamos o &--is-open e dentro desse novo bloco estilizamos a classe da resposta: .faq__questions__item__answer, definindo sua height para auto e seu padding para o valor adequado (80% de 24px) e também alteramos o content no pseudoelemento after do elemento pergunta para que esse seja - ao invés de +;  
quanto a programação criamos a const questions que vai ser um querySelectorAll para o atributo 'data-faq-question' que adicionamos a todos os elementos pergunta (elemento clicável);  
em seguida iteramos por todos os elementos de questions com um addEventListener('click', abreOuFechaResposta), ou seja, para cada questão que for clicada, roda a função abreOuFechaResposta, falta somente criar essa função;  
a função recebe como paremetro elemento, sendo que elemento nada mais é do que o elemento clicável dentro do laço anterior, dentro da função criamos a const classe que contem a classe que sera alternada através do toggle: faq__questions__item--is-open;  
em seguida criamos a const elementoPai = elemento.target.parentNode; já que o elemento clicável é a pergunta mas o elemento que recebe a alternância de classe é o elemento pai, a div .faq__question__item;  
terminamos a função codificando elementoPai.classList.toggle(classe); dessa forma nosso accordion já está funcionando, falta somente adicionar um efeito de transição mais amigável, faremos isso através do sass;  
simplesmente ao elemento já aparente, adicionamos a propriedade transition com o valor que será 'transicionado': height, o tempo de transição: .5s e o efeito: ease;  
um pequeno problema é que estava havendo também uma animação lateral para o texto dentro da div answer, isso ocorre porque o padding lateral também está transicionando de 0 para 19.2, removemos esse comportamento adicionando o padding lateral na div sem o modificador do elemento pai, dessa forma o texto simplesmente desce junto com a div no momento da interação;  
porem com essa estilização adicionamos o efeito de transição somente para a abertura do accordion, para adicionar esse efeito também no fechamento precisamos adicionar a propriedade transition com os mesmos valores também na div answer sem o modificador do elemento pai;  
### Aula 9 - Criando o rodapé
#### **Sobre a aula** 
* compreender a estrutura e os elementos de um rodapé web;
* aprender a estilizar elementos de um rodapé com CSS;
* praticar o uso de variáveis CSS para gerenciar estilos.
#### **Anotações**
O rodapé possui um logo, uma listagem de links, dois paragrafos .text--small;  
primeira coisa é agrupar todo o conteudo do footer (que por sinal, recebe uma classe footer para estilização) dentro de um container footer__container, esse container é centralizado através do max-width: 840px, width: 100% e margin 0 auto, também usamos o text-align: center e damos um padding-bottom de 20px;  
dentro dele criamos uma imagem com a classe footer__logo e estilizamos ela para possuir a largura de 80px e margin: 0 auto 10px;  
em seguida criamos uma ul classe footer__links que é estilizada para ter um margin-bottom de 16px, um display flex, um align-items center e definimos o flex-wrap para wrap e o justify-content center;  
em seguida, dentro dessa estilização estilizamos os itens que possuem a classe footer__links__item, seu display é inline-block, e dentro dessa estilizamos os links para possuirem text-decoration none, adicionamos um padding a cada item além do display block, ainda dentro de a estilizamos o pseudo-seletor :hover para ter uma variação de cor;  
ainda dentro de footer estilizamos os paragrafos para possuirem uma margin-bottom de 16px;  
entre os links existe um seletor de linguagem, criamos esse elemento através da tag select, ela vai estar contida na div .language-selector, que além do select vai conter uma imagem com o icone do globo, o select vai conter duas tags option, uma com o conteúdo English e a outra Português, essa vai possuir o atributo selected;   
na última aula nós não subimos as atualizações para o github, então o commit atual vai conter tanto o arquivo _footer.scss quanto o arquivo _faq.scss, esse será o sétimo commit;  
### Aula 10 - Criando o cabeçalho
#### **Sobre a aula**
* compreender a estrutura HTML e CSS do cabeçalho;
* aplicar técnicas de responsividade;
* implementar comportamentos interativos.
#### **Anotações**
Primeira coisa notável nessa aula é sua duração de 40 minutos, sobre o cabeçalho em si nota-se o comportamento de que na primeira seção somente o botão de entrar é aparente, mas conforme ocorre a rolagem o logo e o botão de 'ASSINE AGORA' surgem, o cabeçalho é fixo no topo da página;  
primeira coisa criamos a tag header com a classe header, dentro dela, em seguida um container com a classe header__container;  
próxima ação é substituir a tag h1 que continha a imagem do logo por uma div, em seguida recriamos a tag h1, só que agora no cabeçalho, tornando mais fácil a identificação do título da página no seu local adequado, o cabeçalho;  
assim, após o h1 que contém a imagem do logo, criamos uma ul .header__links com dois li .header__links__item, cada um com um link contendo primeiro o 'Assine agora' e em segundo 'Entrar';  
ambos os links recebem a classe button;  
em seguida criamos a estrutura de estlização com o header no topo e em seguida paralelos as classes __container, __logo e __links que por sua vez contem __item;  
o contaier do header não possui limitação de largura; ele possui padding de 8 e 36 e o display flex;  além de um justify-content space-beetween, que vai separar o h1 (footer__logo) da ul (footer__links);  
o logo vai ter max-width de 80px com width de 100% e os links vão ter display flex;  
depois dessa estilizaçao inicial notamos que a regra genérica do button contem um margin-top e bottom que não é necessario em todos os botões, somente em alguns, vamos retirá-lo da regra em main e adicioná-lo nas seções adequadas (hero e plans); 
em seguida vamos criar estilizações para modificadores dos botões, será tanto o botão secundário, azul, quanto o botão escuro, preto com transparência 0.8, para isso criamos as variáveis das cores;  
estilizamos o height do botão dentro do header para ele ser um pouco menor e adicionamos as classes adequadas aos botões;  
agora vamos esconder os botões que ficam escondidos no topo da página mas que passam a aparecer conforme a rolagem, para isso criamos a classe hidden e definimos o visibility para hidden;  
agora vamos definir o positon sticky para o header, com top e left 0;  
agora vem a programação, primeiro comentamos cada parte do código explicando o que cada uma faz, em seguida criamos duas const a const heroSection que contem o elemento com a classe hero e em seguida a const alturaHero que contem heroSection.clientHeight;  
em seguida vamos criar um eventListener para o window, o evento será o scroll e a função vai conter uma const posicaoAtual que vai conter window.scrollY;  
criamos essa constante para compará-la com a alturaHero, fazemos isso através de um if (posicaoAtual>alturaHero);  
porém, já que tem muito mais posiçoes > alturaHero, podemos inverter a lógica, deixar os elementos visíveis por padrão e ocultá-los quando a posição for menor que alturaHero;  
vamos então alterar também a lógica do css, ao invés de adicionar a classe hidden ao botão e ao logo, vamos adicionar o modificador --is-hidden para o header, já que no comportamento original a bara do header também some, então quando existe o modificador o background-color vai ser transparent e o header__logo e o header__links__item:first-child terão opacity:0; porém, com esse método o botão fica invisível porém segue clicável, corrigimos isso adicionando o visibility: hidden;  
agora é simplesmente criar funções que adicionam e removem a classe com o modificador, fazemos isso criando uma const para o header com o querySelector e em seguida manipulamos o elemento através do header.classList.add ou classList.remove respectivamente para cada função, adicionamos ambas no funcionamento do if else dentro do eventListener do scroll;  
por fim adicionamos a propriedade transition em todos os elementos com e sem o modificador, no caso dos botões ela aponta para o opacity e no caso do header em si aponta para o background-color;  
por fim vamos subir a prioridade do header com o z-index, já que ele estava sendo coberto pela imagem do rei leão;  
até aqui vai o oitavo commit;  
### Aula 11 - Realize o deploy
#### **Sobre a aula**
* compreender a importância da responsividade em design web;
*aprender a aplicar estilos responsivos usando CSS;
* praticar habilidades de deploy de um projeto web.
#### **Anotações**
adicionamos medias queries nos arquivos devices, plans shows e main, no prmeiro reduzimos a quantidade de colunas para duas, no segundo alteramos o display da lista de planos para block, no terceiro também reduzimos as colunas para duas e no último alteramos o display da image-text-section para block e no caso do modificador --image-full-width, dentro do __content, alteramos o display para block o position para relative o left para 0 e o width para 100%;  
em seguida, no arquivo main vamos adicionar media queries para os font-sizes dos titles, decidimos não fazer o mesmo para os texts já que com a redução de 20% que realizamos anteriormente a diferença ficou insignificante;  
agora vamos também estilizar a responsividade do hero, primeiro alterando a imagem do bg-img para a imagem adequada a celular, essa imagem ficava sob a logo, para resolver isso aumentamos o padding (o bg-img ocupa o padding, a logo não), também ajustamos o bg-size para contain (o que ajusta as proporções da imagem) e o bg-repeat para no-repeat;  
alteramos também o tamanho do logo para ter max-width de 180px;  
definimos o display do __combos para block e definimos o width do __combo para 100% além de adicionar uma margin-bottom de 24px;  
agora vamos ajustar o botão do cabeçalho para um tamanho menor, depois retornaremos ao hero;  
primeira coisa é alterar o font-size dos botões para 13px, o padding para 8 no topo e embaixo e 11 nas laterais e também removemos o letter-spacing;  
depois reduzimos o max-width do logo para 64px;  
de volta ao hero, queremos que a imagem extrapole o header, para isso adicionamos uma margem negativa do tamanho do header, isso vai mover a section hero 55px pra cima, só que a logo ainda não está na posição correta, queremos mais 25px além dos 50vw que já haviamos definido para o padding, para isso usamos a função calc com os valores 50vw + 25px;  
em seguida na section shows, nos botões das abas, queremos remover o wrap do white-space, ou seja, remover as quebras de linha, também queremos que o overflow do eixo x seja scroll, para permitir a rolagem, adicionamos um padding-left de 20px para ajustar a posição do primeiro botão;  
em seguida voltamos a plans para espaçar o botão e o texto dos planos simplesmente estilizando a classe button dentro de plans para ter um margin-top de 24px;  
em seguida, vamos utilizar outra imagem a seção do rei leão, para adicionar essa responsividade no corpo do html vamos usar a tag picture, ela funciona contendo uma tag source com atributo media="(max-width: 768px)" e um atributo srcset apontando para o arquivo;  
com isso finalizamos a responsividade para celular, por algum motivo não realizamos o mesmo para tablet e depois dessa última alteração da imagem do rei leão o professor simplesmete commita as alterações para que realizemos o deploy;  





