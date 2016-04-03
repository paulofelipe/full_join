---
layout: post
title: "Kit de Sobrevivência em R - Parte 3"
date: 2016-03-28 22:10:52 -0300
comments: true
categories: [básico, r]
---


Neste post, você aprenderá um pouco sobre os pacotes, trabalhará com o console para fazer algumas operações e ir se familiarizando mais com o R. Aprenderá como usar as funções disponíveis no R e as funcões adicionais em pacotes.

<!-- More -->

## Pacotes

Um pacote do R e um conjunto de funções que tem uma temática em comum. As funções de um mesmo pacote são carregadas juntas em memória, ou seja, ficam disponíveis para uso no R. Por ter uma temática específica, cada pacote possue uma documentação explicando suas funcionalidades disponíveis e como usá-las. Além das funções, alguns pacotes também fornecem um conjunto de dados que são usados para replicar os exemplos fornecidos nas documentações.

Por exemplo, o `dplyr` é um pacote que possui um série de funções que facilitam consideravelmente a manipulação de dados. Já o `readxl` é um pacote com várias funções para leitura de arquivos excel. E o `ggplot2`, um pacote para criação de gráficos.

No geral, você fará muito uso de pacotes para facilitar tarefas que as funções básicas do R deixam a desejar.

### Instalação

Existem duas opções para instalar um pacote: via comando ou usando a funcionalidade nos menus do RStudio.

Para instalar via comando, você pode digitar o seguinte comando no console:


{% highlight r %}
install.packages('readxl')
{% endhighlight %}

Este comando irá instalar o pacote `readxl` que fornece funções para facilitar a importação de dados em arquivos `xls` e `xlsx`. Nesse caso específico, o pacote fornece duas funções: uma para listar todas as planilhas que estão em um arquivo do excel e outra para ler os dados de uma planilha pro excel. Em um post futuro sobre a importação de dados, trataremos mais sobre esse pacote. Por enquanto, estamos usando somente como exemplo.

Para realizar a instalação com ajuda do RStudio, primeiro clique na aba _Packages_ e depois no botão _Install_. Será aberta uma janela auxiliar em que você poderá escolher a fonte que será utilizada para instalar o pacote. Normalmente, você optará pelo CRAN (este termo será explicado mais adiante, porém trata-se do repositório oficial). Em _Packages_, digite o nome do pacote e depois no botão _Install_. Abaixo está uma imagem de como é o processo de instalação via RStudio.

![alt Instalação de Pacote](/images/install_package.gif "Instalação de Pacote")

### Buscando pacotes

Mas como saber quais pacotes estão disponíveis para uma determinada tarefa? Na maioria das vezes será inevitável realizar uma busca por uma função específica e no meio do caminho se deparar com o pacote. 

Todavia, existem algumas páginas que apresentam uma lista de pacotes relacionadas a uma determinada tarefa, que são denominadas de _Task View_. Para exemplificar, veja [aqui](https://cran.r-project.org/web/views/Graphics.html) uma lista de pacotes para realização de gráficos e visualizações. 


### Carregando um pacote

Para utilizar as funções de um pacote, você deve carregá-lo antes. Para isso, você deve usar o seguinte comando:

{% highlight r %}
library(readxl)
{% endhighlight %}

Esse comando irá carregar o pacote em memória e tornará possível a utilização de todas funções disponíveis nele. Também existe a possibilidade de carregamento de pacotes usando a função `require()`, que é mais indicado no caso de carregamento de um pacote dentro de uma rotina. Por enquanto, não nos preocupemos com ele.

>Dica: repare que para instalar o pacote você usou o nome dele entre aspas `install.packages("readxl") e não vai funcionar sem aspas. Mas, para carregar o pacote em memória, você pode usar com ou sem aspas library(readxl) ou library("readxl")

Ao trabalhar com pacotes, muitas vezes irá aparecer o termo **CRAN**. Ele significa _Comprehensive R Archive Network_. Este é o principal repositório de pacotes do R. Trata-se de um portal que guarda uma série de pacotes que necessariamente passaram por uma série de requisitos antes de serem publicado. Atualmente, estao disponiveis mais de 8.000 pacotes no CRAN. 

Este é o único local onde os pacotes estão disponíveis? Não! 

Vários pacotes já são disponibilizados pelos próprios autores antes mesmo das verificações necessárias para entrar no CRAN. Não são apenas novos pacotes. Novas versões de um pacote podem se encaixar aqui também. Geralmente, eles estão disponíveis no [github](https://pt.wikipedia.org/wiki/GitHub). 

Para realizar a instalação desses pacotes "fora do CRAN", será necessária a instalação do `devtools` (que é um pacote!). Por exemplo, o `ggplot2`, ótimo pacote para gráficos, já possui uma versão estável no CRAN. No entanto, se você desejar instalar a versão que está em desenvolvimento, que pode possuir uma nova funcionalidade, faça o seguinte:

{% highlight r %}
install.packages('devtools') # Caso não esteja instalado ainda
devtools::install_github("hadley/ggplot2")
{% endhighlight %}

Aqui temos um ponto interessante. Para usar funções de um pacote, usualmente carrega-se usando o `library()`. Contudo, se você quiser pontualmente uma função de um pacote, pode-se optar pela forma acima: `nome_do_pacote::nome_da_função`. Dessa forma você evitaria carregar todas as funções do pacote em memória. Isso pode ser muito útil!

## Ajuda no R

Você baixou um pacote e não sabe muito bem como usar as funções que estão disponíveis. O que fazer? Você precisará de ajuda. O primeiro passo é verificar a ajuda do pacote. Serão listadas as funções disponíveis e links para a página de _help_ de cada função. Isto pode ser feito a partir do seguinte comando:


{% highlight r %}
help(package = 'readxl')
{% endhighlight %}

Para buscar ajuda sobre uma função específica, existem algumas possibilidades a depender se o pacote já está carregado ou não. Por exemplo:


{% highlight r %}
?read_excel # se o pacote já estiver sido carregado com library(readxl)
?readxl::read_excel # Se o pacote não estiver carregado
??read_excel  # Pacote não carregado. Demora mais para apresentar um resultado
{% endhighlight %}

É importante destacar o `??`, que faz uma busca mais ampla por funções, demonstrações e arquivos que trazem uma visão geral (vignette) de algum pacote/função.

Sendo mais específico, ao buscar a ajuda por uma função específica, será apresentado um texto com uma estrutura padrão: _Description_, _Usage_, _Arguments_ e _Examples_. Além dessas, podem constar outras seções como _Details_ e _Value_, por exemplo. 

É importante destacar o uso (_Usage_) que trará uma forma genérica de utilização dos parâmetros. Em regra, uma função tem uma série de parâmetros que serão passados para "dentro" dela. Os parâmetros são separados por vírgula e os que apresentam `=` possuem um valor padrão e geralmente são opcionais (nem todos os parâmetros são obrigatórios). 

Após executar uma função, ela retornará o que está descrito na seção _Value_. Pode ser um único número ou uma lista (nos próximos posts ficará mais claro o que é uma lista) de elementos que pode variar de uma vetor a um texto.

Não se preocupe muito se o conceito de função ainda não está totalmente claro. O próprio uso e os próximos posts deixarão todos esses conceitos claros de forma natural por meio de exemplos e práticas. 

## Referências:
* [DataCamp - Functions](https://www.datacamp.com/community/tutorials/functions-in-r-a-tutorial)
* [Principais pacotes para R](https://www.rstudio.com/products/rpackages/)
* [R Packages](http://r-pkgs.had.co.nz/)
* [Lista de pactes mais úteis para Análise de Dados](http://www.analyticsvidhya.com/blog/2015/08/list-r-packages-data-analysis/)