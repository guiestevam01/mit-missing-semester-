```markdown
# ./missing-semester aulas passado sobre

## Visão Geral do Curso + Introdução ao Shell

### Quem somos nós?

Esta aula é lecionada em conjunto por Anish, Jon e Jose. Somos todos ex-alunos do MIT que iniciamos esta aula do MIT IAP quando éramos estudantes. Você pode nos contatar coletivamente em missing-semester@mit.edu.

Não somos pagos para lecionar esta aula e não monetizamos a aula de forma alguma. Disponibilizamos todo o material do curso e as gravações das aulas gratuitamente online. Se você quiser apoiar nosso trabalho, a melhor maneira de fazer isso é simplesmente espalhar a palavra sobre a aula. Se você é uma empresa, universidade ou outra organização que executa este conteúdo para turmas maiores, por favor, envie-nos relatórios de experiência/testemunhos por e-mail para que possamos ouvir sobre isso :)

### Motivação

Como cientistas da computação, sabemos que os computadores são ótimos em auxiliar em tarefas repetitivas. No entanto, com muita frequência, esquecemos que isso se aplica tanto ao nosso uso do computador quanto aos cálculos que queremos que nossos programas realizem. Temos uma vasta gama de ferramentas disponíveis na ponta dos dedos que nos permitem ser mais produtivos e resolver problemas mais complexos ao trabalhar em qualquer problema relacionado a computadores. Ainda assim, muitos de nós utilizam apenas uma pequena fração dessas ferramentas; sabemos apenas o suficiente de encantamentos mágicos de cor para sobreviver e copiamos e colamos comandos da internet às cegas quando travamos.

Esta aula é uma tentativa de resolver isso.

Queremos ensinar como aproveitar ao máximo as ferramentas que você conhece, mostrar novas ferramentas para adicionar à sua caixa de ferramentas e, esperançosamente, instilar em você um pouco de empolgação para explorar (e talvez construir) mais ferramentas por conta própria. É isso que acreditamos ser o "semestre perdido" na maioria dos currículos de Ciência da Computação.

### Estrutura da aula

A aula, sem créditos, consiste em nove palestras de 1 hora, cada uma centrada em um tópico específico. As palestras são em grande parte independentes, embora à medida que o semestre avance, presumiremos que você esteja familiarizado com o conteúdo das palestras anteriores. Temos anotações das aulas online, mas pode haver conteúdo coberto em aula (por exemplo, na forma de demonstrações) que pode não estar nas anotações. Como nos anos anteriores, estaremos gravando as aulas e postando as gravações online.

Estamos tentando cobrir muito terreno ao longo de apenas algumas palestras de 1 hora, então as aulas são bastante densas. Para permitir que você tenha algum tempo para se familiarizar com o conteúdo no seu próprio ritmo, cada aula inclui um conjunto de exercícios que o guiam pelos pontos-chave da aula. Não teremos horários de atendimento dedicados, mas encorajamos você a fazer perguntas no Discord da OSSU, em #missing-semester-forum, ou nos enviar um e-mail em missing-semester@mit.edu.

Devido ao tempo limitado que temos, não poderemos cobrir todas as ferramentas no mesmo nível de detalhe que uma aula em escala completa poderia. Quando possível, tentaremos apontar recursos para aprofundar-se em uma ferramenta ou tópico, mas se algo chamar particularmente a sua atenção, não hesite em nos contatar e pedir referências!

Por fim, se você tiver feedback sobre a aula, por favor envie para nós por e-mail em missing-semester@mit.edu.

---

## Tópico 1: O Shell

### O que é o shell?

Os computadores hoje em dia têm uma variedade de interfaces para receber comandos; interfaces gráficas de usuário elaboradas, interfaces de voz, AR/VR e, mais recentemente: LLMs. Estas são ótimas para 80% dos casos de uso, mas são frequentemente fundamentalmente restritas no que permitem que você faça — você não pode pressionar um botão que não existe ou dar um comando de voz que não foi programado. Para aproveitar ao máximo as ferramentas que seu computador oferece, temos que voltar à velha escola e descer para uma interface textual: O Shell.

Quase todas as plataformas que você pode ter em mãos têm um shell de uma forma ou de outra, e muitas delas têm vários shells para você escolher. Embora possam variar nos detalhes, no núcleo todas são aproximadamente iguais: elas permitem que você execute programas, forneça entrada e inspecione sua saída de maneira semi-estruturada.

Para abrir um prompt de shell (onde você pode digitar comandos), você primeiro precisa de um terminal, que é a interface visual para um shell. Seu dispositivo provavelmente veio com um instalado, ou você pode instalar um facilmente:

*   **Linux:** Pressione `Ctrl + Alt + T` (funciona na maioria das distribuições). Ou procure por "Terminal" no menu de aplicativos.
*   **Windows:** Pressione `Win + R`, digite `cmd` ou `powershell` e pressione Enter. Alternativamente, procure por "Terminal" ou "Prompt de Comando" no menu Iniciar.
*   **macOS:** Pressione `Cmd + Space` para abrir o Spotlight, digite "Terminal" e pressione Enter. Ou encontre-o em Aplicativos → Utilitários → Terminal.

No Linux e macOS, isso geralmente abrirá o Bourne Again SHell, ou "bash" para abreviar. Este é um dos shells mais amplamente utilizados, e sua sintaxe é semelhante à que você verá em muitos outros shells. No Windows, você será saudado pelos shells "batch" ou "powershell", dependendo de qual comando você executou. Estes são específicos do Windows, e não são o foco desta aula, embora tenham análogos para a maior parte do que ensinaremos. Em vez disso, você vai querer o Windows Subsystem for Linux ou uma máquina virtual Linux.

Outros shells existem, frequentemente com muitas melhorias ergonômicas em relação ao bash (fish e zsh estão entre os mais comuns). Embora sejam muito populares (todos os instrutores usam um), eles não são nem remotamente tão onipresentes quanto o bash, e dependem de muitos dos mesmos conceitos, então não nos focaremos neles nesta palestra.

### Por que você deveria se importar com isso?

O shell não é apenas (geralmente) muito mais rápido do que "clicar por aí", ele também vem com um poder expressivo que você não encontra facilmente em nenhum programa gráfico. Como veremos, o shell lhe dá a capacidade de combinar programas de formas criativas para automatizar quase qualquer tarefa.

Conhecer o caminho ao redor de um shell também é muito útil para navegar no mundo do software de código aberto (que frequentemente vem com instruções de instalação que exigem o shell), construir integração contínua para seus projetos de software (conforme descrito na aula de Qualidade de Código) e depurar erros quando outros programas falham.

### Navegando no shell

Quando você inicia seu terminal, verá um prompt que frequentemente parece um pouco com isso:

```bash
missing:~$
```

Esta é a principal interface textual para o shell. Ela diz que você está na máquina `missing` e que seu "diretório de trabalho atual", ou onde você está atualmente, é `~` (abreviação de "home", ou casa). O `$` diz que você não é o usuário root (mais sobre isso depois). Neste prompt, você pode digitar um comando, que será então interpretado pelo shell. O comando mais básico é executar um programa:

```bash
missing:~$ date
Fri 10 Jan 2020 11:49:31 AM EST
missing:~$
```

Aqui, executamos o programa `date`, que (talvez sem surpresa) imprime a data e hora atuais. O shell então nos pede outro comando para executar. Também podemos executar um comando com argumentos:

```bash
missing:~$ echo hello
hello
```

Neste caso, dissemos ao shell para executar o programa `echo` com o argumento `hello`. O programa `echo` simplesmente imprime seus argumentos. O shell analisa o comando dividindo-o por espaços em branco e, em seguida, executa o programa indicado pela primeira palavra, fornecendo cada palavra subsequente como um argumento que o programa pode acessar. Se você quiser fornecer um argumento que contenha espaços ou outros caracteres especiais (por exemplo, um diretório chamado "Minhas Fotos"), você pode citar o argumento com `'` ou `"` (`"Minhas Fotos"`), ou escapar apenas os caracteres relevantes com `\` (`Minhas\ Fotos`).

Talvez o comando mais importante quando você está começando seja `man`, abreviação de "manual". O programa `man`, entre outras coisas, permite que você procure mais informações sobre qualquer comando no seu sistema. Por exemplo, se você executar `man date`, ele explicará o que é `date` e todos os vários argumentos que você pode passar para alterar seu comportamento. Você também pode geralmente obter uma versão curta da ajuda passando `--help` como argumento para a maioria dos comandos.

> **Nota 1**
>
> Depois de `man`, o comando mais importante a aprender é `cd`, ou "change directory" (mudar diretório). Este comando é realmente integrado ao shell, e não é um programa separado (ou seja, `which cd` dirá "no cd found"). Você passa um caminho para ele, e esse caminho se torna seu diretório de trabalho atual. Você também verá o diretório de trabalho refletido no prompt do shell:
>
> ```bash
> missing:~$ cd /bin
> missing:/bin$ cd /
> missing:/$ cd ~
> missing:~$
> ```

> **Nota 2**
>
> Muitos comandos operam no diretório de trabalho atual se nada mais for especificado. Se você não tiver certeza de onde está, pode executar `pwd` ou imprimir a variável de ambiente `$PWD` (com `echo $PWD`), ambos produzem o diretório de trabalho atual.
>
> O diretório de trabalho atual também é útil porque nos permite usar caminhos relativos. Todos os caminhos que vimos até agora foram absolutos — eles começam com `/` e fornecem o conjunto completo de diretórios necessários para navegar até algum local a partir da raiz do sistema de arquivos (`/`). Na prática, você trabalhará mais comumente com caminhos relativos; assim chamados porque são relativos ao diretório de trabalho atual. Em um caminho relativo (qualquer coisa que não comece com `/`), o primeiro componente do caminho é procurado no diretório de trabalho atual, e os componentes subsequentes atravessam como de costume. Por exemplo:
>
> ```bash
> missing:~$ cd /
> missing:/$ cd bin
> missing:/bin$
> ```
>
> Existem também dois componentes "especiais" que existem em todos os diretórios: `.` e `..`. `.` é "este diretório", e `..` é "o diretório pai". Então:
>
> ```bash
> missing:~$ cd /
> missing:/$ cd bin/../bin/../bin/././../bin/..
> missing:/$
> ```
>
> Você geralmente pode usar caminhos absolutos e relativos de forma intercambiável para qualquer argumento de comando, apenas lembre-se qual é seu diretório de trabalho atual ao usar um relativo!

> **Nota 3**

### O que está disponível no shell?

Mas como o shell sabe como encontrar programas como `date` ou `echo`? Se o shell for solicitado a executar um comando, ele consulta uma variável de ambiente chamada `$PATH` que lista quais diretórios o shell deve procurar por programas quando recebe um comando:

```bash
missing:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
missing:~$ which echo
/bin/echo
missing:~$ /bin/echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

Quando executamos o comando `echo`, o shell vê que deve executar o programa `echo` e, em seguida, pesquisa na lista de diretórios separados por `:` no `$PATH` um arquivo com esse nome. Quando o encontra, ele o executa (assumindo que o arquivo é executável; mais sobre isso depois). Podemos descobrir qual arquivo é executado para um determinado nome de programa usando o programa `which`. Também podemos ignorar o `$PATH` completamente fornecendo o caminho para o arquivo que queremos executar.

Isso também dá uma pista de como podemos determinar todos os programas que somos capazes de executar no shell: listando o conteúdo de todos os diretórios no `$PATH`. Podemos fazer isso passando um determinado caminho de diretório para o programa `ls`, que lista arquivos:

```bash
missing:~$ ls /bin
```

> **Nota 4**
>
> Isso vai, na maioria dos computadores, imprimir muitos programas, mas focaremos apenas em alguns dos mais importantes aqui. Primeiro, alguns simples:
>
> *   `cat file`, que imprime o conteúdo do arquivo.
> *   `sort file`, que imprime as linhas do arquivo em ordem classificada.
> *   `uniq file`, que elimina linhas duplicadas consecutivas do arquivo.
> *   `head file` e `tail file`, que respectivamente imprimem as primeiras e últimas linhas do arquivo.

> **Nota 5**
>
> Há também `grep pattern file`, que encontra linhas correspondentes ao padrão no arquivo. Este merece um pouco mais de atenção, pois é muito útil e possui uma gama mais ampla de recursos do que se pode esperar. `pattern` é na verdade uma expressão regular que pode expressar padrões muito complexos — cobriremos isso na aula de qualidade de código. Você também pode especificar um diretório em vez de um arquivo (ou omiti-lo para `.`) e passar `-r` para pesquisar recursivamente todos os arquivos em um diretório.

> **Nota 6**
>
> Existem também algumas ferramentas muito úteis com uma interface um pouco mais complicada. A primeira delas é `sed`, que é um editor de arquivos programático. Ele tem sua própria linguagem de programação para fazer edições automatizadas em arquivos, mas o uso mais comum dele é:
>
> ```bash
> missing:~$ sed -i 's/pattern/replacement/g' file
> ```
>
> Isso substitui todas as instâncias de `pattern` por `replacement` no arquivo. O `-i` indica que queremos que as substituições aconteçam inline (em vez de deixar o arquivo inalterado e imprimir o conteúdo substituído). O `s/` é a maneira de expressar na linguagem de programação `sed` que queremos fazer uma substituição. O `/` separa o padrão da substituição. E o `/g` final indica que queremos substituir todas as ocorrências em cada linha em vez de apenas a primeira. Como no `grep`, `pattern` aqui é uma expressão regular, o que lhe dá um poder expressivo significativo. Substituições de expressões regulares também permitem que a substituição se refira a partes do padrão correspondido; veremos um exemplo disso em um segundo.
>
> A seguir, temos `find`, que permite encontrar arquivos (recursivamente) que correspondem a certas condições. Por exemplo:
>
> ```bash
> missing:~$ find ~/Downloads -type f -name "*.zip" -mtime +30
> ```
>
> Encontra arquivos ZIP no diretório de download que são mais antigos que 30 dias.
>
> ```bash
> missing:~$ find ~ -type f -size +100M -exec ls -lh {} \;
> ```
>
> Encontra arquivos maiores que 100M no seu diretório home e os lista. Note que `-exec` recebe um comando terminado com um `;` independente (que precisamos escapar muito como um espaço) onde `{}` é substituído por cada caminho de arquivo correspondente pelo `find`.
>
> ```bash
> missing:~$ find . -name "*.py" -exec grep -l "TODO" {} \;
> ```
>
> Encontra quaisquer arquivos .py com itens TODO dentro deles.
>
> A sintaxe do `find` pode ser um pouco intimidante, mas esperançosamente isso lhe dá uma noção de quão útil ele pode ser!

> **Nota 7**
>
> O próximo na lista é `awk`, que, como `sed`, tem sua própria linguagem de programação. Onde `sed` é construído para editar arquivos, `awk` é construído para analisá-los. De longe, o uso mais comum de `awk` é para arquivos de dados com uma sintaxe regular (como arquivos CSV) onde você deseja extrair apenas certas partes de cada registro (ou seja, linha):
>
> ```bash
> missing:~$ awk '{print $2}' file
> ```
>
> Imprime a segunda coluna separada por espaços em branco de cada linha do arquivo. Se você adicionar `-F,`, ele imprimirá a segunda coluna separada por vírgulas de cada linha. `awk` pode fazer muito mais — filtrar linhas, calcular agregados e mais — veja os exercícios para uma amostra.
>
> Juntando essas ferramentas, podemos fazer coisas sofisticadas como:
>
> ```bash
> missing:~$ ssh myserver 'journalctl -u sshd -b-1 | grep "Disconnected from"' \
>   | sed -E 's/.*Disconnected from .* user (.*) [^ ]+ port.*/\1/' \
>   | sort | uniq -c \
>   | sort -nk1,1 | tail -n10 \
>   | awk '{print $2}' | paste -sd,
> postgres,mysql,oracle,dell,ubuntu,inspur,test,admin,user,root
> ```
>
> Isso pega logs SSH de um servidor remoto (falaremos mais sobre `ssh` na próxima aula), procura mensagens de desconexão, extrai o nome de usuário de cada mensagem e imprime os 10 principais nomes de usuário separados por vírgula. Tudo em um comando! Deixaremos a dissecação de cada etapa como um exercício.

### A linguagem do shell (bash)

O exemplo anterior introduziu um novo conceito: pipes (`|`). Eles permitem encadear a saída de um programa com a entrada de outro. Isso funciona porque a maioria dos programas de linha de comando operará em sua "entrada padrão" (onde suas teclas normalmente vão) se nenhum argumento de arquivo for fornecido. `|` pega a "saída padrão" (o que normalmente é impresso no seu terminal) do programa antes do `|` e a torna a entrada padrão do programa após o `|`. Isso permite que você componha programas de shell, e é parte do que torna o shell um ambiente tão produtivo para trabalhar!

Na verdade, a maioria dos shells implementa uma linguagem de programação completa (como bash), assim como Python ou Ruby. Ela tem variáveis, condicionais, loops e funções. Quando você executa comandos no seu shell, você está realmente escrevendo um pequeno pedaço de código que seu shell interpreta. Não ensinaremos todo o bash hoje, mas há alguns bits que você achará particularmente úteis:

Primeiro, redirecionamentos: `>file` permite pegar a saída padrão de um programa e escrevê-la em um arquivo em vez de no seu terminal. Isso facilita a análise posterior. `>>file` anexará ao arquivo em vez de sobrescrevê-lo. Há também `<file` que diz ao shell para ler de um arquivo em vez de do seu teclado como a entrada padrão para um programa.

> **Nota 8**
>
> Este é um bom momento para mencionar o programa `tee`. `tee` imprimirá a entrada padrão na saída padrão (assim como `cat`!), mas também a escreverá em um arquivo. Então `verbose cmd | tee verbose.log | grep CRITICAL` preservará o log completo verboso em um arquivo enquanto mantém seu terminal limpo!

A seguir, condicionais: `if command1; then command2; command3; fi` executará `command1`, e se não resultar em um erro, executará `command2` e `command3`. Você também pode ter um ramo `else` se desejar. O comando mais comum a ser usado como `command1` é o comando `test`, frequentemente abreviado simplesmente como `[`, que permite avaliar condições como "um arquivo existe" (`test -f file` / `[ -f file ]`) ou "uma string é igual a outra" (`[ "$var" = "string" ]`). No bash, também existe `[[ ]]`, que é uma versão "mais segura" integrada do `test` que tem menos comportamentos estranhos em relação a citações.

Bash também tem duas formas de loops, `while` e `for`. `while command1; do command2; command3; done` funciona exatamente como o equivalente `if command`, exceto que executará tudo de novo e de novo pelo tempo em que `command1` não der erro. `for varname in a b c d; do command; done` executa `command` quatro vezes, cada vez com `$varname` definido como um de `a`, `b`, `c` e `d`. Em vez de listar os itens explicitamente, você frequentemente usará "substituição de comando", como:

```bash
for i in $(seq 1 10); do
```

Isso executa o comando `seq 1 10` (que imprime os números de 1 a 10 inclusive) e então substitui todo o `$()` pela saída desse comando, dando a você um loop `for` de 10 iterações. Em códigos antigos, você às vezes verá backticks literais (como `for i in `seq 1 10`; do`) em vez de `$()`, mas você deve preferir fortemente a forma `$()`, pois ela pode ser aninhada.

Embora você possa escrever scripts de shell longos diretamente no seu prompt, geralmente você vai querer escrevê-los em um arquivo `.sh`. Por exemplo, aqui está um script que executará um programa em um loop até que ele falhe, imprimindo a saída apenas da execução falha, enquanto estressa sua CPU em segundo plano (útil para reproduzir testes instáveis, por exemplo):

```bash
#!/bin/bash
set -euo pipefail

# Iniciar estresse de CPU em segundo plano
stress --cpu 8 &
STRESS_PID=$!

# Configurar arquivo de log
LOGFILE="test_runs_$(date +%s).log"
echo "Logging to $LOGFILE"

# Executar testes até que um falhe
RUN=1
while cargo test my_test > "$LOGFILE" 2>&1; do
    echo "Run $RUN passed"
    ((RUN++))
done

# Limpar e relatar
kill $STRESS_PID
echo "Test failed on run $RUN"
echo "Last 20 lines of output:"
tail -n 20 "$LOGFILE"
echo "Full log: $LOGFILE"
```

Isso tem uma série de coisas novas nele que recomendo que você gaste algum tempo investigando, pois são muito úteis ao criar invocações de shell úteis, como jobs em segundo plano (`&`) para executar programas simultaneamente, redirecionamentos de shell mais complexos e expansão aritmética.

Vale a pena gastar um segundo nas duas primeiras linhas do programa. A primeira é o "shebang" – você verá isso no topo de outros arquivos além de scripts de shell. Quando um arquivo que começa com a encantamento mágico `#!/path` é executado, o shell iniciará o programa em `/path` e passará o conteúdo do arquivo como entrada. No caso de um script de shell, isso significa passar o conteúdo do script de shell para `/bin/bash`, mas você também pode escrever scripts Python com uma linha shebang de `/usr/bin/python`!

A segunda linha é uma maneira de tornar o bash "mais estrito" e mitigar uma série de armadilhas ao escrever scripts de shell. `set` pode receber muitos argumentos, mas brevemente: `-e` faz com que se qualquer comando falhar, o script saia mais cedo; `-u` faz com que o uso de variáveis indefinidas trave o script em vez de apenas usar uma string vazia; e `-o pipefail` faz com que se programas em uma sequência `|` falharem, o script de shell como um todo também saia mais cedo.

> **Nota 9**

### Próximos passos

Neste ponto, você conhece o caminho ao redor de um shell o suficiente para realizar tarefas básicas. Você deve ser capaz de navegar para encontrar arquivos de interesse e usar a funcionalidade básica da maioria dos programas. Na próxima aula, falaremos sobre como realizar e automatizar tarefas mais complexas usando o shell e os muitos programas úteis de linha de comando disponíveis.

---

## Exercícios

Todas as aulas neste curso são acompanhadas por uma série de exercícios. Alguns lhe dão uma tarefa específica para fazer, enquanto outros são abertos, como "tente usar os programas X e Y". Nós o encorajamos muito a experimentá-los.

Não escrevemos soluções para os exercícios. Se você estiver preso em qualquer coisa em particular, sinta-se à vontade para postar em #missing-semester-forum no Discord ou nos enviar um e-mail descrevendo o que você tentou até agora, e tentaremos ajudá-lo. Esses exercícios também provavelmente funcionarão bem como prompts iniciais em uma conversa com um LLM onde você pode mergulhar interativamente no tópico. O valor real nesses exercícios é a jornada de descobrir as respostas, não a resposta em si. Encorajamos você a seguir tangentes e perguntar "por que" enquanto trabalha neles, em vez de apenas procurar o caminho mais curto para a solução.

1.  Para este curso, você precisa estar usando um shell Unix como Bash ou ZSH. Se você estiver no Linux ou macOS, não precisa fazer nada especial. Se você estiver no Windows, precisa ter certeza de que não está executando `cmd.exe` ou PowerShell; você pode usar o Windows Subsystem for Linux ou uma máquina virtual Linux para usar ferramentas de linha de comando estilo Unix. Para ter certeza de que está executando um shell apropriado, você pode tentar o comando `echo $SHELL`. Se disser algo como `/bin/bash` ou `/usr/bin/zsh`, isso significa que você está executando o programa certo.

2.  O que a flag `-l` faz para o `ls`? Execute `ls -l /` e examine a saída. O que os primeiros 10 caracteres de cada linha significam? (Dica: `man ls`)

3.  No comando `find ~/Downloads -type f -name "*.zip" -mtime +30`, o `*.zip` é um "glob". O que é um glob? Crie um diretório de teste com alguns arquivos e experimente padrões como `ls *.txt`, `ls file?.txt` e `ls {a,b,c}.txt`. Veja *Pattern Matching* no manual do Bash.

4.  Qual é a diferença entre 'aspas simples', "aspas duplas" e $'aspas ANSI'? Escreva um comando que faça echo de uma string contendo um `$` literal, um `!` e um caractere de nova linha. Veja *Quoting*.

5.  O shell tem três fluxos padrão: stdin (0), stdout (1) e stderr (2). Execute `ls /nonexistent /tmp` e redirecione stdout para um arquivo e stderr para outro. Como você redirecionaria ambos para o mesmo arquivo? Veja *Redirections*.

6.  `$?` contém o status de saída do último comando (0 = sucesso). `&&` executa o próximo comando apenas se o anterior foi bem-sucedido; `||` executa apenas se o anterior falhou. Escreva uma one-liner que cria `/tmp/mydir` apenas se ele ainda não existir. Veja *Exit Status*.

7.  Por que `cd` tem que ser integrado ao próprio shell em vez de um programa independente? (Dica: pense sobre o que um processo filho pode e não pode afetar em seu pai.)

8.  Escreva um script que recebe um nome de arquivo como argumento (`$1`) e verifica se o arquivo existe usando `test -f` ou `[ -f ... ]`. Ele deve imprimir mensagens diferentes dependendo se o arquivo existe. Veja *Bash Conditional Expressions*.

9.  Salve o script do exercício anterior em um arquivo (por exemplo, `check.sh`). Tente executá-lo com `./check.sh somefile`. O que acontece? Agora execute `chmod +x check.sh` e tente novamente. Por que esta etapa é necessária? (Dica: veja `ls -l check.sh` antes e depois do `chmod`.)

10. O que acontece se você adicionar `-x` aos flags de `set` em um script? Tente com um script simples e observe a saída. Veja *The Set Builtin*.

11. Escreva um comando que copia um arquivo para um backup com a data de hoje no nome do arquivo (por exemplo, `notes.txt` → `notes_2026-01-12.txt`). (Dica: `$(date +%Y-%m-%d)`). Veja *Command Substitution*.

12. Modifique o script de teste instável da aula para aceitar o comando de teste como argumento em vez de codificar `cargo test my_test`. (Dica: `$1` ou `$@`). Veja *Special Parameters*.

13. Use pipes para encontrar as 5 extensões de arquivo mais comuns no seu diretório home. (Dica: combine `find`, `grep` ou `sed` ou `awk`, `sort`, `uniq -c` e `head`.)

14. `xargs` converte linhas de stdin em argumentos de comando. Use `find` e `xargs` juntos (não `find -exec`) para encontrar todos os arquivos `.sh` em um diretório e contar as linhas em cada um com `wc -l`. Bônus: faça lidar com nomes de arquivos com espaços. (Dica: `-print0` e `-0`). Veja `man xargs`.

15. Use `curl` para buscar o HTML do site do curso (https://missing.csail.mit.edu/) e faça pipe para `grep` para contar quantas aulas estão listadas. (Dica: procure um padrão que aparece uma vez por aula; use `curl -s` para silenciar a saída de progresso.)

16. `jq` é uma ferramenta poderosa para processar dados JSON. Busque os dados de exemplo em https://microsoftedge.github.io/Demos/json-dummy-data/64KB.json com `curl` e use `jq` para extrair apenas os nomes das pessoas cuja versão é maior que 6. (Dica: faça pipe para `jq .` primeiro para ver a estrutura; então tente `jq '.[] | select(...) | .name'`)

17. `awk` pode filtrar linhas com base em valores de colunas e manipular a saída. Por exemplo, `awk '$3 ~ /pattern/ {$4=""; print}'` imprime apenas linhas onde a terceira coluna corresponde ao padrão, enquanto omite a quarta coluna. Escreva um comando `awk` que imprime apenas linhas onde a segunda coluna é maior que 100, e troca a primeira e a terceira colunas. Teste com: `printf 'a 50 x\nb 150 y\nc 200 z\n'`

18. Disseque o pipeline de log SSH da aula: o que cada etapa faz? Em seguida, construa algo semelhante para encontrar seus comandos de shell mais usados em `~/.bash_history` (ou `~/.zsh_history`).

---

*Edit this page.*

*Licenciado sob CC BY-NC-SA.*

> **Nota de Rodapé 1**
> Considere instalar e usar `tldr` além de `man`, pois ele mostra exemplos de uso comuns direto no terminal. LLMs também geralmente são muito bons em explicar como os comandos funcionam e como você pode chamá-los para alcançar o que deseja realizar.

> **Nota de Rodapé 2**
> Note que o shell vem com auto-complete, então você pode frequentemente completar caminhos mais rápido pressionando `<TAB>`!

> **Nota de Rodapé 3**
> Considere instalar e usar `zoxide` para acelerar seu "cd" — `z` lembrará dos caminhos que você visita frequentemente e permitirá acessá-los com menos digitação.

> **Nota de Rodapé 4**
> Considere instalar e usar `eza` para um `ls` mais amigável ao humano.

> **Nota de Rodapé 5**
> Considere instalar e usar `bat` em vez de `cat` para realce de sintaxe e rolagem.

> **Nota de Rodapé 6**
> Considere instalar e usar `ripgrep` em vez de `grep` para uma alternativa mais rápida e amigável ao humano (mas menos portátil). `ripgrep` também pesquisará recursivamente o diretório de trabalho atual por padrão!

> **Nota de Rodapé 7**
> Considere instalar e usar `fd` em vez de `find` para uma experiência mais amigável ao humano (mas menos portátil!).

> **Nota de Rodapé 8**
> Este é um bom momento para mencionar o programa `tee`. `tee` imprimirá a entrada padrão na saída padrão (assim como `cat`!), mas também a escreverá em um arquivo. Então `verbose cmd | tee verbose.log | grep CRITICAL` preservará o log completo verboso em um arquivo enquanto mantém seu terminal limpo!

> **Nota de Rodapé 9**
> A programação de shell é um tópico profundo, assim como qualquer linguagem de programação, mas cuidado: o bash tem um número incomum de armadilhas (gotchas), a ponto de existirem vários sites dedicados a listá-las. Recomendo fortemente fazer uso pesado do `shellcheck` ao escrevê-los. LLMs também são ótimos em escrever e depurar scripts de shell, bem como traduzi-los para uma linguagem de programação "real" (como Python) quando eles ficaram grandes demais para o bash (mais de 100 linhas).
```
