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
