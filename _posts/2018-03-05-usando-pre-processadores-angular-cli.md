---
title: Usando pré-processadores Sass e Stylus com Angular Cli
layout: post
categories: [angular, css]
---
Quando criamos um novo projeto utilizando o **[Angular Cli](https://github.com/angular/angular-cli){:target="_blank"}** a opção padrão para os estilos é .css.
Mas depois de conhecer o maravilhoso mundo dos pre-processadores, não fazer uso deles nos nossos projetos é quase impossível.  

Então como fazer para trabalhar com pre-processadores **[Sass](http://sass-lang.com/){:target="_blank"}**, **[Less](http://lesscss.org/){:target="_blank"}** ou **[Stylus](http://stylus-lang.com/){:target="_blank"}** utilizando o AngularCli?

A primeira forma é assim que iniciamos o projeto: 
```
ng new projeto --style=sass
```

A flag **--style** será responsável para indicar que estaremos usando um estilo alternativo para nossa aplicação. 
Outras opções suportadas pela flag style são: scss, less e styl(para o stylus).

Caso o projeto já tenha sido criado podemos utilizar o seguinte comando, na pasta do projeto:
```
ng set defaults.styleExt = sass
```

Esse comando é uma maneira prática para alterar o arquivo angular-cli.json que você pode checar.
```
"defaults": {
  "styleExt": "scss",
  "component": {
  }
}
```

Lembrando que essa alteração, após a criação do projeto, não alteram os arquivos .css que já foram criados. Cada arquivo deve ser alterado manualmente bem como a chamada feita no **angular-cli.json**: 
```
"styles": [
    "styles.sass"
]
```

### Importando estilos para nosso projeto

Os componentes em projetos Angular são autônomos e isso também se aplica aos seus estilos. Com isso, ao criarmos estilos para um componente o seu uso fica restrito a ele.

Para compartilharmos ou reutilizar estilos em diversos componentes existem duas opções.

Uma forma é utilizar o símbolo **'~'**.

Vamos supor que na pasta **src/** do nosso projeto criamos a pasta **styles/** e o arquivo **_mixins.scss**.

Criamos o componente topo e em seu arquivo de estilo **topo.component.scss** adicionamos o nosso arquivo de mixin:
```
@import '~styles/_mixins.scss';
```

O **'~'** se encarrega de criar o caminho relativo até a pasta **src/** do projeto e com isso temos acesso a nossos estilos em qualquer parte do projeto.

Outra alternativa é utilizar o [stylePreprocessorOptions](https://github.com/angular/angular-cli/wiki/stories-global-styles){:target="_blank"}, no arquivo angular-cli.json
```
"stylePreprocessorOptions": {
  "includePaths": [
  "../src/styles/"
  ]
}
```
Esse é o jeito mais indicado para utilizarmos, lembrando que os estilos estão acessíveis em nível global.
Para importarmos os estilos em nossos componentes podemos apenas utilizar:
```
@import 'mixins'
```

Não é preciso inserir o '_' nem a extensão do arquivo.

Podemos utilizar esse mesmo processo com arquivos externos, como por exemplo do Bootstrap. Indicamos seu caminho e fazemos a importação de todos os arquivos ou apenas daqueles que realmente precisamos usar em nosso projeto.
```
"stylePreprocessorOptions": {
  "includePaths": [
    "../node_modules/bootstrap/scss",
    "../src/styles/"
  ]
}

// src/sass/styles.sass

@import 
  'functions',
  'variables',
  'mixins',
  'print',
  'reboot',
  'type';
```
Com isso temos apenas os arquivos necessários disponíveis para nossa aplicação.

### Autocomplete no VSCode
Uma ótima ajuda que temos com o VSCode é a opção de autocomplete entre os arquivos importados. Para isso basta instalar a extensão [SCSS IntelliSense](https://marketplace.visualstudio.com/items?itemName=mrmlnc.vscode-scss){:target="_blank"}.

