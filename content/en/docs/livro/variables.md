---
title: "Variáveis, Constantes e Conversões Aritméticas"
description: "Neste capítulo, aprenderemos os basic types de dados e veremos como podemos usá-los para declarar variáveis em nosso programa. À medida que avançamos para os próximos capítulos, aprenderemos como construir composite types baseados nos basic types, como arrays e structures. Este capítulo também discute conversões aritméticas e variáveis constantes."
lead: "Neste capítulo, aprenderemos os basic types de dados e veremos como podemos usá-los para declarar variáveis em nosso programa. À medida que avançamos para os próximos capítulos, aprenderemos como construir composite types baseados nos basic types, como arrays e structures. Este capítulo também discute conversões aritméticas e variáveis constantes."
date: 2022-09-23T13:43:16-03:00
lastmod: 2022-09-23T13:43:16-03:00
draft: false
images: []
menu:
  docs:
    parent: ""
    identifier: "variables-5ed808dcc26868cb2b47f4c0908980e6"
weight: 200
toc: true
---

## Variáveis
____

A RAM do computador (Read Access Memory) consiste em milhões de células de memória sucessivas que são usadas para armazenar dados. O tamanho de cada célula é um byte. Por exemplo, um PC com 8 GB (gigabytes) de RAM teria 8 × 1024 MB = 8 × 1024 × 1024 KB = 8 × 1024 × 1024 × 1,024 bytes = 8,589,934,592 células de memória.
Uma *variável* é um local de memória com um determinado nome (por exemplo, i). O valor de uma variável é o conteúdo de sua mémoria de localização (por exemplo, 10). Quando queremos acessar esse valor, usamos o nome da variável (por exemplo, i).

### Nomendo Variáveis

Existem algumas regras básicas para nomear variáveis. Essas regras também se aplicam aos de nomes de functions. Certifique-se de segui-los ou seu código não compilará:

1. O nome ou o identificador pode conter letras, dígitos e *caracteres underscore* _. O C++ não define um limite no comprimento do nome.
2. O nome deve começar com uma letra ou o caracteres underscore.
3. C++ faz distinção entre maiúsculas e minúsculas, o que significa que distingue entre letras maiúsculas e minúsculas. Por exemplo, a variável soma é diferente das variáveis Sum ou sUM.
4. As keywords a seguir não podem ser usadas como nomes de variáveis porque têm um significado especial para o compilador C++.

```s
and       const_cast      friend       or_eq         template     volatile
and_eq    continue        goto         private       this         wchar_t
asm       default         if           protected     throw        while
auto      delete          inline       public        true         xor
bitand    do              int          register      try          xor_eq
bitor     double          long         reinterpret_cast
bool      dynamic_cast    return       typedef
break     else            mutable      short         typeid
case      enum            namespace    signed        typename
catch     explicit        new          sizeof        union
char      extern          not          static        unsigned
class     false           not_eq       static_cast   using
compl     float           operator     struct        virtual
const     for             or           witch         void
```

O C++11 também reserva as keywords a seguir:

```s
alignas  alignof  constexpr  char16_t  char32_t  decltype  noexcept  nullptr
static_assert  thread_local
```
Além disso, a palavra __export__ é reservada, enquanto as palavras __final__ e __override__ têm um significado especial, como veremos no Capítulo 20. A palavra __asm__ permite que o programador adicione código escrito em linguagem assembly. Este livro explica o significado de cada palavra-chave, exceto __thread_local__. Só para saber, thread_local é usado para declarar variáveis locais em threads. Este livro não discute sobre tópicos. Depois de ler um livro que descreve a Standard Template Library (STL), você aprenderá sobre programação multithread.

5. Para evitar conflitos de nomes, não escolha nomes que comecem com um ou dois caracteres _, pois essas opções são reservadas para uso na biblioteca padrão. Além disso, não use nomes que o compilador usa, como nomes de funções de biblioteca ou variáveis (por exemplo, *cout*). Seu uso é permitido, mas é confuso e perigoso. Portanto, é mais seguro lidar com nomes predefinidos como se fossem palavras reservadas.

Além das regras fornecidas anteriormente, existem algumas convenções que são boas para seguir ao nomear suas variáveis. Embora não sejam impostas pelo compilador, essas “rules of thumb” tenderão a tornar seus programas mais fáceis de entender, bem como para aqueles que precisam ler seu código.

Use nomes descritivos para variáveis (claro, o mesmo se aplica a funções, tipos, …). É muito mais fácil ler um programa quando os nomes das variáveis indicam o uso pretendido. Por exemplo, se você usar uma variável que contém a soma de alguns números, dê a ela um nome como *sum* em vez de um nome irrelevante como i. Muitos programadores preferem usar letras minúsculas ao nomear variáveis e letras maiúsculas ao definir macros ou constantes. Nomes curtos (por exemplo, i) são geralmente usados como índices em arrays ou loops. Não dê nomes a variáveis que sejam ligeiramente diferentes (por exemplo, *more* e *More*); é muito fácil cometer um erro e usar uma variável no lugar da outra.

Quando necessário, não tenha medo de usar nomes longos para descrever o papel de uma variável. Se um nome de variável consiste em palavras, a prática usual é separá-las com o caractere underscore _ para melhor legibilidade. Por exemplo, você pode chamar uma variável que contém o número de dias *days_number*, em vez de *daysnumber*, ou algo menos legível. Em geral, seja qual for a abordagem escolhida, é bom ser consistente e aplicá-la ao longo do programa.

### Data Types