# Cap 1 - Conceitos Básicos

## 1.2 - Validação, Verificação e Teste (VV&T)

A construção de software é complexa e sujeita a **erros humanos**, mesmo com o uso de métodos e ferramentas adequados.

Para reduzir problemas antes da liberação do software, utilizam-se atividades de **Validação, Verificação e Teste (VV&T)**, cujo objetivo é garantir que:

- O processo de desenvolvimento esteja correto.
- O produto final esteja em conformidade com a especificação.

As atividades de VV&T podem ocorrer durante todo o ciclo de desenvolvimento e são classificadas em:

- **Estáticas**: não exigem execução do programa (ex.: revisões técnicas).
- **Dinâmicas**: baseiam-se na execução do programa ou modelo.

## 1.3 - Termos do jargão

Definições fundamentais:

- **Engano (mistake)**: ação humana incorreta.
- **Defeito (fault)**: problema no código ou definição (resultado do engano).
- **Erro (error)**: estado incorreto durante a execução.
- **Falha (failure)**: resultado externo incorreto percebido pelo usuário (saída incorreta).

Relação entre os termos: Engano → Defeito → Erro → Falha.

Outros conceitos importantes:

- **Domínio de entrada (D(P))**: conjunto de todos os valores possíveis de entrada de um programa.
- **Domínio de saída**: conjunto de todos os possíveis resultados produzidos.
- **Dado de teste**: um elemento do domínio de entrada.
- **Caso de teste**: par (entrada, resultado esperado).
- **Conjunto de teste (T)**: conjunto de casos de teste utilizados.
- **Programa executado (P)**: programa que processa os casos de teste.
- **Oráculo (S(P))**: mecanismo (humano ou automatizado) que decide se a saída está correta com base na especificação do programa.

## 1.4 - Fases da atividade de teste

A atividade de teste é dividida em fases com objetivos distintos:

1. **Teste de Unidade (Unitário)**
   - Foco nas menores partes do sistema (funções, métodos, classes).
     - No paradigma Procedural (Procedimental), é chamado _Teste Intraprocedimental_;
     - No paradigma OO, o teste unitário também é conhecido como _Teste Intramétodo_.
   - Identifica erros de algoritmo, estrutura de dados ou programação.
   - Pode ser realizado pelo próprio desenvolvedor.
   - Executado durante a implementação.
2. **Teste de Integração**
   - Verifica a interação entre unidades.
     - _Interprocedimental_ ou _Intermétodo_.
   - Foco na estrutura e comunicação entre componentes.
   - Geralmente executado pela equipe de desenvolvimento.
3. **Teste de Sistema**
   - Avalia o sistema completo.
   - Verifica requisitos funcionais e não funcionais (segurança, desempenho, robustez).
   - Pode ser conduzido por equipe independente.
4. **Teste de Regressão**
   - Executado após modificações no software.
   - Garante que mudanças não introduziram novos defeitos.
   - Verifica manutenção da funcionalidade anterior.
5. **Teste de Aceitação**
   - Realizado por alguém representando o usuário final ou cliente.
   - Verifica se o sistema atende às necessidades e requisitos do cliente.
   - Executado em ambiente simulado de produção (sem mocks), utilizando dados reais.

Cada teste deve ter seus casos de sucesso e falha e devem cobrir o máximo de caminhos possíveis.

## 1.5 Técnicas e critérios de teste

O domínio de entrada de um programa pode ser extremamente grande, tornando o teste exaustivo impraticável.

**Solução**: selecionar um subconjunto representativo do domínio por meio de subdomínios de teste, que agrupam entradas com comportamento esperado semelhante.

Duas estratégias principais:

- **Teste aleatório**: seleção probabilística de muitos casos de teste.
- **Teste de partição (ou de subdomínios)**: identificação explícita dos subdomínios e seleção de representantes de cada um (foco do livro).

Para definir subdomínios, utilizam-se **critérios de teste**, que estabelecem regras para geração de requisitos de teste.

Tipos de critérios:

1. **Funcionais** - baseados na especificação.
2. **Estruturais** - baseados no código.
3. **Baseados em defeitos** - focados em erros típicos.

# Cap 6 - Teste Orientado a Objetos e de Componentes

## 6.3 - Tipos de defeitos em POO

###### pág 4

A programação orientada a objetos (POO) possui construções poderosas que aumentam o risco de erros e a complexidade de teste. O encapsulamento, a composição de subsistemas e o acoplamento dinâmico permitem que o comportamento do sistema seja definido apenas em tempo de execução.

A herança cria novos contextos a cada nível da hierarquia, não garantindo que comportamentos corretos em níveis superiores permaneçam corretos nos inferiores. Em hierarquias complexas, especialmente com herança múltipla e muitos métodos polimórficos, o esforço de teste aumenta significativamente. Polimorfismo e acoplamento dinâmico ampliam o número de caminhos de execução, enquanto o encapsulamento pode dificultar a observação do estado interno dos objetos.

O reúso também impõe desafios: componentes reutilizáveis devem ser altamente confiáveis e, mesmo que já tenham sido testados, precisam ser retestados no novo contexto de uso.

Embora a POO reduza alguns defeitos comuns na programação procedural (como problemas com variáveis globais e fluxo de controle extenso), ela não elimina erros de codificação. Além disso, o grande número de métodos e interfaces em sistemas OO pode aumentar defeitos relacionados a interfaces.

### 6.3.1 - Efeitos colaterais da programação OO

### Encapsulamento

O encapsulamento controla a visibilidade de atributos e métodos, promovendo ocultação de informação e modularidade.

Apesar de não causar defeitos diretamente, pode dificultar testes, pois limita o acesso ao estado interno dos objetos. O teste exige inspeção e modificação do estado, o que pode requerer métodos auxiliares (get/set) ou mecanismos como reflexão. Algumas linguagens restringem a reflexão a métodos públicos e protegidos, dificultando ainda mais o processo.

### Classes abstratas e genéricas

**Classes abstratas** fornecem apenas interface, sem implementação. Não podem ser instanciadas, e seu teste só é possível após especialização em classes concretas. Métodos concretos que dependem de métodos abstratos podem ter teste dificultado.

**Classes genéricas** permitem declarar atributos e parâmetros que podem assumir diferentes tipos específicos, favorecendo o reúso e o acoplamento dinâmico.

Principais desafios de teste:

- Necessidade de escolher tipos específicos para instanciar parâmetros genéricos durante o teste.
- Risco de escolha inadequada de tipos, comprometendo a cobertura.
- Necessidade de reteste das subclasses quando a classe genérica é modificada.

### Herança

A herança promove reúso por compartilhamento de características, mas pode enfraquecer o encapsulamento.

É essencial compreender as classes ancestrais ao implementar subclasses; caso contrário, podem surgir violações de condições implícitas. Hierarquias extensas dificultam compreensão, aumentam a probabilidade de erros e reduzem a testabilidade.

### Herança múltipla

Permite que uma subclasse herde de duas ou mais superclasses. Embora simples sintaticamente, pode causar grandes impactos semânticos.

Principais riscos:

- Mudanças em superclasses podem gerar interações inesperadas na subclasse.
- Métodos herdados podem comportar-se de forma diferente no novo contexto.
- Herança repetida (uma superclasse aparece mais de uma vez na hierarquia) aumenta conflitos de nomes e risco de comportamento inesperado.
- Problemas relacionados à visibilidade, herança pública/privada e diferenças entre classes abstratas e concretas.

### Polimorfismo

#### 1. Indecidibilidade no acoplamento dinâmico

Em chamadas polimórficas, não é possível determinar em tempo de compilação qual método será executado — essa decisão ocorre apenas em tempo de execução.

Problemas:

- Sobrescrita pode alterar pré e pós-condições.
- Cada possível ligação polimórfica representa uma computação distinta.
- Funcionamento correto em alguns casos não garante correção em todos.
- Risco de envio de mensagens à classe errada.

#### 2. Extensibilidade de hierarquias

Não é possível criar um conjunto de testes que cubra todas as classes possíveis em hierarquias extensíveis.

Solução sugerida: uso de assertivas (pré e pós-condições), que devem ser refinadas — nunca relaxadas — em métodos sobrescritos, ajudando a detectar usos indevidos.

### Containers heterogêneos e type casting

Containers heterogêneos armazenam objetos de diferentes classes. Para acessar métodos específicos, pode ser necessário realizar conversão de tipos (casting).

Possíveis falhas:

- **Downcasting incorreto**: conversão para classe incompatível.
- Uso de objeto não convertido para invocar método inexistente ou inadequado.

Esses erros geralmente não são detectados em compilação, exigindo atenção especial nos testes.

### Outros problemas

#### Sequência de mensagens

Em POO, métodos devem ser executados em sequências corretas. Determinar quais sequências são válidas é um desafio importante.

#### Estados dos objetos

Objetos encapsulam estado, que pode assumir diferentes configurações ao longo da execução.

Existem duas definições de estado:

- **Estado normal**: todas as combinações possíveis de valores dos atributos (potencialmente infinito).
- **Estado baseado em projeto**: conjunto reduzido de estados relevantes para o comportamento observado.

A abordagem baseada em projeto reduz significativamente o número de casos de teste necessários.

Ao executar um método, quatro situações podem ocorrer:

1. Transição para novo estado válido.
2. Permanência no mesmo estado.
3. Transição para estado indefinido.
4. Transição para estado inválido.

As situações 3 e 4 caracterizam erro. As situações 1 e 2 também podem indicar erro, dependendo do comportamento esperado.

Conclusão: em programas OO, o estado do objeto deve fazer parte do caso de teste. Apenas entradas e saídas não são suficientes; é necessário considerar explicitamente as mudanças de estado na validação do sistema.

## 6.4 - Fases de teste OO

###### pág 11

Segundo o padrão _IEEE 610.12-1990 [49]_, uma unidade é um componente de software que não pode ser subdividido. **Em POO, pode-se considerar que a menor unidade a ser testada é um método**, sendo que a classe à qual o método pertence pode ser vista como o driver do método. Sem a existência da classe, não é possível executar um método. No paradigma procedimental, o teste de unidade também é chamado de intraprocedimental, e no paradigma de programação OO, intramétodo [40].  
Por definição, uma classe engloba um conjunto de atributos e métodos que manipulam esses atributos. Assim, considerando uma única classe, já é possível pensar-se em teste de integração. **Métodos da mesma classe podem interagir entre si para desempenhar funções específicas que caracterizam uma integração entre métodos** que deve ser testada: teste intermétodo [40]. No paradigma procedimental, esta fase de teste também pode ser chamada de teste interprocedimental.

###### pág 12

Harrold e Rothermel [40] definem ainda outros dois tipos de teste para POO: _teste intraclasse e teste interclasse_. **No teste intraclasse são testadas interações entre métodos públicos (de uma mesma classe) fazendo-se chamadas a esses métodos em diferentes sequências**. O objetivo é identificar possíveis sequências de ativação de métodos inválidas que levem o objeto a um estado inconsistente. Segundo os autores, como o usuário pode invocar sequências de métodos públicos em uma ordem indeterminada, o teste
intraclasse aumenta a confiança de que diferentes sequências de chamadas interagem adequadamente. **No teste interclasse, o mesmo conceito de invocação de métodos públicos em diferentes sequências é utilizado; entretanto, esses métodos públicos não necessitam estar na mesma classe**.

###### pág 13

(...) Segundo Colanzi [20], o teste de POO é organizado em quatro fases:

- **Teste de unidade**: testa os métodos individualmente;
- **Teste de classe**: testa a interação entre métodos de uma classe;
- **Teste de integração**: testa a interação entre classes do sistema; e
- **Teste de sistema**: testa a funcionalidade do sistema como um todo.

Considerando-se o método como a menor unidade, o teste de classe, proposto por Colanzi [20], pode ser visto como parte do teste de integração, juntamente com o teste intraclasse e interclasses.

## 6.5 - Estratégias, técnicas e critérios de teste OO

###### pág 13

Howden [48] define que o teste pode ser classificado de duas maneiras: **teste baseado em especificação e teste baseado em programa**, dependendo em qual nível os critérios de teste são aplicados...

> O _teste baseado em especificação_ é aquele onde os critérios de teste são derivados da especificação do software, sem considerar a estrutura interna do programa. Já o _teste baseado em programa_ é aquele onde os critérios de teste são derivados da estrutura interna do programa, como o código-fonte, a arquitetura ou o design do software.

###### pág 14

Um problema com os critérios de teste baseados em especificação é a dificuldade de quantificar a atividade de teste, visto que não se pode garantir que partes essenciais ou críticas do programa sejam executadas. Outro problema é que o teste baseado em especificação está sujeito às inconsistências decorrentes de uma especificação de má qualidade, pois é ela a base da qual são derivados os casos de teste. Como, em geral, a especificação é feita de forma descritiva e informal, os requisitos derivados da especificação também são, de certa maneira, descritivos e informais, dificultando a automatização dos critérios funcionais.

Entre os critérios de teste baseados em programa, destacam-se os critérios estruturais baseados em fluxo de controle e de dados e os critérios baseados em mutação. O teste de mutação e os operadores definidos para linguagens OO são descritos no Capítulo 5 e os critérios estruturais para POO são descritos a seguir.

### 6.5.1 - Critérios estruturais

Para viabilizar o teste de fluxo de dados nos níveis intramétodo, intermétodos e intraclasse, Harrold e Rothermel [40] propuseram as seguintes representações de programa: **Grafo de Chamadas de Classe** (CCG - class call graph), o **Grafo de Fluxo de Controle de Classe** (CCFG - class control flow graph) e o CCFG encapsulado (framed CCFG).

> O _grafo de chamadas de classe_ é um grafo direcionado onde os nós representam métodos e as arestas representam chamadas entre métodos. O _grafo de fluxo de controle de classe_ é um grafo direcionado onde os nós representam blocos básicos de código e as arestas representam o fluxo de controle entre esses blocos.  
> O CCFG encapsulado é uma extensão do CCFG que inclui informações sobre o estado do objeto, permitindo a análise de dependências entre métodos com base no estado do objeto.

###### pág 15

Com base nesses níveis de teste, Harrold e Rothermel [40] definiram pares de definição e uso (**Pares DEF-USO**) que permitem avaliar relações de fluxo de dados em POO com base na definição de um dado e o uso desse mesmo dado, seguem-se estas definições:

| Tipo        | Onde ocorre                                             | O que avalia                                    |
| ----------- | ------------------------------------------------------- | ----------------------------------------------- |
| Intramétodo | Dentro do mesmo método                                  | Fluxo de dados interno                          |
| Intermétodo | Entre métodos na mesma execução                         | Fluxo de dados entre métodos                    |
| Intraclasse | Entre diferentes chamadas de métodos públicos da classe | Fluxo de dados entre execuções dentro da classe |

###### pág 20

O chamado Grafo de Instruções (GI) representa o fluxo
de controle das instruções de bytecode... Cada nó do grafo corresponde a uma única instrução de bytecode...

Desse modo, é percorrido o GI e, por meio do agrupamento de diversas instruções individuais, são formados blocos de instruções que dão origem a um novo nó no Grafo Def-Uso (GDU). Os conjuntos de variáveis definidas e usadas, relacionados aos nós do GDU são obtidos por meio da união dos conjuntos individuais de cada instrução que compõe o bloco. O GDU representa o modelo base que é utilizado para se derivarem requisitos de teste de fluxo de controle e de dados intramétodo para o teste de programas e componentes Java.

> O GDU é originado a partir do GI, porém considerando apenas os nós onde ocorrem as definições ou usos dos dados definidos.

Critérios de teste baseados em fluxo de controle:

| Critério     | Descrição                                                                                                         |
| ------------ | ----------------------------------------------------------------------------------------------------------------- |
| All-Nodes ei | Exige a cobertura de todos os comandos não relacionados ao tratamento de exceção                                  |
| All-Nodes ed | Exige a cobertura de todos os comandos relacionados ao tratamento de exceção                                      |
| All-Edges ei | Exige cobertura de todos os desvios condicionais do método (desvios não decorrentes do lançamento de uma exceção) |
| All-Edges ed | Exige cobertura de todos os desvios de execução decorrentes do lançamento de uma exceção                          |

Critérios de teste baseados em fluxo de dados:

| Critério     | Descrição                                                                                                                                       |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| All-Defs     | Exige que, para cada definição de uma variável, ao menos um caminho até algum uso dessa definição seja exercitado                               |
| All-Uses     | Garante que todos os caminhos de cada definição para cada um de seus usos possíveis (sejam eles de computação ou de predicado) sejam testados   |
| All-P-Uses   | Foca nos usos de predicado (decisões, como em um if), exigindo que todos os caminhos de uma definição para usos em decisões sejam cobertos      |
| All-C-Uses   | Foca nos usos computacionais (cálculos ou saídas), garantindo caminhos de uma definição para seus usos em expressões matemáticas ou atribuições |
| All-DU-Paths | O critério mais rigoroso, que exige testar todos os caminhos simples (sem laços repetidos) entre cada definição e cada um de seus usos          |

###### pág 27

Com base em um estudo experimental realizado em um trabalho anterior com um conjunto significativo de programas escritos em Java, Souter et al. [94] chegaram à conclusão de que a utilização do projeto de software OO resulta em programas com muitos métodos, cada um com um número limitado de sentenças e com fluxo de controle intramétodo bastante simples.  
Um sumário das conclusões a que chegaram é destacado a seguir:

- O número de instruções condicionais dentro de um método é muitas vezes 0, e em média variou entre 0 e 3;
- Muitas vezes uma pequena porcentagem dos métodos definidos em uma classe servidora é realmente utilizada por uma dada classe cliente;
- Apenas aproximadamente metade dos métodos utilizados pelas classes clientes de fato alteram o estado do objeto utilizado;
- Manipulações de variáveis de tipos primitivos tipicamente utilizadas como base no teste de fluxo de dados ocorrem poucas vezes em programas OO;
- As computações necessárias são na maioria das vezes alcançadas a partir da manipulação de variáveis de instância de objetos via chamadas a métodos.

Esses resultados sugerem que o **teste baseado em fluxo de controle pode não ser a maneira mais efetiva de se revelar o comportamento de um programa OO**. Além disso, Souter e Pollock [92] argumentam que as **abordagens de fluxo de dados**, por exemplo, a de Harrold e Rothermel [40] discutida anteriormente, **não atingem o objetivo principal do teste de fluxo de dados OO de levar em conta as manipulações de objetos**. Com isso, as associações de fluxo de dados obtidas dos critérios de Harrold e Rothermel [40] seriam classificadas como sendo livres de contexto (context-free), uma vez que podem ser cobertas sem considerar um contexto específico.

### 6.5.2 Estratégia de Teste Incremental Hierárquica

###### pág 28

Como descrito anteriormente, a herança é um mecanismo que permite tanto o compartilhamento da especificação da classe como o do código-fonte para o desenvolvimento de novas classes baseadas em classes já existentes. A definição de uma subclasse é dada por um modificador que estabelece as diferenças ou alterações nos elementos que compõem a superclasse. Com isso, um modificador e a superclasse são utilizados na criação de uma subclasse. A Figura 6.8 ilustra como transformar uma superclasse P com um modificador M em uma subclasse R. O operador de composição ⊗ une simbolicamente M e P , produzindo R, sendo R = P ⊗ M.

O projetista da subclasse especifica o modificador, o qual pode conter diferentes tipos de elementos que alteram a superclasse. Os seis tipos de elementos são:

1. **Novo**: definido apenas na subclasse → precisa de teste completo.
2. **Recursivo**: herdado sem modificação → reteste limitado.
3. **Redefinido**: mesma assinatura, nova implementação → reteste; pode reutilizar testes de especificação.
4. **Virtual-novo**: declarado na subclasse com implementação incompleta → teste completo.
5. **Virtual-recursivo**: herdado virtual sem modificação → reteste limitado.
6. **Virtual-redefinido**: método virtual redefinido → reteste; reutilização possível de testes baseados em especificação.

#### Teste da Superclasse

O teste ocorre em três níveis:

1. Teste Intramétodo

- Teste individual de cada método.
- Uso de **critérios funcionais e estruturais (fluxo de dados)**.
- Gera histórico de teste

2. Teste Intraclasse

- Testa interações entre métodos da mesma classe.
- Usa **Grafo de Classe**:
  - Nó = método
  - Arco = chamada/mensagem

3. Teste Interclasses

- Testa interação entre métodos de classes diferentes.
- Mesma estratégia do teste intraclasse.

##### Histórico de Teste

Todos os testes executados são armazenados.  
Para métodos virtuais sem implementação:

- Apenas testes baseados em especificação são criados.
- Execução ocorre somente após implementação em subclasses.

#### Teste da Subclasse

A história da subclasse é construída a partir de:

- H(P) → histórico da superclasse
- G(P) → grafo da superclasse
- M → modificador

O algoritmo **TestSubClass**:

1. Inicializa histórico e grafo da subclasse com os da superclasse.
2. Para cada elemento do modificador:
   - **Novo / virtual-novo**:
     - Gerar testes de especificação e implementação.
     - Gerar testes de integração.

   - **Recursivo / virtual-recursivo**:
     - Reutilizar testes.
     - Retestar apenas se houver impacto.

   - **Redefinido / virtual-redefinido**:
     - Gerar novos testes de implementação.
     - Reutilizar testes de especificação se possível.
     - Atualizar testes de integração.

## 6.6 Teste de Componentes

###### pág 37

Como definido por Szyperski [95], um componente de software é uma unidade de composição de sistemas com especificações contratuais de interfaces e explícita dependência de contexto. Um componente de software pode ser desenvolvido independentemente e ser utilizado por terceiros para composição. Componentes de software existem em diferentes formas.

Características:

- Desenvolvimento independente.
- Reutilização por terceiros.
- Pode variar de classe simples a componentes complexos (JavaBeans, EJB, COM).
- Reuso mais genérico que OO tradicional.

###### pág 38

- **Perspectiva do Cliente**
  - _Ausência de código-fonte_
    - Impossibilita critérios estruturais (fluxo de dados, mutação).
  - _Multilinguagem_
    - Ferramentas dependem da linguagem.
  - _Funcionalidade excedente_
    - Parte do componente não utilizada afeta métricas de cobertura.
    - Elementos não utilizados devem ser excluídos da avaliação.
- **Perspectiva do Desenvolvedor**
  - Tem acesso ao código-fonte.
  - Teste similar a unidade/integração tradicional.
  - Critérios simples (cobertura de comandos) são insuficientes.
  - Custo de defeito pós-lançamento é alto.

### 6.6.1 Estratégias e Critérios de Teste

- Baseados apenas na especificação.
- Não garantem cobertura de partes críticas da implementação.

#### Alternativas Estruturais sem Código-Fonte

1. **Reflexão Computacional**

- Inspeciona estrutura interna.
- Permite invocação automática de métodos.
- Automatiza geração e execução de testes.
- Limitação:
  - Não garante cobertura estrutural completa.

2. **Polimorfismo (Wrapper)**

- Métodos polimórficos verificam:
  - Pré-condições
  - Pós-condições
- Similar a empacotador.
- Limitações:
  - Exige especificação formal.
  - Não garante cobertura de código.
  - Necessita geração automática de wrappers.

3. **Metadados**

- Fornecem informações estruturais e comportamentais.
- Podem incluir dados úteis para teste.
- Problemas:
  - Não há padrão consolidado.
  - Exige esforço adicional do desenvolvedor.

4. **Grafo Def-Uso baseado em Especificação**

- Constrói dependências a partir da especificação.
- Permite uso de critérios de fluxo de dados.
- Limitação:
  - Cobertura da especificação ≠ cobertura do código.

5. **Componentes Autotestáveis**

- Testes embutidos no componente.
- Podem incluir:
  - Verificação de pré/pós-condições
  - Histórico de verificação
  - Serviços de autoteste
- Limitações:
  - Maior custo de desenvolvimento.
  - Falta de padronização.

6. **Análise em Bytecode Java**

- Permite aplicar critérios estruturais sem código-fonte.
- Duas abordagens:
- Análise de dependência em bytecode.
- Diferença nos modelos de fluxo de dados:
  - Modelo 1: apenas variáveis locais.
  - Modelo 2: inclui atributos de instância, classe e agregados.
- Modelo mais abrangente representa melhor interações intramétodo.

### 6.6.2 Problemas no Teste de Integração

- Principais Dificuldades
  1. Código-fonte indisponível.
  2. Dependência de contexto.
  3. Documentação insuficiente.
  4. Dependência do cliente em relação ao produtor.

- Soluções
  1. Mitigar falta de informação
  2. Facilitar troca de informação produtor–cliente

- Propostas incluem
  - Encapsular informações úteis dentro do componente.

- Problema
  - Definem como fornecer informação, mas não especificam claramente quais informações devem ser fornecidas.
