==================
TUTORIAL SED & AWK
==================

===
SED
===

O SED é um editor de texto. É utilizado em tarefas comuns de edição e visualização de texto, através de linhas de comando. E somente trabalha com linhas em arquivos de texto

Observações importantes:

É preciso usar a barra de espaço nos locais corretos para delimitar os caracteres 
Após o comando sed é necessário delimitar cada condição com aspas simples ( ' ) ou duplas ( '' )
É necessário usar o maior que ( > ) para salvar a edição em um arquivo output de nome diferente ou igual (nesse caso o arquivo inicial é modificado), devido a isso é importante    salvar o arquivo a cada comando ou usar uma série de comandos e salvar com o  ( > )
É possível criar scripts com múltiplos comandos de SED para alterar/visualizar arquivos. Nesse caso, não é necessário utilizar o argumento ( -e ) em cada comando, porém é necessário utilizar um script

==============
Comando básico 
==============

.. code:: bash

    sed 'comandos/CARACTERES/comandos' INPUT.file > OUTPUT.file 
   
==========================================================================
Comando de substituição da primeira letra, palavra ou número de cada linha
==========================================================================

.. code:: bash

   sed 's/CARACTERDEINTERESSE/CARACTERDEINTERESSESUBSTITUIDO/' INPUT.file > OUTPUT.file
  
O argumento para substituição é a letra ( s )

Exemplos:

   sed 's/T/U/' DNA.txt > RNA.txt                     
   
   sed 's/DNA/RNA/' DNA.txt > RNA.txt

================================================================
Comando de substituição global da letra ou palavra de cada linha
================================================================

.. code:: bash

   sed 's/CARACTERDEINTERESSE/CARACTERDEINTERESSESUBSTITUIDO/g' INPUT.file > OUTPUT.file
 
O argumento para substituição é a letra ( s ) e, para que seja global utiliza-se a letra ( g ) no final, seguido das aspas

Exemplos:

   sed 's/T/U/g' DNA.txt > RNA.txt                       
   
   sed 's/DNA/RNA/g' DNA.txt > RNA.txt

==============================================================================
Comando de deleção da linha inteira que contenha a letra ou palavra de escolha
==============================================================================

.. code:: bash

   sed '/CARACTERDEINTERESSE/d' INPUT.file > OUTPUT.file
  
O argumento para deleção da linha inteira é a letra (d)

Exemplos: 

   sed '/T/d' DNA.txt > RNA.txt                
   
   sed '/DNA/d' DNA.txt > RNA.txt

==============================================
Comando para deletar todas as linhas em branco
==============================================

.. code:: bash

   sed '/^$/d' INPUT.file > OUTPUT.file
  
O argumento para deletar a linha continua sendo a letra ( d ), porém o argumento ( ^ ) indica qual caractere a linha deve ser começar e o argumento ( $ ) é o marcador ou delimitador do fim da linha. O fato de a linha em branco ser deletada é devido a nenhuma, palavra ou letra, estar sendo especificada

Exemplo: 
  
   sed '/^$/d' DNA.txt > RNA.txt

=======================================================
Comando para deleção de linha específica ou selecionada
=======================================================

.. code:: bash

   sed 'NÚMERODALINHASELECIONADAd' INPUT.file > OUTPUT.file
  
O argumento para deletar a linha continua sendo a letra ( d ), porém, diferentemente dos comandos anteriores, o número da linha que será deletada vem atrás do argumento ( d ). Nesse caso, não é necessário o uso das ( / )

Exemplos:

   sed '3d' DNA.txt > RNA.txt 
   
   sed '4d' DNA.txt > RNA.txt          
   
   sed '5d' DNA.txt > RNA.txt 

=========================================================================
Para selecionar mais de uma linha é necessário utilizar o argumento ( ; )
=========================================================================
 
.. code:: bash

   sed 'PRIMEIRALINHASELECIONADA;SEGUNDALINHASELECIONADA;TERCEIRALINHASELECIONADAd' INPUT.file > OUTPUT.file
  
O argumento ( ; ) seleciona a linha específica. Cada linha selecionada deve ser acompanhada do argumento ( d ) para que seja deletada

Exemplos:

   sed '1d;2d;3d' DNA.txt > RNA.txt
   
   sed '2d;4d;6d' DNA.txt > RNA.txt
   
   sed '1d;5d;7d' DNA.txt > RNA.txt

===============================================================================
Para selecionar intervalos entre linhas é necessário utilizar o argumento ( , )
===============================================================================

.. code:: bash

  sed 'PRIMEIRALINHASELECIONADA,SEGUNDALINHASELECIONADAd' INPUT.file > OUTPUT.file
  
O argumento ( , ) significa intervalo, ou seja, diz que entre uma linha e outra aquele conteúdo será selecionado

Exemplos:

   sed '1,3d' DNA.txt > RNA.txt  
   
   sed '2,4d' DNA.txt > RNA.txt 
   
   sed '20,50d' DNA.txt > RNA.txt

====================================================
Listagem de linhas que contém caracteres específicos 
====================================================

.. code:: bash
  
   sed -n '/CARACTERDEINTERESSE/p' INPUT.file
  
O argumento ( p ) é o argumento de filtragem/listagem do arquivo, sempre acompanhado do argumento ( -n ) que suprime o padrão inicial do arquivo. Nesse caso, sem o argumento ( > ) não será criado um novo arquivo. Isso mostrará a linha que contém o caractere de interesse

Exemplo: 

   sed -n '/SEQUENCEID/p' DNA.txt
  
=============================================
Seleção e Vizualização de linhas selecionádas
=============================================

Da mesma forma que podemos deletar linhas selecionadas/específicas, podemos visualizar/printar linhas selecionadas/específicas. Utilizando os argumentos ( ; ) selecionamos mais de uma linha em específico e o argumento ( , ) selecionamos linhas entre(intervalo) duas linhas especificadas:

Exemplos para selecionar e visualizar uma linha em específico:

   sed -n '1p' DNA.txt  
   
   sed -n '5p' DNA.txt
  
Exemplos para selecionar e visualizar mais de uma linha em específico: 

   sed -n '1p;2p;3p' DNA.txt
   
   sed -n '2p;4p;6p' DNA.txt 
   
   sed -n '1p;5p;10p' DNA.txt
  
Exemplos para selecionar e visualizar linhas selecionadas entre(intervalo) uma linha e outra, em específico:

   sed -n '1p,3p' DNA.txt
   
   sed -n '2p,4p' DNA.txt
   
   sed -n '1p,10p' DNA.txt
  
============================
Transliteração de caracteres
============================

.. code:: bash

   sed 'y/CARACTERESDEINTERESSE/caracteresdeinteresse/' INPUT.file > OUTPUT.file
  
Nesse caso também ocorre uma substituição, porém o argumento utilizado é o ( y ) e, diferentemente do argumento ( s ), não reconhece palavras. A substituição é feita na ordem dos caracteres que foram selecionados

Exemplos:

   sed 'y/ACTG/actg/' DNA.txt > DNA2.txt 
   
   sed 'y/ACTG/acug/' DNA.txt > RNA.txt
  


===========================================================
Negação de linhas selecionadas utilizando o argumento ( ! ) 
===========================================================

.. code:: bash

   sed '/CARACTEROUCARACTERESESPECÍFICOS/!y/CARACTERESDEINTERESSE/caracteresdeinteresse/' INPUT.file > OUTPUT.file
  
O argumento ( ! ) significa que todas as linhas que contenham os caracteres selecionados com os separadores ( / / ), não serão inclusas na deleção/substituição/transliteração/print, no caso do exemplo usaremos a transliteração e negaremos linhas que contenham com o caractere ( > )

Exemplo: 

   sed '/>/!y/ACTG/actg/' DNA.txt > RNA.txt        

Nesse caso, todas as linhas que contenham o caractere ( > ) serão inclusas na transliteração

================
Argumento ( -e )
================

Múltiplos Comandos em SED é possível caso utilizado o argumento ( -e )  antes de cada comando 
O sed não precisa estar presente em cada comando, ele vem apenas para chamar o arquivo editor de texto

Exemplo:

.. code:: bash
   
   sed -e 's/ATG/*ATG*/g' -e '/^>/d' DNA.txt > DNA2.txt 
 
Supondo que seja uma sequência de DNA, esse comando substituiria (argumento ( s )) todos os ATG por *ATG* (o asterisco serviria para flanquear/destacar os nucleotídeos) de todas as linhas (argumento( g )). Além disso excluiria (argumento ( d )) todas as linhas que começassem (argumento( ^ )) com o caractere ( > ), ou seja, a identificação de cada sequência

Também possível criar scripts com múltiplos comandos de SED para alterar/visualizar arquivos. Nesse caso, não é necessário utilizar o argumento ( -e ) em cada comando, porém é necessário utilizar a flag/argumento ( -f ) e um arquivo script (arquivo com um editor de texto (exemplo: nano ) separando cada comando). Usaremos o mesmo exemplo anterior

Exemplo com o editor de texto nano: Criar um arquivo chamado ( script.sed ) contendo: 

.. code:: bash

  s/ATG/*ATG*/g                                                                                                                                 
  /^>/d
  
Nesse caso não usaremos aspas, porém em cada comando é necessário separar com ENTER
Após criar o script, para chama-lo, devemos escrever: 

.. code:: bash

  sed -f script.sed DNA.txt > DNA2.txt 
  
No caso, o sed usará o script chamado ( script.sed ) para alterar o arquivo ( DNA.txt ) e salvar esse arquivo como ( DNA2.txt )

###################################################################################################################################################################################

===
AWK
===

==============
Comando Básico
==============

.. code:: bash

   awk 'CONDIÇÕES/CARACTERES/{AÇÕES}' INPUT.file > OUTPUT.file

O AWK é uma linguagem de programação, utilizado para tarefas comuns em manipulação de dados: realiza cálculos, filtra, lê, escreve e toma decisões em diversos arquivos, principalmente em arquivos tipo tabelas. Assim como o SED, o AWK lê o arquivo, linha por linha, porém as colunas são divididas em campos ( Colunas ). Cada campo é separado por um espaço (padrão), TAB ou, um delimitador definível. Toda linha é armazenada em ( $0 ), o primeiro campo (coluna) seria ( $1 ), o segundo campo (coluna) por ( $2 ), e assim por diante. Como no AWK é possível realizar ações, elas sempre são definidas pelas chaves ( {} ). O AWK considera como delimitadores: espaços em branco ( SPACE BAR ) e tabulações ( TAB ). E o Argumento ( │ ) separa múltiplos comandos, assim como o argumento ( -e ) na linguagem do programa SED

=======================================================================================================
Identificação  do número de campos/colunas ( NF ), delimitados por tabulação ( TAB ) ou barra de espaço
=======================================================================================================

.. code:: bash

   awk '{print NF}' INPUT.file INPUT.file > OUTPUT.file 
  
Nesse caso o delimitador não é diferenciado

Para especificar o delimitador ( TAB ) quando realizar a ação de print de todas as linhas, utiliza-se o comando:

.. code:: bash

   awk -F'/t' '{print NF} INPUT.file > OUTPUT.file
  
Dessa forma será identificado o número de campos/colunas, tabulados, em cada linha


Quando o objetivo for descobrir o número de campos/colunas de todas as linhas, utiliza-se o comando:

.. code:: bash

   awk '{print $NF}' INPUT.file > OUTPUT.file
  
Desse modo será identificado o número do último campo/coluna, ou seja, o número de campos/colunas totais
Ou a penúltima e assim por diante:

.. code:: bash

  awk '{print $(NF-1)}' INPUT.file > OUTPUT.file
  

Para identificar a numeração de cada linha ( NR ), utiliza-se o comando:

.. code:: bash

   awk '{print NR, $0}' INPUT.file > OUTPUT.file
  
É necessário utilizar o delimitador ( $0 ) para que a linha inteira seja impressa logo em seguida

==============================================
Filtragem - Pesquisa de caracteres em arquivos
==============================================


.. code:: bash

   awk '/CARACTERDEINTERESSE/' INPUT.file

Esse comando faz uma busca e imprime na tela todas as linhas que contiverem: CARACTERDEINTERESSE. Essa busca é feita em todos os campos ( colunas ) e em todas as linhas

Exemplos: 

   awk '/DNA/' INPUT.file   
   
   awk '/RNA/' INPUT.file


Para especificar letras maiúsculas ou minúsculas, basta fazer o uso da condição ( [ ] )

Exemplos:

  awk '/[Dd]NA/' INPUT.file 
  
  awk '/[Rr]NA/' INPUT.file 
  
======================================
Extração de colunas - Print de Colunas
======================================

.. code:: bash

   awk '{print $*}' INPUT.file > OUTPUT.file
  
Esse comando faz a impressão ( print ) das colunas ( $ ) especificadas ( * ). A impressão pode ser salva com o ( > ) em um arquivo OUTPUT

Exemplos: 

   awk '{print $1}' INPUT.file > OUTPUT.file
   
   awk '{print $1,$2,$3}' INPUT.file > OUTPUT.file  
   
   awk '{print $7,$3,$5}' INPUT.file > OUTPUT.file

Obs.: No terceiro exemplo foi possível mudar a ordem em que os campos (colunas) aparecem

Também é possível mesclar os comandos de filtragem e extração de colunas

Exemplos: 

   awk '/DNA/{print $1}' INPUT.file > OUTPUT.file  
   
   awk '/ATCG/{print $1,$2,$3}' INPUT.file > OUTPUT.file
  
======================================================
Seleção de linhas e colunas com condição: contém ( ~ )
======================================================

Exemplos:

  awk '$1~/ATCG/{print $1}' INPUT.file 
  
  awk '$4~/ATCG/{print $1,$2,$3,$4}' INPUT.file
  
O primeiro exemplo pode ser lido dessa forma: ''caso contenha ( ~ ) os caracteres ( ATCG ) na coluna ( $1 ), imprima ( print ) a coluna ( $1 ) de todas as  linhas''

O segundo exemplo pode ser lido dessa forma: ''caso contenha ( ~ ) os caracteres ( ATCG ) na coluna ( $4 ), imprima ( print ) as colunas ( $1,$2,$3 e $4 ) de todas as linhas''

==========================================================
Seleção de linhas e colunas com a condição: exclusão ( ! )
==========================================================

Exemplo: 

   awk '!/ATCG/{print $1}' INPUT.file

O exemplo pode ser lido dessa forma: ''Imprima ( print ) a coluna ( $1) de todas as linhas que não contenham ( ! ) o caractere ( ATCG )'' 

Nesse caso não é especificado o número do campo ( coluna )

====================================================================
Também é possível mesclar os comandos, contém ( ~ ) e exclusão ( ! )
====================================================================

Exemplo: 
  
   awk '$4!~/ATCG/{print $1,$2,$3,$4}' INPUT.file
  
O exemplo pode ser lido dessa forma: '' imprima as colunas ( $1,$2,$3 e $4 ) de todas as linhas que a coluna ( $4 ) não contenham ( !~ ) o caractere ( ATCG )''

O uso da condição contém ( ~ ), nesse caso, serve para especificar a coluna em que se está trabalhando


==================================================================
Argumentos usados para combinar critérios em filtragem de arquivos
==================================================================

1. Argumento ( == ): Significa que algum nome (geralmente o número da coluna/campo a ser selecionado(a)) é igual a nome desejado 

Exemplo:

   awk '$1==''DNA''' INPUT.file
  
No exemplo, será filtrado todas as linhas, da primeira coluna, que são exatamente iguais aos caracteres (DNA)

Nesse caso, os caracteres são indicados entre as aspas duplas


2. Argumento ( && ): Esse argumento indica o padrão E ( && )

Exemplo: 

   awk '$1==''DNA'' && $2==''ATCG''' INPUT.file
  
No exemplo, somente será filtrado as linhas contiverem o campo ( $1 ) sendo ele igual ( == ) o caractere ( DNA ) e (&&) o campo ( $2 ) sendo igual ( == ) ao caractere ( ATCG ) 


3.Argumento ( ││ ): Esse argumento indica o padrão OU ( ││ )

Exemplo:

   awk '$1==''DNA'' ││ $2==''ATCG''' INPUT.file

No exemplo, somente será filtrado as linhas que contiverem o campo ( $1 ) sendo igual ( == ) ao caractere ( DNA ) ou ( ││) o campo ( $2 ) sendo igual ( == ) ao caractere ( ATGC )


4.Para agrupar critérios de filtragem em um mesmo comando é necessário utilizar o parênteses ( () )

Exemplo:

   awk '($1==''DNA'' ││ $1==''RNA'') && $2>10' INPUT.file
  
No exemplo será filtrado a linha inteira, quando o campo/coluna ( $1 ) for igual ( = ) aos caracteres ( DNA ) e ( RNA ) e ( && ), o valor da coluna ( $2 ) for maior que ( > ) 10

Obs.: Os argumentos E ( && ) e OU ( ││ ) são agrupados devido aos parênteses ( () )


5. Argumento ( != ): Esse argumento significa: diferente. Indica que o campo/coluna é diferente do caractere ou valor filtrado

Exemplo: 

   awk '$1==''DNA'' && $2!=''AUCG''' INPUT.file
  
No exemplo, será filtrado a linha inteira que o campo/coluna ( $1 ) seja igual ( == ) ao caractere ( DNA ) e ( && ) o campo/coluna ( $2 ) seja não pode conter ( != ) o caractere ( AUCG ) 

=============================================================
Criação ou substituição de campos/colunas através de cálculos
=============================================================

Exemplo 1): 
  
   awk '{print $2-$1,print $0}' INPUT.file > OUTPUT.file
  
No exemplo, o programa irá imprimir ( print ) a linha inteira e, criar um campo ( $0 ) no inicio da linha com o resultado da subtração entre os campos ( $2 ) e ( $1 )

Exemplo 2): 
  
   awk '{$3=$2-$1; print}' INPUT.file > OUTPUT.file
  
No exemplo, o programa irá imprimir ( print ) a linha inteira e, criar um campo ( $3 ) no final da linha (caso o arquivo tenha apenas dois campos/colunas) com o resultado da subtração entre os campos ( $2 ) e ( $1 ) respectivamente

Obs.: A diferença em subtrair ou criar um campo/coluna é no uso da vírgula ( , ) e o ponto-vírgula ( ; ), respectivo ao exemplo 1 e 2
