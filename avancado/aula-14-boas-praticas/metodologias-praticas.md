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
