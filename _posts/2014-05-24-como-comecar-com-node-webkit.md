---
layout: post
title:  "Como começar com Node Webkit? Parte 1"
date:   2014-05-24 12:29:07
categories: programming javascript
cover: "https://cdn.tutsplus.com/net/uploads/2013/12/html5-node-webkit-retina-preview.png"
excerpt: "Como fazer apps desktop só com JavaScript?"
---
Como se não bastasse ser magico escrever JS no server e no front, agora tambem é possivel
escrever JS em apps desktop. Node Webkit, um projeto nascido dentro da Intel, teve seu codigo
aberto em 2011, e ganhou notoriedade esse ano com o projeto PopcornTime. O projeto provê a plataforma Node.js dentro do browser Webkit, que foi extendido
para dar poderes de manipulação do browser aos desenvolvedores que antes eram impossiveis.

###Como instalar?

O projeto pode ser instalado no OS X, Linux e Windows muito facilmente. Para tal, entre na seção de downloads do [projeto no github](https://github.com/rogerwang/node-webkit#downloads),
baixe o arquivo apropriado para você, extraia e se lembre do local onde ele está.
Agora precisamos achar o binario do node-webkit. No Linux, ele se chama **nw**, no Windows **nw.exe** e no OS X ele fica empacotado dentro do node-webkit.app (/path/to/node-webkit.app/Contents/MacOS/node-webkit).
No meu Macbook eu defini um **alias** pra facilitar. É só colocar isso no seu **.bash_profile** ou no **.bashrc**:
alias nw="/Applications/node-webkit.app/Contents/MacOS/node-webkit". Você pode substituir o caminho e apontar para o loca onde está o seu binario.

###Criando um app simples

Para quem já fez algo com Node.js, vai se familiarizar com a forma com que se cria projetos com node-webkit.
Como no Node, uma arquivo package.json é usabo pra descrever a aplicação. Nesse arquivo, o elemento 'main' especifica o ponto de entrada da aplicação e qual pagina o node-webkit deve exibir, por exemplo um "index.html". Como em um app usando Angular ou Ember,
esse arquivo só deve incluir CSS's e JavaScript's necessarios. O **package.json** tambem serve pra descrever, por exemplo, o tamanho da janela. Veja como ficaria:

{% highlight json linenos %}
{
  "name": "hello",
  "main": "index.html",
  "window": {
    "toolbar": false,
    "width": 800,
    "height": 600
  }
}
{% endhighlight %}
Agora no seu **index.html**, faça um HTML basico, com fins de exemplo:

{% highlight html linenos %}
<!DOCTYPE html>
<html>
  <head>
    <title>Meu Primeiro App Node Webkit</title>
  </head>
  <body>

  </body>
</html>
{% endhighlight %}

Pronto, agora só precisamos empacotar tudo em um arquivo com extensão **.nw**. Fazemos isso com o comando ``` zip -r my-first-app.nw *``` no Linux e OS X.
E usando o comando **nw** (definido no alias algumas linhas acima), eu faço isso ```nw my-first-app.nw``` e pronto! Nosso primeiro app com node-webkit rodando!

Eu sei, nada muito util. Mas na proxima parte vamos fazer uma integração com o twitter.
