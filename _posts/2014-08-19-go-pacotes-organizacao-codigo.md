---
layout: post
title:  "Go: Organizando e usando pacotes."
date:   2014-08-19 23:00:07
categories: programming go
cover: "https://pbs.twimg.com/media/Bgyw0Q2IIAAz9K7.jpg:large"
excerpt: "Vamos ver como criar pacotes para aplicações de larga escala"
---


Em um post anterior, falei em como criar pacotes com Go, mas muito superficialmente. De uns tempos pra cá, venho tendo a necessidade de criar estruturas para aplicações de larga escala, criando bibliotecas reutilizáveis e claro, usando pacotes de terceiros. Nesse post vou mostrar um pouco como organizar e reutilizar esses pacotes.

Toda aplicação Go é contida dentro de um **pacote** (``package``). Todo pacote deve estar dentro do ``$GOPATH`` e são nomeados de acordo com a pasta e arquivo em que está. Para carrega-lo em nosso código usamos `ìmport``.

{% highlight go linenos %}
package main
import (
  "fmt"
  "os"
  "strings"
 )

func main() {
  who := "World"
  if len(os.Args) > 1 {
    who = strings.Join(os.Args[1:], "")
  }
  fmt.Println("Hello", who)
}
{% endhighlight %}
Nesse exemplo fizemos o import de 3 pacotes da biblioteca padrão do Go. Podemos notar o uso do metodo ``Join``, do pacote ``strings`` e ``Args``, do pacote ``os``.

Agora vamos criar nossos próprios pacotes. O primeiro passo é criar um workspace. Dentro desse workspace vamos ter 3 pastas:  
``bin``: Aqui ficaram os executáveis.  
``src``: É onde seus pacotes vão sobreviver. Todo código .go vai ficar aqui.  
``pkg``: Algum pacote extra do SO.  

Quando você importa um pacote, o Go vai atras do pacote em cada workspace declarado no $GOPATH. O meu $GOPATH está setado para ``~/go``

Dentro de ``~/go/src`` crie ``foo/foo.go``, o abra em seu editor e edite:
{% highlight go linenos %}
package foo

import "fmt"

func Bar() {
	fmt.Println("Bar")
}
{% endhighlight %}
Geralmente, os arquivos que contem o pacote são nomeados de acordo com a pasta (o pacote e a pasta chamam-se ``foo`` e o arquivo ``foo.go``).

Para fazer o build desse código, basta rodar ``go build``, que vai gerar um binario executavel ``foer``.  Basta você rodar ``./foer`` que o resultado será
``bar`` impresso no terminal. Já para instalar o pacote e deixa-lo disponível globalmente, temos que executar ``go install``. O pacote estará em ``$GOPATH/bin/foer``.

Para usar pacotes de terceiro, vamos usar o comando ``go get``, que baixa a dependencia e a coloca dentro do nosso workspace. Vamos ver um exemplo com o Martini web framework.
{% highlight bash linenos %}
go get github.com/go-martini/martini
{% endhighlight %}
Edite o arquivo ``foo.go`` e adicione:
{% highlight go linenos %}
package main

import "github.com/go-martini/martini"

func main() {
  m := martini.Classic()
  m.Get("/", func() string {
    return "Hello world!"
  })
  m.Run()
}
{% endhighlight %}
E execute ``go run foo.go``, que já faz o build e executa o binário.

Bom, era mais ou menos isso que eu tinha pra falar. Vamos fazer mais coisas alem de scripts!
