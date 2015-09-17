#Guia básico de CSS3

Além de um introdução CSS3, este guia pretende mostrar como criar um site responsivo, ou seja, que se adapte a qualquer dispositivo.

Você terá um nível de compreensão muito maior se acompanhar também meu vídeo no YouTube, onde eu mostro passo a passo como criar um site responsivo, mobile-first (técnica de criar páginas partindo do menor tamanho possível e ir escalando até chegar ao tamanho final, que geralmente é o desktop).

O objetivo deste guia não é esgotar o conteúdo proposto (CSS e CSS3), e sim apresentar o necessário para construir um site completamente responsivo, bem estruturado, utilizando as melhores práticas e útlimas especificações da linguagem.

Animações, transições e outras interações mais complexas virão em um próximo guia, acompanhadas de um vídeo no canal.

##Público alvo deste guia
Pessoas que estão iniciando o aprendizado de tecnologias para desenvolvimento web, desenvolvedores que queiram atualizar seus conhecimentos em CSS3 e design responsivo e quem mais estiver curioso sobre como funciona um site “por baixo do capô”. É aconselhável conhecimento básico em HTML, que pode ser adquirido aqui e um entendimento mínimo de inglês.

##O que veremos
Como criar o estilo de um site responsivo, utilizando o máximo possível das últimas especificações do CSS3, com muito flexbox e nada de floats.

##O que não veremos
História do CSS, quem criou, por que criou, especificações antigas, elementos
antigos e fora de uso, animações e transições. As duas últimas serão abordadas em um material futuro.

##Índice


###Introdução
CSS significa **C**ascading **S**tyle **S**heets, ou folhas de estilo em cascata. O detalhe aqui é a parte de “cascata”. Basicamente isso quer dizer que as regras de estilo se sobrepõem, ou seja, uma regra que eu escrever no começo do meu documento de CSS (no alto da cascata) vai ter menor prioridade sobre uma que eu escrever no fim deste documento (no fim da cascata), por exemplo. O exemplo é tosco, mas é assim que funciona.

Por fim, CSS é uma linguagem utilizada para prover **estilo**, que define a **aparência** do conteúdo (HTML).

Mãos à obra.

###Sintaxe

Aqui entra o requisito de entender o mínimo de inglês. TODAS as regras e valores são descritas em inglês. Apesar disso, CSS é muito intuitivo. Vou configurar a **cor** e o **tamanho da fonte** de todos os parágrafos de uma página para que você possa ver isso:

```css
p {
    font-size: 24px;
    color: black;
}
```

No exemplo acima, ```p``` é um **seletor** que aplica estilo a todos os elementos ```<p>``` de uma só vez. As **propriedades** ```font-size``` e ```color``` estão inclusas entre chaves e descrevem qual característica está sendo alterada. Os **valores** determinam o estilo da propriedade em questão e devem vir depois do ```:``` (dois pontos) e seguidos por ```;``` (ponto e vírgula) para finalizar a declaração.

Resumindo: Um par de **propriedade** e **valor** é chamado de **declaração** e deve estar entre ```{}``` (chaves) e separados por ```:``` (dois pontos) e seguidos por ```;``` (ponto e vírgula).

###Onde escrever CSS
Existem três principais locais onde você pode escrever CSS:

* Em linha (inline)
```html
<p style=”color: red;”>Aqui vai meu texto</p>
```
* No documento HTML
```html
<style>
    p {
        color: red;
    }
</style>
```
* Arquivo externo (onde você vai usar em 98% dos casos)
```css
p {
    color: red;
}
```

No caso 1, você precisa aplicar os estilos a cada elemento, misturado com o HTML. Imagine ter que estilizar 400 parágrafos e depois de uma semana ter que mudar a cor de todos… Só faça isso se for em últimos casos.

No caso 2, geralmente se adiciona dentro do ```<head>``` uma tag ```<style>``` que abrigará nossas regras. Esse método é aconselhável caso você tenha poucas regras ou queira reduzir o número de requisições de arquivos externos. Ainda que nesse caso você possa criar uma regra que aplique estilo a todos os seus 400 parágrafos, essas regras só serão aplicadas ao documento atual, ou seja, se você tiver 20 páginas, vai ter que copiar e colar em cada uma delas o MESMO código.

No caso 3, por ser um arquivo externo, você escreve apenas uma vez o código e pode linkar esse arquivo a quantas páginas quiser, assim, quando você alterar o arquivo CSS, todas as páginas receberão o mesmo estilo. A menos que você tenha um ÓTIMO motivo pra usar os outros métodos, **escolha sempre esse**.

###Seletores

####Seletores de tipo
Corresponde ao nome do elemento. Usado sozinho, um seletor com um elemento específico seleciona todos os elementos daquele tipo em um documento.

Exemplo que pinta o fundo e a cor da fonte de todos os cabeçalhos ```h1```:
```css
h1 {
    background-color: red;
    color: white;
}
```

####Seletores de ID
Corresponde ao ID definido nos atributos de um determinado elemento no HTML. Aplica estilo exatamente ao elemento que contém o ID solicitado. Note que **não pode existir mais de um** ID com o mesmo nome no HTML.

Exemplo:

Trecho do HTML:
```html
<p>Elemento sem ID</p>
<p id=”importante”>Elemento que será selecionado</p>
```

CSS:
```css
p#importante {
    color: red;
}
```

####Seletores de classe
Corresponde à classe definida nos atributos dos elementos no HTML. Aplica estilo a todos os elementos que tiverem aquela classe. Note que vários elementos podem compartilhar da mesma classe, ao contrário do ID, que é único.

Exemplo:

Trecho do HTML:
```html
<p>Elemento sem classe</p>
<p class=”importante”>Elemento que será selecionado</p>
<h1 class=”importante”>Elemento que será selecionado</h1>
```

CSS:
```css
.importante {
    color: red;
}
```

####Descendentes
Cada espaço separa os elementos e vai aprofundando os elementos selecionados. Lemos da direita para a esquerda. O último exemplo abaixo significa que queremos pintar de vermelho os elementos a (link) dentro dos li (listas).

Exemplos:
```css
pai filho filho-do-filho {
    regra: valor;
}

li a {
    color: red;
}
```


Agora que já sabemos como selecionar um elemento específico no HTML, vamos às…

###Regras de estilo mais comuns

Antes, uma passada em dois conceitos muito importantes no design responsivo.

####Diferença entre EM, REM, % e PX

####Pixel
Provavelmente a unidade mais conhecida e também a maior inimiga do design responsivo. Pixels são unidades de medida exatas e fixas, ou seja, 16px serão sempre 16px, independente do tamanho da tela! A menos que você mude através de media queries o tempo todo para se adaptar. Utilize com moderação e mais especificamente para elementos que precisem de um tamanho exato.

####EM
É uma unidade de medida tipográfica, relativa. Traduzindo, um EM é do tamanho da largura da letra M maiúscula naquela fonte. A parte do “relativa” é um pouco mais complexa. Ela é relativa ao contexto em que está inserida.

![WAT?](http://garotasgeeks.com/wp-content/uploads/2014/04/wat-meme.jpg)

Ela é relativa como porcentagem, basta alguns cálculos para chegarmos ao nosso objetivo.

A fórmula é: objeto / contexto = resultado

Então, se eu quiser saber qual o tamanho em EMs de um parágrafo que hoje tem font-size: 12px, dentro de uma DIV que tem o font-size: 30px, faço o seguinte:

12px (objeto, parágrafo) / 30px (contexto, div) = 0.4em

Qual a utilidade disso?

Dessa forma eu posso alterar o tamanho de diversos elementos dentro dessa DIV mudando apenas o tamanho da sua fonte que o seus elementos filhos vão escalar proporcionalmente.

####REM
Mas dá pra simplificar.
Enquanto o EM é relativo ao elemento pai (que pode ser uma SECTION, um FOOTER, etc.), o REM é relativo à raiz, ou ROOT, que nesse caso vai ser sempre o BODY!
Ou seja, faço aquela conta ali de cima sempre com o mesmo contexto, que por padrão é 16px (tamanho da fonte no body). Com isso, se eu mudar o tamanho da fonte só do body, eu consigo fazer com que todo meu site se adapte proporcionalmente!

####%
A porcentagem aqui é o que todos já sabem. Nosso elemento vai se expandir e contrair de acordo com o percentual que definirmos.

Não veremos aqui ainda, mas saiba que existem outras medidas muito importantes também, como o vh, vw, vmin, vmax.

###Box model

**No CSS, todos elementos são caixas.**

![THAT'S ALL FOLKS. HAVE A NICE DAY.](http://assets.diylol.com/hfs/563/d00/a06/resized/serious-cat-meme-generator-that-s-all-folks-have-a-nice-day-c548d7.jpg)

Pronto, vamos todos pra casa. Só mais essa imagem e tudo ficará mais claro ainda. 

![Ilustração do box model. Margin, border, padding e content.](http://www.kuahla.com/learnhtml/images/boxmodel.gif)













