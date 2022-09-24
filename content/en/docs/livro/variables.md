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

Existem algumas regras básicas para nomear variáveis. Essas regras também se aplicam aos nomes das functions. Certifique-se de segui-los ou seu código não compilará:

1. O nome ou o identificador pode conter letras, dígitos e *caracteres underscore* _. O C++ não define um limite no comprimento do nome.
2. O nome deve começar com uma letra ou o caracteres underscore.
3. C++ é *case sensitive*, o que significa que distingue entre letras maiúsculas e minúsculas. Por exemplo, a variável soma é diferente das variáveis Sum ou sUM.
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
Além disso, a palavra __export__ é reservada, enquanto as palavras __final__ e __override__ têm um significado especial, como veremos no Capítulo 20. A palavra __asm__ permite que o programador adicione código escrito em linguagem assembly. Este livro explica o significado de cada keyword, exceto __thread_local__. Só para saber, thread_local é usado para declarar variáveis locais em threads. Este livro não discute sobre este tópico. Depois de ler um livro que descreve a Standard Template Library (STL), você aprenderá sobre programação multithread.

5. Para evitar conflitos de nomes, não escolha nomes que comecem com um ou dois caracteres _, pois essas opções são reservadas para uso na biblioteca padrão. Além disso, não use nomes que o compilador usa, como nomes de funções de biblioteca ou variáveis (por exemplo, *cout*). Seu uso é permitido, mas é confuso e perigoso. Portanto, é mais seguro lidar com nomes predefinidos como se fossem palavras reservadas.

Além das regras fornecidas anteriormente, existem algumas convenções que são boas para seguir ao nomear suas variáveis. Embora não sejam impostas pelo compilador, essas “rules of thumb” tenderão a tornar seus programas mais fáceis de entender, bem como para aqueles que precisam ler seu código.

Use nomes descritivos para variáveis (claro, o mesmo se aplica a funções, tipos, …). É muito mais fácil ler um programa quando os nomes das variáveis indicam o uso pretendido. Por exemplo, se você usar uma variável que contém a soma de alguns números, dê a ela um nome como *sum* em vez de um nome irrelevante como i. Muitos programadores preferem usar letras minúsculas ao nomear variáveis e letras maiúsculas ao definir macros ou constantes. Nomes curtos (por exemplo, i) são geralmente usados como índices em arrays ou loops. Não dê nomes a variáveis que sejam ligeiramente diferentes (por exemplo, *more* e *More*); é muito fácil cometer um erro e usar uma variável no lugar da outra.

Quando necessário, não tenha medo de usar nomes longos para descrever o papel de uma variável. Se um nome de variável consiste em palavras, a prática usual é separá-las com o caractere underscore _ para melhor legibilidade. Por exemplo, você pode chamar uma variável que contém o número de dias *days_number*, em vez de *daysnumber*, ou algo menos legível. Em geral, seja qual for a abordagem escolhida, é bom ser consistente e aplicá-la ao longo do programa.

### Data Types

C++ fornece um conjunto de data types. Cada variável deve ter um type. O tipo determina a quantidade de memória alocada para a variável, o intervalo de valores que podem ser atribuídos a ela e o tipo de operações que podem ser aplicadas a ela. O tamanho dos tipos depende da implementação, ou seja, pode variar entre os diferentes sistemas. Os tipos de dados e seu tamanho usual em um sistema de 32 bits são mostrados na Tabela 2.1.

C++11 adicionou os seguintes tipos:

__char16_t__: Usado para armazenar conjuntos de caracteres de 16-bits, como **UTF-16**.

__char32_t__: Usado para armazenar conjuntos de caracteres de 32-bits, como **UTF-32**.

__long long int__: Usado para integers muito grandes (pelo menos 64-bits). É válido que **sizeof(long)** <= **sizeof(long long int)**

{{< alert icon="💡" text="O espaço de memória que um data type reserva pode variar de um sistema para outro. Por exemplo, o type __int__ pode reservar dois bytes em um embedded system ou um sistema mais antigo, quatro bytes ou oito bytes em um sistema moderno. Para saber o número de bytes que um data type reserva em seu sistema, use o operador __sizeof__, conforme discutido no Capítulo 4."/>}}

**Tabela 2.1**

```
____________________________________________________________________________

Data Type          Tamanho usual (Bytes)          Faixa de Valores (Min-Max)  
____________________________________________________________________________
bool                       1                               false/true
char                       1                               −128 … 127
wchar_t                    2                            −32.768 … 32.767
short int                  2                            −32.768 … 32.767
int                        4                     −2.147.483.648…2.147.483.647
long int                   4                     −2.147.483.648…2.147.483.647
float                      4                O menor valor possível: 1.17*10^-38
                                            O maior valor possível: 3.4*10^38

double                     8                O menor valor possível: 2.2*10^−308
                                            O maior valor possível: 1.8*10^308
long double              12, 16
unsigned char              1                                0 … 255
unsigned short int         2                               0 … 65535
unsigned int               4                            0 … 4.294.967.295
unsigned long int          4                            0 … 4.294.967.295

```

Os tipos __char__, __short__, __int__ e __long__ são usados para armazenar valores integer, que podem ser signed or unsigned. Se adicionarmos a palavra __unsigned__ a variável não possui sign bit e pode armazenar apenas valores positivos ou zero. A palavra __int__ pode ser omitida, por exemplo, __long__ em vez de __long int__. Além disso, as palavras podem ser misturadas em qualquer ordem, por exemplo, a declaração __unsigned long int__ a; é o mesmo que __int long unsigned__ a;.

Com exceção do tipo __char__, todos os outros tipos são signed por padrão. Nos signed types, o bit mais à esquerda é reservado para o sign. Se o número for negativo, seu valor é 1, caso contrário 0. A vantagem de __unsigned__ types é que eles têm um limite superior mais alto do que seus equivalentes signed, pois não precisam contabilizar valores negativos.

Os caracteres são representados por códigos numéricos específicos. O tipo char é normalmente usado para armazenar os códigos numéricos dos caracteres do conjunto básico, como o conjunto ASCII (por exemplo, ele inclui caracteres que aparecem no teclado, como dígitos, letras, sinais de pontuação, …). O tipo __wchar_t__ é usado para armazenar os códigos numéricos dos caracteres de um conjunto maior, como o Unicode.

O tipo char pode ser signed ou unsigned, depende da implementação. Portanto, se for importante para o seu programa, você deve escrever explicitamente __char signed__ ou __char unsigned__ em vez de __char__. Por exemplo, se escrevermos: 

```c++
char a = 255;
int b = a;
```
o valor de b não está especificado. Em um sistema onde o tipo __char__ é signed b torna-se -1, enquanto em outro onde o tipo __char__ é unsigned b torna-se 255.

O tipo __bool__ tem dois valores possíveis, __true__ e __false__. O literal __true__ é convertido em 1 quando convertido em um valor e __false__ em 0. Por outro lado, valores diferentes de zero são convertidos em __true__, enquanto um valor zero é convertido em __false__. Por exemplo:

```c++
bool b = 2; // b torna-se true.
int i = false; // i torna-se 0.
```
Normalmente, uma variável **bool** é usada para armazenar o resultado de uma ação, como se um valor é encontrado em uma array ou não.

Os tipos __float__, __double__ e __long double__ são usados para armazenar valores com uma parte fracionária, ou seja, números floating-point. Ao contrário dos integer types, os floating-point são sempre signed. Embora o tipo __long double__ normalmente forneça a mais alta precisão, raramente é usado porque a precisão dos tipos __float__ e __double__ geralmente é suficiente. 

Embora o C++ permita que cada implementação defina seus próprios tamanhos para os data types, ele impõe algumas restrições aos seus tamanhos mínimos. Especificamente, o tamanho do tipo __char__ deve ser de pelo menos 8 bits, o tamanho do __short__ pelo menos 16 bits e o tamanho do __int__ pelo menos igual ao do __short__. O tamanho do tipo __long__ deve ser de pelo menos 32 bits e pelo menos igual ao do tipo __int__. A seguinte ordem se aplica: __sizeof(char)__ <= __sizeof(short)__ <= __sizeof(int)__ <= __sizeof(long)__. O tamanho do tipo __wchar_t__ depende da implementação; no entanto, aplica-se: __sizeof(char)__ <= __sizeof(wchar_t)__ <= __sizeof(long)__. Se for importante economizar memória e os valores se ajustarem, use __short__ ao invés de __int__, pois seu tamanho geralmente é menor. Um exemplo típico é quando você tem uma grande matriz de integers.

Para os tipos floating-point, C++ especifica que o tamanho do tipo __long double__ deve ser pelo menos igual ao do __double__, e o tamanho do tipo __double__ deve ser pelo menos igual ao do __float__. Se você quiser aprender os tamanhos dos tipos integer e floating-point que seu sistema suporta, use o operador __sizeof__. Se você quiser saber mais sobre os type limits, leia os arquivos de cabeçalho *climits* e *cflat*. Além disso, você pode usar o arquivo de cabeçalho de *limits* e obter informações de type. Por exemplo, o proximo statement exibe o valor máximo do tipo __int__:

```c++
std::cout << "O valor máximo do tipo int é: " << std::numeric_limits<int>::max();
```

Para obter o valor mínimo, substituímos max() por min(). Se você deseja obter os valores máximos para outros data types, substitua o tipo int nos colchetes angulares(angled brackets) pelo tipo desejado.

{{< alert icon="💡" text="Se você não se importa com a precisão use o tipo __float__, pois normalmente ele reserva menos bytes e cálculos com números float tendem a ser executados mais rapidamente."/>}}

Vamos executar o seguinte programa. O operador == na instrução __if__ compara o valor de *a* contra 3.1. O que você acha que o programa exibirá, Sim ou Não?

```c++
#include <iostream> // Example 2.1.
int main()
{
  float a = 3.1;
  if(a == 3.1)
    std::cout << "Sim\n";
  else
    std::cout << "Não\n";
  return 0;
}
```
Embora a resposta óbvia seja Sim, o programa gerou Não ? Surpresa! E o motivo se deve à capacidade limitada do tipo __float__ para representar precisamente o número 3.1. Como veremos mais tarde, por padrão, o tipo de uma floating constant (por exemplo, 3.1) é __double__.



