# DerivadaRush

## Visão geral do objetivo

Criar um site onde a pessoa possa **treinar derivadas de forma séria e divertida**, com:

* Conta de usuário e **histórico de desempenho** (acertos, erros, tempo, temas).
* **Banco de questões colaborativo**, onde usuários podem sugerir novas questões de cálculo.
* Vários **modos de treino**:

  * modo rápido com limite de tempo (até 5 minutos),
  * modo sem limite,
  * modo zen (sem pressão de tempo).
* Forma de responder **sem digitar LaTeX**:

  * conectar o celular via **QR code**,
  * tirar foto da solução no papel,
  * o sistema lê a fórmula e corrige automaticamente.
* Correção que não dependa de texto exato:

  * comparar funções pela **diferença numérica/área dos gráficos**, aceitando respostas equivalentes.

---

## Estado atual

* Código implementado: **0**
* O que existe hoje:

  * ideia do produto,
  * visão das funcionalidades finais,
  * noção de que a primeira versão será um **treino local simples em HTML/CSS/JS**.
* Momento atual:

  * ainda na etapa de **desenho conceitual** e escolha da **ordem em que as coisas vão nascer**,
  * começando a preparar a **primeira versão jogável mínima**.

---

## Checklist geral do que precisa ser feito

> A ordem é aproximada; você pode mesclar ou reordenar conforme for desenvolvendo.

* [ ] **Definir o escopo da primeira versão jogável**

  * [ ] Decidir quais funcionalidades mínimas entram no primeiro release (ex.: pool fixo de questões, timer simples, marcar acertos/erros).
  * [ ] Escrever (para você mesmo) uma descrição curta: “O que essa primeira versão já permite fazer? O que ainda não existe?”

* [ ] **Montar o esqueleto do front-end estático**

  * [ ] Criar repositório do projeto e estrutura básica de arquivos (HTML, CSS, JS).
  * [ ] Criar uma tela inicial com:

    * [ ] área para exibir a questão,
    * [ ] área para o timer,
    * [ ] botões básicos de controle (iniciar treino, próxima questão, mostrar resposta, acertei/errei).
  * [ ] Garantir que você consegue mexer em layout e comportamento sem se perder (estrutura mínima organizada).

* [ ] **Construir o treino local single-player (sem servidor)**

  * [ ] Definir um conjunto inicial de questões de derivadas (em qualquer formato simples).
  * [ ] Implementar lógica de mostrar questão, sortear próximas e evitar repetições óbvias na mesma sessão.
  * [ ] Adicionar modos de timer: limitado, ilimitado e zen (comportamento simples, sem obsessão com detalhes).
  * [ ] Permitir que o usuário marque manualmente acertos/erros e ver um resumo básico na tela.
  * [ ] (Opcional nesta etapa) Guardar estatísticas simples no navegador para não perder tudo ao recarregar.

* [ ] **Organizar o “motor de treino” para ser reaproveitável**

  * [ ] Separar mentalmente (e minimamente no código) o que é:

    * [ ] regra de treino (como escolhe questões, como conta acertos/erros),
    * [ ] interface (como as coisas aparecem na tela),
    * [ ] acesso a dados (de onde vêm as questões e para onde vão as estatísticas).
  * [ ] Deixar claro onde você vai “trocar a fonte de dados” no futuro (quando passar de array local para API/banco).
  * [ ] Refatorar o necessário para que adicionar novas telas/funcionalidades não vire uma bagunça total.

* [ ] **Escolher a stack de backend e banco de dados**

  * [ ] Decidir qual tecnologia vai usar para o servidor (ex.: Node.js/Express ou Next.js, etc.).
  * [ ] Decidir qual banco relacional usar (provavelmente PostgreSQL).
  * [ ] Definir, em alto nível, quais entidades serão persistidas:

    * [ ] usuários,
    * [ ] questões,
    * [ ] tentativas/respostas,
    * [ ] possivelmente sessões de treino.

* [ ] **Dar identidade ao usuário (login simples)**

  * [ ] Implementar uma forma de criar conta e entrar (não precisa ser ultra-complexo no começo).
  * [ ] Fazer o front-end conversar com o backend para:

    * [ ] registrar novo usuário,
    * [ ] autenticar,
    * [ ] saber “quem está logado” durante o treino.
  * [ ] Associar o progresso do treino a um usuário identificado, não só à máquina/navegador.

* [ ] **Persistir histórico em banco de dados**

  * [ ] Criar as tabelas básicas para usuários, questões e tentativas.
  * [ ] Adaptar o backend para salvar:

    * [ ] tentativas de questões,
    * [ ] acertos/erros,
    * [ ] tempos de resolução (se fizer sentido).
  * [ ] Fazer o front buscar estatísticas reais (do banco) em vez de depender só de dados locais.
  * [ ] Garantir que o usuário vê o histórico dele mesmo se mudar de dispositivo ou limpar o navegador.

* [ ] **Transformar o banco de questões em algo colaborativo**

  * [ ] Permitir que usuários proponham novas questões (num formato mínimo, sem precisar resolver todos detalhes de UX).
  * [ ] Adicionar algum mecanismo de aprovação/moderação:

    * [ ] flag simples “aprovada / pendente” já é suficiente no começo.
  * [ ] Usar esse banco colaborativo como fonte de questões para o treino, com filtro para só usar itens aprovados.
  * [ ] Pensar em formas simples de organização: temas, níveis, tags básicas.

* [ ] **Adicionar correção automática baseada na matemática das respostas**

  * [ ] Decidir como representar internamente as expressões matemáticas (texto, LaTeX, outro formato).
  * [ ] Implementar uma estratégia numérica para comparar a resposta do usuário com a resposta oficial:

    * [ ] avaliar as duas funções em vários pontos,
    * [ ] definir tolerâncias para dizer “equivalente” ou “errado”.
  * [ ] Integrar essa correção automática ao fluxo de treino:

    * [ ] o usuário responde (digitando ou outra forma),
    * [ ] o sistema avalia e registra o resultado automaticamente,
    * [ ] ainda permitindo ajuste manual se necessário.

* [ ] **Permitir uso combinado de PC e celular (sessões compartilhadas via QR)**

  * [ ] Definir o conceito de uma sessão de treino que pode ser acessada em mais de um dispositivo.
  * [ ] Implementar a criação de uma sessão identificável (por um token, por exemplo).
  * [ ] Mostrar um QR code no PC que aponta para a sessão corrente.
  * [ ] Criar uma interface mínima no celular que, ao ler esse QR, entra na mesma sessão e consegue interagir com o treino (enviar resposta, por exemplo).
  * [ ] Pensar em um esquema simples de sincronização entre PC e celular (mesmo que comece com algo bem básico).

* [ ] **Integrar entrada por foto (OCR de fórmulas)**

  * [ ] Escolher um serviço ou biblioteca de OCR adequado para fórmulas matemáticas (pelo menos em nível experimental).
  * [ ] Permitir que o celular capture uma foto da resposta escrita no papel.
  * [ ] Mandar essa foto para o backend, que chama o serviço de OCR e tenta extrair a expressão.
  * [ ] Reaproveitar a lógica de correção numérica para avaliar a resposta capturada.
  * [ ] Criar um fluxo de confirmação:

    * [ ] mostrar ao usuário a expressão reconhecida,
    * [ ] permitir correção manual antes da avaliação, quando necessário.

* [ ] **Polir UX, visual e segurança básica ao longo do caminho**

  * [ ] Melhorar gradualmente a experiência de uso:

    * [ ] fluidez dos fluxos de treino,
    * [ ] tipografia, cores, feedback visual.
  * [ ] Ajustar mensagens, textos, nomes de modos e telas para ficarem claros.
  * [ ] Cuidar, de forma incremental, dos pontos de segurança mais básicos:

    * [ ] proteção de dados de usuário,
    * [ ] validação de entradas,
    * [ ] regras mínimas de privacidade.
