# Conteúdo

- Plataforma de desenvolvimento .NET
- Estrutura de projetos em C#
- Tipos de variáveis
- Operações Aritméticas
- Hello World! em C#

# DotNet

Plataforma de desenvolvimento criada pela Microsoft, após um acordo com a Sun Microsystems, era usado Java para desenvolver porém não possuía uma boa compatibilidade com as bibliotecas de código nativo do ambiente Windows, o que motivou a Microsoft a desenvolver sua própria implementação do Java chamado J++ juntamente com a IDE para desenvolvimento Visual J++

J++ era de domínio da MS e só podia ser usada nesse ambiente, o que violava um acordo com a Sun, a MS deu início à criação de sua própria plataforma de desenvolvimento.

## Plataforma de desenvolvimento:

1. Conjunto de linguagens de programação
2. Bibliotecas em ambientes de desenvolvimento disponibilizado de forma unificada para uso, podendo ser oferecidas como um produto ou não, facilitam o desenvolvimento em algum contexto especifico ou multicontexto.

DotNET oferece:

- Suporte a 3 linguagens de programação: C#, F# e VB
- Linguagem intermediária, permitindo que todas as bibliotecas sejam compartilhadas entre suas linguagens e ambientes, facilitando o desenvolvimento em seus contextos;
- O Unity, para programação de jogos.
- O Azure para aplicações em nuvem;
- Suporte para aplicações IoT e diversos outros serviços.

## O que é o DotNET?

Nasceu suportando múltiplas linguagens, tem como ideia principal, que toda linguagem aceita compartilhar as mesmas bibliotecas, facilitando assim a migração e compartilhamento de código entre si.

Suas primeiras versões eram em código fechado para ambientes Windows, e com o tempo a MS, tornou-a gratuita e de código aberto, sob a licença MIT e Apache 2.

## O que criar com DotNET?

Tendo em mente que é a principal plataforma de desenvolvimento da MS, seus principais usos são em:

- APIs da Web
- Aplicativos com Aprendizado de Máquina
- Aplicativos de console
- Aplicativos Desktop Windows
- Aplicativos em Internet das Coisas (IoT)
- Aplicativos em Nuvem
- Aplicativos móveis
- Aplicativos Web
- Aplicações em servidor, na nuvem
- Jogos
- Microsserviços

## Instalando o DotNET Core no Linux

Verificar pacotes instalados dotnet:

```
apt list --installed "dotnet*"
```

Remover pacotes existentes para instalar pacotes específicos:

```
sudo apt-get remove 'dotnet*'
```

Realizar update no sistema:

```
sudo apt-get update
```

Instalando runtime dotNET:

```
sudo apt install aspnetcore-runtime-6.0
```

Após instalação verificar os pacotes instalado usando apt list.\

Agora instalar o SDK dotNET, para desenvolvimento dos aplicativos na plataforma:

```
sudo apt install dotnet6
```

Verificar se foi instalado com sucesso:

```
dotnet --info
```

