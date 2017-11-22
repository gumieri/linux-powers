# _CLI_ powers

Uma das primeiras formas de se comunicar com computadores foi através de texto.
Estes primeiros terminais eram conectados a impressoras de telégrafo ([teletipos](https://pt.wikipedia.org/wiki/Teletipo)) que imprimiam em papel o que lhes era pedido.
Até hoje pode-se encontrar resquício disso, o termo _tty_ é uma abreviação para teletipo (_teletype_ em inglês) que também é um nome para terminal.

Mais tarde, monitores com a tecnologia de [tubos de raios catódicos (CRT)](https://pt.wikipedia.org/wiki/Tubo_de_raios_cat%C3%B3dicos) foram conectados a computadores.
A transição foi simplesmente trocar o papel pela tela. Ao invés de imprimir em tinta, imprimia-se no monitor.
As vantagens mais óbvias estavam na economia de papel e velocidade em que a informação era impressa na tela.

Como a programação consiste em escrever textos para serem interpretados por computadores,
essa interface de comandos, há tanto tempo criada, ainda se mostra bastante prática.

## _Shell_

A camada responsável por interpretar os comandos do usuário para a máquina é chamada de _shell_ (concha ou casca).
O _shell_ encobre a camada mais baixa de um sistema operacional, o seu _kernel_, escondendo suas complexidades e dos detalhes técnicos de sua interface.

Existem várias implementações diferentes de _shells_, a mais antiga era chamada somente de _shell_ foi distribuido no _Unix_ de 1971 a 1975.
Porém este _shell_ foi completamente reescrito por Setephen Bourne e distribuido a partir de 1979 no _Unix_, esta implementação é chamada de _Bourne Shell_.

Atualmente existem diversos _shells_, o mais comum sendo o `bash` ou _Bourne Again Shell_ que é uma brincadeira com o termo _Born again_ ("nascido de novo" em inglês).

## `bash`

A linguagem de comandos `bash` está presente na maioria dos sistemas operacionais descendentes ou inspirados no _Unix_ como _shell_.
O _macOS X_ e diversas distribuições _Linux_ são exemplos desses sistemas.

Então é pelo `bash` que temos uma interface de comunicação com o computador, através de comandos implementados neste _shell_ podemos interagir com a máquina.

[Mais…](shell/bash.md)

## Comandos

Todo comando é um programa que pode ser chamado pelo `bash`.
Estes comandos ficam instalados em locais especificos do sistema em que o `bash` está configurado para buscar.

A maioria destes comandos terão nomes extremamente curtos para serem rápidos de digitar.

[Mais…](shell/bash.md)

## `ls`

O comando `ls` lista o conteúdo do diretório.
Se você acabou de abrir o seu emulador de terminal, provavelmente o que lhe será apresentado como reposta é o conteúdo de seu diretório _home_.

![ls no diretório home](media/ls.gif)

Este diretório que é seu "lar" (_home_) é representado também como til (`~`).
O motivo para isto é histórico, os teclados dos anos 70 (ADM-3A) para se digitar o til utilizava-se a tecla _home_.

[Mais…](file-system/ls.md)

## Parâmetros

Ou também chamados de argumentos, são valores informados à direita de algum comando.
estes parâmetros são repassados para o comando que tem então seu comportamento alterado.

O uso de parâmetros é bastante intuitivo,
cada palavra ou número separada por um ou mais espaços em branco (` `) será considerada um parâmetro diferente.

Existem outros caracteres que tem uma importância especial para o `bash`, que vai além do seu significado literal.
Portanto são tratados de uma forma diferenciada e não são repassados como parâmetros.
Para ver a lista completa destes caracteres, veja a sessão de [caracteres especiais para o bash](shell/bash.md#caracteres-especiais).

Nos casos onde algum destes caracteres deveria fazer parte do parâmetro que você quer passar, a solução é simples:
basta colocar o parâmetro todo entre aspas simples (`'`), exemplo:
```bash
echo 'Olá mundo!'
```

Outra forma de fazer o mesmo é utilizando a barra invertida (`\`) antes do caractere que deveria ser ignorado por esse tratamento especial do `bash` e só repassada adiante.
Exemplo:
```bash
echo Olá\ mundo\!
```

Neste exemplo, o espaço logo após a palavra `Olá` está sendo ignorado pelo interpretador `bash` e simplesmente entendido como parte do parâmetro, da mesma forma que o ponto de exclamação.
Por causa deste comportamento, a barra invertida também é chamada de caractere de escape.

[Mais…](shell/bash.md)

## Estrutura de diretórios

Diretórios (ou pastas) no _Linux_ e nos _Unix_ são bastante diferentes do _Windows_.
Por exemplo, quando um _pendrive_ é conectado ele não vai aparecer como um novo disco, não existe sequer um `C:\`.
Pode-se parecer desnecessário e confusa a complexidade da estrutura de diretórios dos _Linux_ e _Unix_,
porém essa mesma complexidade permite uma maleabilidade enorme destes sistemas quando se trata de gerenciamento de discos e arquivos.

A estrutura de diretórios nos _Linux_ e _Unix_ consiste em um diretório raíz (em inglês: _root_) que é onde todos os outros diretórios e arquivos podem ser criados.

O diretório raís é referenciado por uma barra (`/`) e a partir dele é possível chegar a qualquer arquivo ou outro diretório dentro do sistema.

O diretório _home_ que é representado pelo `~` (til) encontra-se pelo caminho `/home/` e tem o nome de seu usuário, que seria por exemplo `/home/powers/` para um usuario nomeado _powers_,
Para o usuário _powers_, o `~` referencia este diretório.
Estes são caminhos "absolutos", tem essa denominação pelo motivo de que estes caminhos indicam como chegar a um diretório (ou arquivo) a partir da raís do sistema.
Isso porque este caminho (ou _path_, em inglês) inicia com `/`, sem qualquer palavra antes desta barra, a única referencia que se pode assumir é que esta é a referencia à raís.

Um caminho como `Documents/arquivo_de_texto.txt` é chamado de caminho "relativo" por não apresentar o "trajeto" inteiro desde a raís do sistema, dessa forma este caminho será relativo à algum outro local.
Caminhos relativos fazem sentido por exemplo quando você quer abrir um diretório ou arquivo logo onde você está, sem ter que referenciar todo o caminho novamente a partir da raís.

Existem mais dois pontos a serem abordados sobre caminhos relativos:
1. o `.` (ponto);
2. e o `..` (ponto duplo, ou ponto-ponto).

O `.` é uma referência ao diretório atual, considerando que você esteja em `/home/powers/Documents/`, o `.` é uma referência para este diretório.

Enquanto o `..` é uma referência ao diretório "pai" (ou _parent_), o diretório que contém o diretório atual, neste caso seria o `/home/powers/`.

Todo diretório possui uma referência a ele mesmo (`.`) e ao seu _parent_ (`..`), no caso do diretório `/`, seu parent é ele mesmo.
O `.` é muito utilizado em casos que queremos executar algum arquivo que está logo no diretório que estamos:

```bash
./faz_pizza
```
Neste exemplo, existe um arquivo executável chamado `faz_pizza` no diretório que estamos e para poder executá-lo, precisamos informar que estamos executando algo do diretório atual.
Isso acontece por questões de segurança, executar alguma coisa sempre envolve algum risco e esta característica traz clareza a o que o usuário está querendo executar.

## `cd`

Para navegar por estes diretórios existe o comando `cd` (_change directory_).
Ele aceita um parâmetro, o diretório para o qual você pretende ir.

Por exemplo, para navegar até o diretório raíz, basta digitar o exemplo abaixo e apertar `↵` (_Enter_) ao final:
```bash
cd /
```

Caso você não passe nenhum parâmetro para o comando `cd` o que irá acontecer é que você será levado ao seu diretório _home_.
Isso porquê o valor padrão para o parâmetro deste comando é o seu _home_. Exemplo:
```bash
cd
```

```bash
cd ..
```

```bash
cd -
```

## `pwd`

## _Autocomplete_

## `file`

## `locate`

- `updatedb`

## `mv`

## `cp`

## `rm`

## `mkdir`

## `rmdir`

## `touch`

- atualiza a data de edição de um arquivo

- caso não exista o arquivo requisitado, cria o arquivo vazio

## `history`

## Control C

## `whatis`, `man`

## _Flags_

## _Status_ que os comandos retornam
