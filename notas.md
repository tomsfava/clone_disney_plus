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