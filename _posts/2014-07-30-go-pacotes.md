---
layout: post
title:  "Iniciando com Go: Criando Pacotes"
date:   2014-07-30 15:21:07
categories: programming go
cover: "https://c2.staticflickr.com/8/7186/6830705590_ed04db9d17.jpg"
excerpt: "Como criar pacotes com Go? Do inicio a publicação"
---

Recentemente comecei a me aprofundar em Go, e vi a necessidade de criar alguns pacotes. Como eu vim de Node.js, sou acostumado a criar modulos pra resolver alguns pequenos problemas.

Vamos lá, com alguns passos simples é possível fazer nossos pacotes.

**1) Configure seu $GOPATH**

Você pode definir a variável de ambiente $GOPATH para qualquer pasta que você quiser. Se você trabalha em projetos maiores, é uma boa idéia criar um $GOPATH diferente para cada um deles. Eu recomendaria esta abordagem especialmente para a implantação, de forma que a atualização de uma biblioteca para o projeto A não quebra projeto B que pode exigir uma versão anterior da mesma biblioteca.
Observe também que você pode configurar seu $GOPATH a uma lista de pastas, delimitado por dois pontos. Então você pode ter um $GOPATH contendo todos os pacotes comumente utilizados, e GOPATHS separadas para cada projeto com pacotes adicionais ou diferentes versões de pacotes existentes.
Mas a menos que você está trabalhando em uma série de diferentes projetos Go simultaneamente, é o suficiente ter apenas um único $GOPATH localmente. Então, vamos criar um:

{% highlight bash linenos %}
mkdir $HOME/gopath
{% endhighlight %}

Em seguida, você precisa definir duas variáveis ​​de ambiente para contar a go tool onde ele pode encontrar pacotes Go existentes e onde ele deve instalar novos. A melhor forma é adicionar as duas linhas seguintes ao seu ~/.bashrc ou ~ /.profile (e não se esqueça de recarregar sua .bashrc depois).

{% highlight bash linenos %}
export GOPATH="$HOME/gopath
export PATH="$GOPATH/bin:$PATH
{% endhighlight %}



**2) Crie seu projeto**

Se você quiser criar um novo projeto Go, que sera hospedado no github.com mais tarde, você deve criar este projeto em $GOPATH/src/github.com/meunome/meuprojeto. É importante que o caminho corresponda a URL do repo github.com, porque a go tool vai seguir a mesma convenção. Então, vamos criar a raiz do projeto e inicializar um novo repositório git:

{% highlight bash linenos %}
mkdir -p $GOPATH/src/github.com/myname/myproject
cd $GOPATH/src/github.com/myname/myproject
git init
{% endhighlight %}
**3) Escreva sua aplicação**

Comece a programar e não se esqueça de git add e git commit em seus arquivos. Além disso, não use importações relativos como importação "./utils" para sub-pacotes. Eles estão atualmente em situação irregular e não deve ser usado em tudo, porque eles não vão trabalhar com a go tools. Use as importações como github.com/meunome/myproject/utils.

**4) Publique sua aplicação**

Criar um novo repositório no github.com, faça o upload de sua chave pública SSH se você não tiver feito isso antes e de um push suas alterações para o repositório:

{% highlight bash linenos %}
git remote add origin git@github.com:myname/myproject.git
git push origin master
{% endhighlight %}

Simples, não? agora você tem seu pacote Go publicado e pronto para compartilhar com a comunidade!
