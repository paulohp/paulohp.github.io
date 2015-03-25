---
layout: post
title:  "Parseando paginas <br> HTML com D"
title_p:  "Parseando paginas HTML com D"
date:   2015-03-25 00:00:00
lang: pt
categories: programming dlang
cover: "http://www.bitwisemag.com/images/illustrations/cover/12/d_language_cover.jpg"
excerpt: "Aprenda algo novo por diversão, deixe o mimimi para os outros"
---

Se tem uma coisa que eu gosto muito de fazer é aprender coisas novas. E a área de tecnologia me permite fazer isso bem.

Sempre que vou aprender uma linguagem de programação nova, eu tento fazer algo divertido antes de sair lendo livros e etc. A partir dai eu ja sei mais ou menos se vou me dedicar ou não a esses estudos. A primeira coisa que eu faço é um ‘crawlerzinho’, como eu gosto de chamar, que basicamente entra em um site qualquer e extrai informações que eu preciso.

Então vamos nessa. Vou levar em conta que você tenha o ambiente do D instalado, mas se não tiver, [pode ver aqui](http://dlang.org/). Suponhamos que eu quero extrair o titulo deste post. A biblioteca padrão do D não nos oferece um bom pacote para isso, portanto precisamos buscar na comunidade. No [github do Adam Ruppe](https://github.com/adamdruppe/arsd), um cara muito foda em D, tem algumas libs bem interessantes. Por enquanto vamos baixar os arquivos `dom.d`, `characterencodings.d`, e `curl.d` do repositorio dele. Com os arquivos em baixados, vamos criar nosso `crawler.d`:

{% highlight d linenos %}
import arsd.dom;
import arsd.curl;
import std.stdio;

void main() {
  auto document = new Document();
  document.parseGarbage(curl("http://google.com"));

  writeln(document.querySelector("a"));
}
{% endhighlight %}

E para compilar você pode fazer isso:

```rdmd crawler.d dom.d characterencodings.d curl.d```

Você precisa da biblioteca cURL instalada. Se você usar um computador com algum OS baseado em UNIX, como o Linux ou MacOS, não se preocupe, provavelmente ela já esta instalada. Mas se você estiver no Windows, a internet deve ter alguma ajuda pra você.

Nas três primeiras linhas fazemos o import das bibliotecas baixadas anteriormente, mais a biblioteca de io padrão do D.
{% highlight d linenos %}
import arsd.dom;
import arsd.curl;
import std.stdio;
{% endhighlight %}

Em seguida definimos nossa função `main`, onde criamos uma instancia no `dom.d` e atribuímos ela a `document`. A função `parseGarbage` limpa o html baixado com o ```curl("http://kirk.svblte.com/")```. A lib `dom.d` contem um monte de funções legais pra poder trabalhar com manipulação do DOM, tipo `getElementeById` e `querySelectorAll`. E finalmente é usado o `writeln` para imprimir o HTML no console.

Bom, era isso que eu tinha pra mostrar pra vocês, em breve vou postando mais textos sobre a D. 
