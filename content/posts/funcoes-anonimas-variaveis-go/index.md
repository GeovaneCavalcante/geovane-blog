---
title: "Desvendando funções anônimas e variádicas em Go"
description: "Explorando os conceitos de funções anônimas e variádicas na linguagem Go"
date: 2024-03-21
categories: ["Desenvolvimento", "Go", "Programação"]
tags: ["Go", "Algorithms", "Function", "Programming"]
---

Funções são populares na maiorias da linguagens de programação. Elas oferecem maneiras de encapsular trechos de código que podem ser reaproveitados em partes distintas de um programa, possibilitando dividir grandes tarefas em partes menores, tornando-se um grande pilar na modularização.

Em Go, as funções têm uma estrutura de definição com o nome, uma lista de parâmetros de entrada especificando o nome e o tipo das variáveis. Estas variáveis recebem os valores dos argumentos passados na chamada da função e que tem escopo local, também uma lista de parâmetros de saída que podem ser capturados no retorno após a função ser executada. Confira o exemplo abaixo de uma função que recebe dois argumentos inteiros "a" e "b" e retorna a soma dos dois inteiros.

```go
func Sum(a int, b int) (int) {
    return a + b
}
```

Existem também outras maneiras também de fazer a declaração de funções, podendo fazer a omissão de alguns parênteses quando é retornando somente um valor, o agrupamento de variáveis de mesmo tipo na declaração de argumentos, também podendo ser agrupado a lista de retorno. Pode-se nomear os valores retornados na lista de retorno e fazendo a omissão dos valores na função "return".

```go
// Omitindo parêntese do retorno
func Sum(a int, b int) int {
    return a + b
}

// Agrupando variaveis por tipo
func Sum(a, b int) int {
    return a + b
}

// Parâmetro de retorno nomeado
func Sum(a int, b int) (c int) {
    c = a + b
    return
}
```

Um ponto interessante sobre a assinatura de função é que duas funções podem ter o mesmo tipo se elas tiverem a mesma sequência e tipo de entrada e a mesma sequência de tipos de resultado.

```go
package main

type TestFunc func(a int, b int) (int, int)

func Test(a, b int) (int, int) {
    return a + b, a - b
}

// função declarada com parâmetros de retorno nomeados
func Test2(a int, b int) (c int, d int) {
    c = a + b
    d = a - b
    return
}

func main() {
    var t TestFunc
    t = Test
    t(1, 2)

    // Atribuindo uma função com declaração diferente
    t = Test2
    t(1, 2)
}
```

Perceba a variável declarada com tipo "TestFunc" com uma assinatura de função com dois argumentos entrada inteiros e dois inteiros na saída. Logo abaixo são declaradas duas funções que contém os mesmos tipos de entradas e saídas mas não tem a mesma forma de declaração. Essas maneiras diferentes de declarar as funções não influenciam e respeitam a sua assinatura. Como na função "main", que uma variável "t" é declarada com o tipo acima e consegue receber as duas funções.

## Funções anônimas

As funções anônimas também são conhecidas como funções literais. Geralmente são utilizadas para encapsulamento de lógica ou representação de expressões. Também quando a função tem curto período de vida e não tem a necessidade de reaproveitamento em outro lugar. Elas são declaradas na forma de funções regulares mas sem nome, podendo ser atribuídas diretamente a variáveis ou como parâmetro pra funções de ordem superior.

```go
package main

import "fmt"

func main() {
    s := func(a, b int) int {
        return a + b
    }(2, 3)

    fmt.Println(s)
}
```

O exemplo acima declara uma função anônima de soma de dois números inteiros, perceba que deve ser omitido nome da função e que pode logo após sua declaração fazer a sua execução, passando em parênteses os argumentos necessários. Abaixo um outro exemplo do uso de uma função anônima no formato de parâmetro para uma função de nível superior.

```go
package main

import (
    "fmt"
)

// função que recebe um callback como argumento
func process(data string, callback func(string)) {
    // faz algo com os dados
    fmt.Println("Processando:", data)
    // chama o callback com os dados processados
    callback(data)
}

func main() {
    // chamada da função 'process' com um callback anônimo
    process("dados de teste", func(result string) {
        fmt.Println("Callback recebido:", result)
    })
}
```

## Funções Variádicas

As funções variádicas são funções que podem ser invocadas com um número variável de argumentos. Existem exemplos familiares na biblioteca padrão do Go, como a função "fmt.Println()", você pode passar uma infinidade de valores.

```go
package main

import "fmt"

func main() {
    fmt.Println("Teste", "Teste2")
    fmt.Println("Teste", "Teste2", "Teste3", "Teste4")
}
```

A declaração das funções variádicas tem um particularidade na sua definição.

```go
func fmt.Println(a ...any) (n int, err error)
```

Analisando a assinatura da função "Println" do pacote "fmt" percebe-se que existe um argumento "a" que é declarado com reticência e logo após seu tipo, "any". Essa declaração transforma essa variável em uma slice do tipo que pode ser iterada ou usada de acordo com o que uma slice do tipo permite.

```go
package main

import "fmt"

func variadic(x ...int) int {
    total := 0
    for _, v := range x {
        total += v
    }
    return total
}

func main() {
    fmt.Println(variadic(1, 2, 3, 4, 5, 6, 7, 8, 9, 10))

    xi := []int{1, 2, 3, 4, 5, 6, 7, 8, 9}
    fmt.Println(variadic(xi...))
}
```

Percebe-se que no exemplo acima a função "variadic" recebe um argumento na "x" do tipo inteiro, esse argumento é uma slice de inteiros. Na chamada função veja que pode-se passar valores separados por virgula como argumento da função ou passar um slice de inteiros seguindo por reticência a direita.

Um ponto de atenção é que embora uma função variádica transforme a variável em um slice do tipo definido, ela tem assinatura diferente de uma função que você declara o tipo explicitamente.

```go
package main

type TestFunc func(a ...int) int

func Test(a ...int) int {
    total := 0
    for _, v := range a {
        total += v
    }
    return total
}

func Test2(a []int) int {
    total := 0
    for _, v := range a {
        total += v
    }
    return total
}

func main() {
    var t TestFunc
    t = Test
    t(1, 2)

    t = Test2 //cannot use Test2 (value of type func(a []int) int) as TestFunc value in assignment
    t(1, 2)
}
```

## Referências

- [Introdução a Funções - IME USP](https://www.ime.usp.br/~leo/mac2166/2017-1/introducao_funcoes.html)
- [A Linguagem de Programação Go](https://novatec.com.br/livros/linguagem-de-programacao-go/)

Tags: Go, Algorithms, Function, Programming 