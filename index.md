<style>
  .cabecalho {
    position: absolute;
    top: 10%;
    margin-left: 5%;
    margin-right: 10%;
    font-size: 48px;
    font-weight: bold;
  }
  .conteudo {
    position: absolute;
    top: 30%;
    margin-left: 5%;
    margin-right: 10%;
    font-size: 28px;
    text-align: justify;
  }
  .normal {
    font-size: 24px;
  }
  .small {
    font-size: 16px;
  }
  .tiny {
    font-size: 10px;
  }
  .bold {
    font-weight: bold;
  }
  .center {
    text-align: center;
  }
  section.lead h1 {
    text-align: center;
  }
</style>

<script src="https://polyfill.io/v3/polyfill.min.js?features=es6"></script>
<script id="MathJax-script" async src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML"></script>

![bg opacity](./background.png)
# Pesquisa Operacional II
## Otimização Inteira - Problema da Mochila

Prof. M.Sc. Diego Ascânio Santos (ascanio@cefetmg.br)

Aula baseada sobre o material do professor Dr. João Fernando Machry Sarubbi (joao@cefetmg.br - DECOM), vídeoaulas do curso de algoritmos de pesquisa operacional da Universidade Nacional de Taiwan e referências da documentação do Google OR-Tools

Belo Horizonte, 2023.

---
![bg opacity](./background.png)
<div class="cabecalho">
Roteiro
</div>

<div class="conteudo">
<ol>
  <li>Introdução</li>
  <li>Formulação</li>
  <li>Resolução via Solver</li>
</ol>
</div>

---
![bg opacity](./background.png)
<!-- _class: lead -->
# Introdução

---
![bg opacity](./background.png)
<div class="cabecalho">
Introdução
</div>
<div class="conteudo">
<p>
O objetivo do problema da mochila é o de descobrir a maneira mais eficiente de guardar objetos em uma mochila de capacidade limitada para maximizar o valor (a utilidade) dos objetos a serem carregados.
</p>
<p>
Cada objeto possui um peso \( p_i \) e um valor \( v_i \) e a mochila possui uma capacidade máxima de carga \(P\).
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Introdução
</div>
<div class="conteudo normal">
<p>
Constituem-se exemplos do problema da mochila:
</p>
<p>
<ul>
<li>Colocar roupas em uma mala</li>
</ul>
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Introdução
</div>
<div class="conteudo normal">
<p>
Constituem-se exemplos do problema da mochila:
</p>
<p>
<ul>
<li>Colocar roupas em uma mala</li>
<li>Otimizar a organização de itens em um armazém (logística de armazenamento)</li>
</ul>
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Introdução
</div>
<div class="conteudo normal">
<p>
Constituem-se exemplos do problema da mochila:
</p>
<p>
<ul>
<li>Colocar roupas em uma mala</li>
<li>Otimizar a organização de itens em um armazém (logística de armazenamento)</li>
<ul><li>Para maximizar o uso da capacidade de armazenamento e facilitar o acesso aos produtos</li></ul>
</ul>
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Introdução
</div>
<div class="conteudo normal">
<p>
Constituem-se exemplos do problema da mochila:
</p>
<p>
<ul>
<li>Colocar roupas em uma mala</li>
<li>Otimizar a organização de itens em um armazém (logística de armazenamento)</li>
<ul><li>Para maximizar o uso da capacidade de armazenamento e facilitar o acesso aos produtos</li></ul>
<li>Planejar a disposição de mercadorias dentro de contêineres de transporte (carregamento de contâineres)</li>
</ul>
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Introdução
</div>
<div class="conteudo normal">
<p>
Constituem-se exemplos do problema da mochila:
</p>
<p>
<ul>
<li>Colocar roupas em uma mala</li>
<li>Otimizar a organização de itens em um armazém (logística de armazenamento)</li>
<ul><li>Para maximizar o uso da capacidade de armazenamento e facilitar o acesso aos produtos</li></ul>
<li>Planejar a disposição de mercadorias dentro de contêineres de transporte (carregamento de contâineres)</li>
<ul><li>Visando maximizar o uso da capacidade de carga e garantir a estabilidade durante o transporte</li></ul>
</ul>
</p>
</div>

---
![bg opacity](./background.png)
<!-- _class: lead -->
# Formulação do Problema

---
![bg opacity](./background.png)
<div class="cabecalho">
Formulação do Problema
</div>
<div class="conteudo normal">
<p>
Retomando nossa introdução:
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Formulação do Problema
</div>
<div class="conteudo normal">
<p>
Retomando nossa introdução:
</p>
<p>
O objetivo do problema da mochila é o de descobrir a maneira mais eficiente de guardar objetos em uma mochila de capacidade limitada para maximizar o valor (a utilidade) dos objetos a serem carregados.
</p>
<p>
Cada objeto possui um peso \( p_i \) e um valor \( v_i \) e a mochila possui uma capacidade máxima de carga \(P\).
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Formulação do Problema
</div>
<div class="conteudo normal">
<p>
Retomando nossa introdução:
</p>
<p>
O objetivo do problema da mochila é o de descobrir a maneira mais eficiente de guardar objetos em uma mochila de capacidade limitada para maximizar o valor (a utilidade) dos objetos a serem carregados.
</p>
<p>
Cada objeto possui um peso \( p_i \) e um valor \( v_i \) e a mochila possui uma capacidade máxima de carga \(P\).
</p>
<p> Qual o modelo do problema? </p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Formulação do Problema
</div>
<div class="conteudo normal">
<p>
Considerando o conjunto \( X \) de \( n \) objetos passíveis de inserção na mochila.
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Formulação do Problema
</div>
<div class="conteudo normal">
<p>
Considerando o conjunto \( X \) de \( n \) objetos passíveis de inserção na mochila.
</p>
<p>
Queremos maximizar a quantidade de itens transportados na mochila? Não necessariamente. Acima de tudo, queremos maximizar a utilidade (o valor) dos itens a serem transportados. Como cada item \(x_i\) possui um valor \(v_i\) (\(i = 1, \cdots, n\)), logo, a utilidade deste transporte - a função que queremos maximizar - é definida por:
</p>
<p>
\[ \sum_{i = 1}^{n}{x_i \cdot v_i} \]
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Formulação do Problema
</div>
<div class="conteudo small">
<p>
Considerando o conjunto \( X \) de \( n \) objetos passíveis de inserção na mochila.
</p>
<p>
Queremos maximizar a quantidade de itens transportados na mochila? Não necessariamente. Acima de tudo, queremos maximizar a utilidade (o valor) dos itens a serem transportados. Como cada item \(x_i\) possui um valor \(v_i\) (\(i = 1, \cdots, n\)), logo, a utilidade deste transporte - a função que queremos maximizar - é definida por:
</p>
<p>
\[ \sum_{i = 1}^{n}{x_i \cdot v_i} \]
</p>
<p>Entretanto, a mochila tem uma carga máxima \( P \) e cada item \( x_i \) possui seu próprio peso \( p_i \). Logo, temos a primeira restrição do problema: que a soma dos pesos de todos os itens transportados não ultrapassem \( P \):</p>
<p>
\[ \sum_{i = 1}^{n}{x_i \cdot p_i} \leq P \]
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Formulação do Problema
</div>
<div class="conteudo small">
<p>
Considerando o conjunto \( X \) de \( n \) objetos passíveis de inserção na mochila.
</p>
<p>
Queremos maximizar a quantidade de itens transportados na mochila? Não necessariamente. Acima de tudo, queremos maximizar a utilidade (o valor) dos itens a serem transportados. Como cada item \(x_i\) possui um valor \(v_i\) (\(i = 1, \cdots, n\)), logo, a utilidade deste transporte - a função que queremos maximizar - é definida por:
</p>
<p>
\[ \sum_{i = 1}^{n}{x_i \cdot v_i} \]
</p>
<p>Entretanto, a mochila tem uma carga máxima \( P \) e cada item \( x_i \) possui seu próprio peso \( p_i \). Logo, temos a primeira restrição do problema: que a soma dos pesos de todos os itens transportados não ultrapassem \( P \):</p>
<p>
\[ \sum_{i = 1}^{n}{x_i \cdot p_i} \leq P \]
</p>
<p>Por fim, em quase todos os casos não convém fracionar itens (Noé não dividiu o elefante ao meio na arca), logo, temos nossas restrições de não-fracionabilidade:</p>
<p>
\[ x_i \in Z_{+} \forall i = 1, \cdots, n \]
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Modelo
</div>
<div class="conteudo">
<p style="margin-left: 50%; margin-right: 30%;">
$$
\begin{align*}
\text{Max Z} = &\sum_{i = 1}^{n}{x_i \cdot v_i} \\
\text{subject to} \\
               &\sum_{i = 1}^{n}{x_i \cdot p_i} \leq P \\
               &x_i \in Z_{+} \forall i = 1, \cdots, n 
\end{align*}
$$
</p>
</div>

---
![bg opacity](./background.png)
<!-- _class: lead -->
# Resolução via Solver

---
![bg opacity](./background.png)
<div class="cabecalho">
Resolução via Solver - Problema
</div>
<div class="conteudo normal">
<p>
Ao viajar de Minas para São Paulo, seus amigos paulistas sempre lhe pedem para vender delícias de nossa terra para eles. Você tem de ir a São Paulo uma vez a cada quinzena para uma reunião de seu empregador, retornando para Belo Horizonte no mesmo dia. Por isso, o empregador não paga despacho de bagagens e devido as taxas de despacho de bagagem serem lesivas ao consumidor, não é possível despachar malas, sendo sua carga máxima restrita a bagagem de mão - 10 kg.
</p>
<p>
Considerando que você tem de levar seu notebook corporativo para a reunião (2kg), bem como, que:
<ul>
<li> 1 lata de doce de leite de viçosa 400g vale R$ 40,00 </li>
<li> 1 garrafa de cachaça Vale Verde (que pesa 750g) vale R$ 80,00 </li>
<li> 1 queijo canastra são roque 1kg vale R$ 65,00 </li>
<li> 1 queijo do serro Juá 450g vale R$ 79,90 </li>
</ul>
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Resolução via Solver - Problema
</div>
<div class="conteudo small">
<p>
Que seus amigos sempre lhe pedem ao menos:
<ul>
<li> 2 latas de doce de leite </li>
<li> 3 garrafas de cachaça </li>
<li> 1 queijo canastra são roque </li>
<li> 1 queijo do serro Juá </li>
</ul>
</p>
<p>
Que seu fornecedor possui no máximo:
<ul>
<li> 20 latas de doce de leite </li>
<li> 30 garrafas de cachaça </li>
<li> 10 queijos canastra São Roque </li>
<li> 5 queijos do serro Juá </li>
</ul>
</p>
<p>
E que os itens não podem ser fracionados para não desvalorizarem, resolva este problema através do problema da mochila pelo solver OR tools do google, especificando o valor máximo que você consegue obter, bem como, a quantidade de produtos que permite alcançar tal valor.
</p>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Resolução via Solver - Variáveis de Decisão
</div>
<div class="conteudo small">
<table>
    <tr>
       <td>Nome</td><td>Variável</td><td>Peso (\(g\))</td><td>Valor (R$)</td>
    </tr>
    <tr>
       <td>Doce de Leite</td><td>\(x_0\)</td><td>400</td><td>40,00</td>
    </tr>
    <tr>
       <td>Cachaça</td><td>\(x_1\)</td><td>750</td><td>80,00</td>
    </tr>
    <tr>
       <td>Queijo Canastra</td><td>\(x_2\)</td><td>1000</td><td>65,00</td>
    </tr>
    <tr>
       <td>Queijo do Serro</td><td>\(x_3\)</td><td>450</td><td>79,90</td>
    </tr>
</table>
</div>

---
![bg opacity](./background.png)
<div class="cabecalho">
Resolução via Solver - Modelo
</div>
<div class="conteudo small">
<p>
\[
\begin{align*}
\text{Max Z} =& 40x_0 + 80x_1 + 65x_2 + 79,9x_3 \\
\text{sujeito à} \\
& 400x_0 + 750x_1 + 1000x_2 + 450x_3 \leq 8000 \\
& 2 \leq x_0 \leq 20 \\
& 3 \leq x_1 \leq 30 \\
& 1 \leq x_2 \leq 10 \\
& 1 \leq x_3 \leq 5 \\
& x_0, x_1, x_2, x_3 \in Z_{+}
\end{align*}
\]
</p>
</div>

---
![bg opacity](./background.png)
<iframe src="http://localhost:8888/notebooks/problema_da_mochila_mineiro.ipynb" width=100% height=100% ></iframe>
