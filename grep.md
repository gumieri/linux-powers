# Comando `grep`

A história do `grep` é um tanto antiga. Nascido no UNIX e hoje presente em praticamente todos os sistemas _unix-like_ (Linux, MacOS, FreeBSD, etc).
Portanto, é uma ferramenta que você terá acesso com bastante facilidade. Esta ferramenta serve para buscar um padrão, uma palavra ou texto dentro de arquivos e _streams_.

## Os parâmetros

Para utilizar este comando, deve-se informar o que deseja-se buscar e onde (sendo o onde opcional dependendo da situação):
```bash
grep 'string a ser buscada' arquivo/em_que_deseja-se/buscar/a_string.md
```

As duas informações mostradas acima são parâmetros, que são separados por espaço.
Caso haja espaço ou outro caracter especial que deva fazer parte do parâmetro, recomenda-se coloca-los entre aspas (como demonstrado acima).
Uma alternativa as aspas pode ser também escapar o espaço ou caracter especial com a barra invertida (`\ `):

```bash
grep string\ a\ ser\ buscada arquivo/em_que_deseja-se/buscar/a_string.md
```

O segundo parâmetro é opcional devido alguns comportamentos em combinação com o `grep`.
Você pode jogar o _output_ de algo para o `grep` filtrar:
```bash
ps aux | grep node
```
(ver as linhas dos processos onde contém a string 'node' no meio)

Pode-se passar um conjunto de arquivos para ele buscar, como:
```bash
grep asdf *.txt
```

## As _flags_

Ou também poderá buscar recursivamente em todos os arquivos com a _flag_ `-r`:
```bash
grep -r asdf diretorio/do/projeto
```

O problema é que nesses casos a gente quer ignorar diretórios como `.git` ou `node_modules`.
Portanto, podemos informar quais diretórios não queremos:
```bash
grep -r diretorio/do/projeto --exclude-dir={.git,node_modules,log,tmp}
```

Uma _flag_ é uma configuração que é passada para o comando, essas opções se diferenciam de parâmetros por um ou dois sinais de menos (`-` ou `--`)).

Para programadores a _flag_ `-n` é interessante também, pois ela apresenta o número da linha em encontrada dentro do arquivo.

O grep é "case sensitive", ou seja, diferencia caracteres maiúsculos e minúsculos.
Para não diferenciar existe a _flag_ `-i`.

A _flag_ `-v` (ou `--invert-match`) é útil para quando você quer todas as linhas que não coincidem com o padrão buscado, invertendo a busca.

Outra coisa muito bacana são as _flags_ `-A`, `-B` e `-C`
Eles recebem um numero que corresponde às linhas após (`-A` After), antes (`-B` Before) ou tanto antes quanto depois (`-C` Context) do que você está buscando.
```bash
grep asdf *.txt -C 5
```

Como o uso padrão do `grep` é para encontrar a linha contendo a _string_ buscada, o comando normalmente retorna a linha inteira destacando a parte buscada.
Porém é possível retornar somente o padrão buscado, o que faz sentido em casos de busca por regex onde a intenção é encontrar este padrão para usa-lo em algum outro local.
Para isso existe a _flag_ `-o` (ou `--only-matching`).
```bash
ls -l jars/*.jar | grep -Eo '([0-9]+)\.([0-9]+)\.([0-9]+)(?:\.(R[0-9]+))?')
```
(exemplo buscando a versão definida no nome de algum arquivo `jar` no padrão `11.22.33.R44`)

Note que caso o comando `grep` não encontre qualquer resultado o retorno será um erro, permitindo assim utilza-lo para operações lógicas que só devem ser executadas caso o `grep` encontre algo:
```bash
grep 'padrão' arquivo.txt && echo 'encontrou' || echo 'não encontrou'
```
## Conclusão

Resumindo, se você precisa buscar por uma _string_ dentro de arquivos, o `grep` dá conta do recado.
Qualquer dúvida consulte a ajuda do comando (`grep --help`) ou o manual (`man grep`).

## Extra
Atualmente existem alternativas com melhor perfomance em relação às buscas e opções:
- `ack` ([beyondgrep](https://beyondgrep.com/)) é quem procurou reinventar o `grep`, sendo recursivo por padrão e evitando diretórios dos controladores de versão (como o `.git`);
- `ag` ([the silver searcher](https://github.com/ggreer/the_silver_searcher)) veio após o `ack`, mas é facilmente instalável nos servidores, como o _CentOS_, onde basta instalar usando o `yum` pelo nome `the_silver_searcher`;
- `rg` ([ripgrep](https://github.com/BurntSushi/ripgrep)) é o mais novo entre estes, feito em _rust_ e é mais o rápido. Prometendo um nivel de compatibilidade tanto com `grep` quanto com o `ag`.
