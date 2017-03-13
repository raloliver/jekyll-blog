---
layout: post
title: "Sass & Compass"
date: 2016-02-14 22:22:10 -0300
categories: css
tags: 
    - css
    - sass
---

![Sass & Compass](https://lh4.googleusercontent.com/-bQ80p_sfJFs/Vr_lTMQ0SUI/AAAAAAAAjjM/bSeszDif3fU/w1207-h905-no/Sass_Logo_Color.svg.png)

O CSS é uma linguagem um pouco burra quando se trata de lógica e tudo nos pré-processadores é pensando em como você consegue melhorar mais seu código e como ele pode ficar mais organizado. 

O CSS é muito simples. Mas uma má organização pode levar equipes inteiras à loucura em longo prazo. Mas tenha em mente que ele, o SASS, não é uma ferramenta para escrever menos CSS, mas para organizar seu CSS

Exemplo:

	
```
$cores: (
azul: #0176bb, 
vermelho: #e3413e, 
amarelo: #f8e042
);

@each $tema, $cor in $cores {
.tema-#{tema} body {
background-color: $cor;
}
}
	
```
	
O $tema seria cada uma das chaves, no nosso caso azul, vermelho e amarelo. O $cor seria cada um dos valores dos temas, ou seja, os valores hexadecimais. A função @each está dizendo assim: a cada valor dos temas (azul, vermelho, amarelo) que encontrar no mapa $cores, repita o bloco de código.

A função @each vai tratar de criar os blocos de CSS com o nome do tema e o hexadecimal.

Funções como if, else, while, each e for são aceitas no SASS ou em qualquer outro pré-processador. 

Também é possível criar funções com a condição de que, se algo for qualquer coisa diferente de falso, execute determinado comando.

Se você tem uma variável qualquer, no nosso caso monster, ela pode mudar de valor em determinado lugar do código. Se mudar, há uma série de condições ali.

	
```
$type: monster;
p {
@if $type == ocean {
color: blue;
} @else if $type == matador {
color: red;
} @else if $type == monster {
color: green;
} @else {
color: black;
}
}
	
```


*for*
"Inicia uma variável e executa uma ação, incrementando essa variável um determinado número de vezes."
```
@for $i from 1 through 4 {
.item-#{$i} {
width: 10px * $i;
font-size: 10px * $i;
}
}
```
*each*
"Define uma variável para item de uma lista de valores, produzindo blocos de código utilizando os valores da lista."
	
```
$cores: (
azul: #0176bb,
vermelho: #e3413e,
amarelo: #f8e042
);
@each $tema, $cor in $cores {
.tema-#{tema} body {
background-color: $cor;
}
}
	
```
*while*
"Repete um determinado bloco e código enquanto determinado estado for verdadeiro."
	
```
$i: 1
$column-width: 60px
@while $i < 13 {
.grid-#{$i} {
column-width: $column-width;
}
$column-width: $column-width + 90px;
$i: $i + 1;
}
	
```

O Miller Medeiros (http://blog.millermedeiros.com/about/) escreveu um ótimo artigo com o nome de The problem with CSS pre-processors (http://blog.millermedeiros.com/the-problem-with-css-pre-processors/). 

Lá ele cita alguns motivos interessantes sobre não usar pré-processadores. Sugiro que você leia.

Pra facilitar essa curva de aprendizado, as equipes podem manter um manual explicando as boas práticas de escrita de código.

Sem comentar o aninhamento (nesting) de seletores para evitar o repetição de elementos.

Para evitar problemas assim, a documentação deveria ser muito bem atualizada, apontando todas as relações de mixins, extends, variáveis etc.

Geralmente pré-processadores escrevem mais código do que você escreveria manualmente.
Usando extend

Hoje meu processo envolve usar Middleman e SASS nos projetos do Tableless

Fiz um artigo no Tableless que explica como instalar SASS na sua máquina de maneira fácil. Segue o link: http://tableless.com.br/instalando-sass-na-maquina-video/

A minha opinião é de que você não precisa aprender todas as novas ferramentas e tecnologias que existem por aí.

Muitos devs perdem tempo precioso dando atenção para novas ferramentas que nem serão usadas pela equipe ou que morrerão nos próximos meses.

Para usar o Sass é preciso instalar o ruby, como orientado no próprio site da documentação. A extensão do arquivo padrão é .scss e para observar as mudanças e a compilação do arquivo final (.css) o comando é:
```
sass --watch file.scss:file.css
```
Uma boa prática é observar os nome dos diretórios e arquivos com o _ na frente. As variáveis são criadas a partir do $, exemplo: $color. Geralmente existe um arquivo principal .scss que faz a chamada via import de todos os outros arquivos. Mantenha sempre as variáveis num único arquivo, assim como os mixins, usando sempre a pasta helpers para padronizar a estrutura.

No Sass existem as funções, mixins, variáveis, aninhamento e outros detalhes que naturalmente não seria possível no css normal. O @include, faz referencia a chamada de um mixin. 

*Mixins*
O @mixin é criado de maneira parecida com o placeholder, mas aceita valores padrão, como no exemplo a seguir:
```
@mixin border-radius($radius: 0.3em) {
  -webkit-border-radius: $radius;
  border-radius: $radius;
}
```
Geralmente os mixins são usados para bloco de códigos, mas você pode usar os do Compass (framework) também. É possível com o @mixin receber argumentos na função, inclusive com a opção de valor padrão.

Functions
Com o @function é possível realizar funções matemáticas e para invocar basta chamar ela sem nenhum operador, apenas o nome, exemplo:
@function fixed-width ($value) {
	@return $value x $variable;
}
width: fixed-width(18);


Ainda é possível arrendodar o resultado de uma operação, usando a função round do próprio Sass.

PlaceHolder
Para criar extend e placeholder, basta usar o % na frente na criação e chamar atraves do @extend.
Com o @extend você invoca um placeholder e faz chamada via %.
```
%image-replacement {
  text-indent: -9999px;
  overflow: hidden;
  background-repeat: no-repeat;
}

.plataformas li {
  @extend %image-replacement;
}
```
Existem comandos internos no SASS para assistir, compilar e comprimir.
Com o Sass também é possível realizar aninhamento (nesting) o que reduz a quantidade de código e sempre faz referencia ao item pai, exemplo:
	
```
header {
  border-top: 5px solid $color-default;
  background: rgba($color-second, 0.8);
  height: 90px;
  width: 100%;
  position: absolute;
    // # para concatenar com string
    @media #{$max-width} {
      height: auto;
        h1 {
          max-width: 50%;
          margin: 0 auto;
            img {
              max-width: 100%;
              margin: .5em auto;
              display: block;
            } // fim do img
        } // fim do h1
    } // fim do mq (media query)
} // fim do header
	
```

Algo legal para usar com o Sass são as combinações de cores. Funções de cores em variações simples parecidas com as cores e regras do material design, exemplo: darken(#069, 20%) ou lighten(). Existem também outras funções: complement, sature e adjust-hue.

Media Queries
Com o aninhamento (nesting) é possível criar as media queries internas diretamente no seletor (também da pra fazer automaticamente com o grunt).

Nos arquivos .scss é possível criar comentários com duas barras (//) e esses comentários não serão exibidos no css final.

Confira também a sintaxe para uso de valores completos em variáveis.
Declaração: 
	
```
$max-width: "(max-width:" $container-desktop")";
	
```
Chamada: 
	
```
header .container {
  position: relative;

    @media #{$max-width} {
      position: static;
    }
}
	
```
Isso é como concatenar e ainda isolar toda um media querie numa variável.



*COMPASS*
Instalação
	
```
- gem install compass 
- compass create
	
```

Atenção ao arquivo config.rb onde contêm as configurações do projeto.
Também é possível observar (watch) com o compass: 
	
```
compass watch file.scss // atenção ao diretório (funciona como --watch do sass)

	
```
Por padrão o compass adiciona comentários ao .css final, para desativar essa opção, altere o arquivo de configuração (config.rb) line-_comments=false (atenção o watch deve ser reiniciado).

*Sprites*
O compass cria os sprites automaticamente. Basta isolar os arquivos desejados num diretório e chamar ele no arquivo principal do scss. Com a possibilidade de configurar um espaçamento entre as imagens.
*directory é o nome do diretório onde se encontram os arquivos para o sprite.
	
```
$directory-spacing: 5px;
@import "directory/*.png";
	
```

Para compilar os sprites é necessário invocar a função no arquivo desejado através do comando: 
@include all-directory-sprites;

Com base no nome do diretório e dos arquivos, novas classe são criadas.

Minificar
Com o compass, basta editar o arquivo de configuração (config.rb):
output_style = :compressed
Diretamente no Sass também é possível fazer:
	
```
sass --style compressed file.scss:file.min.css
	
```
Ainda é possível realizar operações matemáticas no sass, como por exemplo para a conversão do tamanho de fonte (em, rem, px).
