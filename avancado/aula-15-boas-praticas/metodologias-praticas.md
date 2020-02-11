# Metodologias e práticas no desenvolvimento de CSS

## Object Oriented CSS (OOCSS)
A ideia base é separar a _estrutura_ do elemento do seu _visual_.
Por exemplo, para o conjunto de botões
```
<button class="botao primario">Click me</button>
<button class="botao secundario">Click me 2</button>
```
o CSS utilizando a metodologia OOCSS seria:
```
.botao{
	/* Estrutura: tamanho e forma */
	width: 200px;
	height: 50px;
}

.primario{
	/* Visual: cores */
	color: white;
	background-color: #0062ac;
}

.secundario{
	color: #252525;
	background-color: #f2f2f2;
}
```

## Blocks, Elements and Methods (BEM)
Não se trata de como _estilizar_ os elementos, mas sim de como _nomear_ as classes.
Portanto, é utilizado em conjunto com outras práticas de estruturação do CSS.

### Block
É uma entidade _standalone_ que tem sentido por si própria, como:

`botao`, `container`, `menu`, `input`

### Element
Parte de um bloco que não tem sentido sozinho, e é semanticamente atrelado ao bloco:

`botao label`, `container item`, `menu item`, `input caption`

### Modifier
É um _flag_ em um bloco ou elemento, utilizado para alterar aparência ou comportamento:

`disabled`, `highlighted`, `checked`, `fixed`, `size big`, `color yellow`

### Convenção de nomenclatura
* O nome do _Element_ é separado do nome do _Block_ por dois _undescores_ ( `_` )
* O nome do _Modifier_ é separado do _Block_ ou _Element_ por dois hífens ( `--` )
* O valor do _Modifier_, se houver, é separado do nome do _Modifier_ por um hífen ( `-` )

### Exemplos
```
.page { }

.content { }

.footer { }

	.footer__copyright { }

.button--highlighted { }

.profile { }

	.profile__image { }

	.profile__image--disabled { }

	.profile__image--background-blue { }
```

## Atomic CSS (ACSS)
Consiste em declarar no CSS algumas classes que possuem apenas uma declaração.
Isso serve para que não seja criar regras para apenas alguns elementos quando desejamos alterá-los,
e acaba fazendo com que apareçam classes que servem de _aliases_ para algumas propriedaes com valores definidos.

Por exemplo, o CSS abaixo possui três classes atômicas:
```
.mt-10{ margin-top: 10px; }
.mt-20{ margin-top: 20px; }
.fs-20{ font-size: 2.0em; }
.minha-div{
	color: red;
	background: green;
	font-size: 1.5em;
}
```

Neste exemplo, três classes ofereceram um valor específico para uma propriedade em específico.
Associando ao seguinte HTML:
```
<div class="minha-div mt-10" >
	Treina<span class="fs-20">Web</span>
</div>
```
Aqui, temos uma `div` com uma classe comum. O tamanho de fonte dessa classe é `1.5em`, no entanto, 
temos interesse que apenas uma palavra dentro dessa `div` tenha um tamanho de fonte maior, `2em`.
Para isso, em vez de utilizar um seletor apenas para esse ajuste (ou ainda, declarar a regra direto no HTML),
utilizamos a classe `fs-20`, que serve unicamente (atomicamente) para este propósito.
Além disso, passamos a classe `mt-10` para dar uma margem superior de `10px`,
separando este ajuste das propriedades da `div`.

Com _ACSS_, geralmente são criadas classes com diversos valores para as propriedades de `margin`,
`padding` e `font-size`.

## DRY CSS
Leva a famosa sigla do desenvolvimento de software: _Don't Repeat Yourself_.
No caso do CSS, consiste em otimizar removendo declarações de uma mesma propriedade ao longo do código
que tenham valores repetidos.
Por exemplo:
```
div{
	background-color: #f2f2f2;
	height: 100px;
	width: 40%;
}

.minha-classe{
	background-color: #f2f2f2;
	width: 90px;
	height: 100px;
	display: inline-block;
}
```
Aqui, é possível ver repetição de propriedade e valor para `background-color` e `height`.
Portanto, ao aplicar _DRY CSS_ deixaríamos como:
```
div, .minha-classe{
	background-color: #f2f2f2;
	height: 100px;
}

div{
	width: 40%;
}

.minha-classe{
	width: 90px;
	display: inline-block;
}
```

## Scalable and Modular Architecture for CSS (SMACSS)
Foi desenvolvida pela _Yahoo!_ e é uma arquitetura amplamente utilizada.
Baseia-se em categorizar as regras do CSS em:

### Base
São as regras _default_.
Praticamente são compostas de seletores de um único elemento, mas podem incluir seletores de atributo,
pseudo-classes, seletores filhos ou seletores-irmãos.
Essencialmente, um estilo _Base_ define que onde quer que este tipo de elemento esteja na página, ele
deve ter _essa_ aparência.
Por exemplo:
```
html, body, form { margin: 0; padding: 0; }
input[type=text] { border: 1px solid #999; }
a { color: #039; }
a:hover { color: #03C; }
```

### Layout
Dividem a página em seções. _Layouts_ agrupam um ou mais _modules_.

### Module
São as partes reutilizáveis e modulares do design.
Representam os _callouts_, as ações da barra lateral, as listas de produtos e assim por diante.

### State
Modos de descrever como os módulos ou layouts vão aparentar em um estado particular,
por exemplo, "oculto" ou "expandido", "ativo" ou "inativo".
Identificam também a aparência dos módulos e layouts em telas que são menores ou maiores.
Também definem como um módulo vai aparentar em diferentes exibições, como na _homepage_ ou em uma página interna.

### Theme
São similates a regras _state_ no sentido de definirem a aparência de módulos ou layouts.
Aplicam-se à configurações de exibição da página, por exemplo, as opções de tema claro ou tema escuro.
A maior parte dos sites não requere uma camada de _theme_.

## Inverted Triangle CSS (ITCSS)
Aproveita o fluxo do código no CSS - isto é, a ordem em que o código é processado - para determinar as regras.
Isso é vantajoso para determinar regras específicas que sobrescrevem as regras mais genéricas, mesmo que uma
propriedade já tenha tido seu valor atribuído em um ponto _anterior_ do CSS.

Daí o nome _Inverted Triangle_: a proposta é iniciar o código com declarações mais _genéricas_ e deixar as mais
_específicas_ na parte final do arquivo.
Isso é padronizado em um triângulo invertido que tem as seguintes camadas (de cima para baixo):
* Settings - **mais genérico**;
* Tools;
* Generic;
* Base;
* Objects;
* Components;
* Trumps - **mais específico**.

### Settings
Configurações do projeto, como variáveis de medidas, cores etc.
```
$my-color: #0057fb;
$footer-height: 120px;
```

### Tools
Onde são colocadas funções, mixings, placeholders etc.
Se não estiver utilizando algum preprocessador CSS, esta camada não é utilizada.
```
@mixin my-box(){
	width: 200px;
	height: 100px;
}
```

### Generics
Camada para as propriedades com menor especificidade.
O mais comum aqui acaba sendo o seletor `*`.
```
*{
	box-sizing: border-box;
}
```

### Base
Voltada para estilizações mais básicas dos elementos.
Portanto, aqui não devem ser usados IDs ou classes, apenas seletores de tags.
```
div{
	padding: 10px;
}
```

### Objects
Aqui são declaradas apenas classes.
É onde fica a estilização da estrutura dos elementos.
```
.my-button{
	width: 200px;
	padding: 10px;
}
```

### Components
A camada superior, _Objects_, tenta ser mais genérica.
Aqui, tenta-se ser mais específico quanto à estilização dos elementos.
Nesta camada também são utilizadas apenas classes.
```
.my-red-button{
	background-color: red;
	color: white;
	border: 2px solid black;
}
```

### Trumps
Camada com as regras mais específicas de todas.
Por ser a última a ser processada, tudo o que é colocado aqui sobrescreve as camadas _superiores_.
Aqui, é permitido o uso do modificador `!important`, que impede a propriedade declarada de ser
sobrescrita.

A maioria das propriedades declaradas nesta camada são pequenos ajustes em alguns elementos, ou
definições de estado de elementos.
```
.hidden{
	display: none !important;
}
```
