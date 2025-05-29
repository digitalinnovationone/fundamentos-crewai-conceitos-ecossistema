# Aula 4: Conceitos de Agentes, Tarefas e Papéis

## Conteúdo Teórico (Entendendo Agentes, Tarefas e Papéis no CrewAI)

*   **Objetivo:** Apresentar e diferenciar os conceitos fundamentais de agentes, tarefas e papéis no CrewAI, e como eles colaboram.

Olá! Na Aula 3, montamos a "casa" para o nosso projeto CrewAI, criando a estrutura de pastas e arquivos essenciais. Agora, na Aula 4, vamos conhecer os "moradores" e suas "funções": os conceitos de Agentes, Tarefas e Papéis. Esses são elementos centrais no CrewAI para a construção de soluções inteligentes.

É comum confundir esses termos no começo, então vamos definir cada um claramente.

**O que é um Agente (Agent) no CrewAI?**
Um Agente é uma **entidade autônoma** que faz parte da sua "tripulação" (Crew). Ele é o "quem" realiza as ações no seu projeto.
*   **Características de um Agente:**
    *   Possui um **Papel (Role)**.
    *   Possui um **Objetivo (Goal)**.
    *   Possui uma **História de Fundo (Backstory)** (opcional, mas ajuda a definir o comportamento).
    *   Pode ter **Ferramentas (Tools)** para interagir com o mundo externo.
    *   Pode ter a capacidade de **Delegar** tarefas para outros agentes.
    *   Pode ter **Memória** para lembrar de conversas passadas.

Pense em um agente como um membro especializado de uma equipe. Por exemplo, um "Pesquisador de Dados" ou um "Analista Financeiro".

**O que é um Papel (Role) no CrewAI?**
O Papel define a **função ou responsabilidade** de um agente dentro da equipe. É a "especialidade" do agente.
*   Um papel dá contexto ao agente, influenciando como ele pensa e interage.
*   Exemplos de papéis: "Gerente de Projetos", "Editor de Conteúdo", "Suporte ao Cliente".

A distinção entre tarefa e papel é fundamental: o papel é quem o agente é e o que ele representa na equipe, a tarefa é o que ele faz.

**O que é uma Tarefa (Task) no CrewAI?**
A Tarefa é uma **ação específica a ser realizada** ou um objetivo pontual a ser alcançado por um agente. É o "o quê" fazer.
*   **Características de uma Tarefa:**
    *   Possui uma **Descrição (Description)** clara do que precisa ser feito.
    *   Possui um **Resultado Esperado (Expected Output)**.
    *   É **atribuída** a um agente específico.
    *   Pode usar **Ferramentas**.
    *   Pode ter **Parâmetros** para personalizá-la.
    *   Pode ter **Condições** para sua execução.
    *   Pode gerar um **arquivo de saída** (`output_file`).

Exemplos de tarefas: "Pesquisar as últimas notícias sobre IA", "Escrever um rascunho de e-mail de marketing", "Gerar um relatório de vendas".

**Como Agentes, Tarefas e Papéis Colaboram?**
A beleza do CrewAI é a **colaboração**.
*   Você define uma **Tripulação (Crew)**.
*   Nessa tripulação, você tem **Agentes**, cada um com um **Papel** definido e, opcionalmente, com ferramentas específicas.
*   Você define uma série de **Tarefas** que precisam ser completadas.
*   Você **atribui** cada Tarefa a um **Agente** que tenha o Papel e as ferramentas adequadas para realizá-la.
*   Você define um **Processo** (sequencial ou hierárquico) que dita como essas tarefas serão executadas pelos agentes.
*   Os agentes executam suas tarefas designadas, colaborando entre si, passando informações ou resultados de uma tarefa para outra, seguindo o fluxo do processo.

É como uma equipe de projeto: o Gerente (Papel) atribui a tarefa de "Pesquisar" (Tarefa) ao Pesquisador (Agente com Papel de Pesquisador), que usa a Internet (Ferramenta). O resultado da pesquisa pode ser passado para o Redator (Agente com Papel de Redator) que tem a tarefa de "Escrever".

**Perguntas Frequentes dos Estudantes:**
*   *Qual a diferença entre agente, tarefa e papel?* Agente é a entidade que age, Papel é a função ou especialidade do agente, Tarefa é a ação ou objetivo específico que o agente realiza. Pense: **Agente = Quem**, **Papel = Qual a função**, **Tarefa = O Quê fazer**.
*   *Como criar um agente com múltiplas tarefas?* Você define o agente uma vez, e pode atribuir várias tarefas a ele. O CrewAI orquestra a execução dessas tarefas para o agente.
*   *É possível alterar os papéis de um agente durante a execução?* O conceito padrão no CrewAI é que o papel é definido na criação do agente. Ajustes dinâmicos em tempo real são mais avançados e geralmente envolvem lógicas mais complexas ou a definição de múltiplos agentes com papéis ligeiramente diferentes para cenários específicos.
*   *Como monitorar o desempenho das tarefas atribuídas?* O CrewAI (especialmente na versão Enterprise ou com integrações) oferece ferramentas de monitoramento e logs para acompanhar a execução das tarefas e o comportamento dos agentes. Analisar os logs é fundamental.
*   *Existem limitações para o número de tarefas ou papéis?* Não há limites técnicos rígidos documentados nos fontes para iniciantes, mas a complexidade aumenta com mais agentes, tarefas e papéis. Boas práticas sugerem manter o design focado e modular para facilitar o gerenciamento.

## Conteúdo Prático (Projeto Hands-On: Implementando Agentes e Tarefas)

*   **Objetivo:** Implementar a definição de um agente básico e uma tarefa simples dentro da estrutura de projeto criada na Aula 3.

Excelente! Agora que entendemos os conceitos de Agentes, Tarefas e Papéis, vamos usá-los para dar vida à estrutura do projeto que criamos na Aula 3. Nosso objetivo é definir um agente simples e uma tarefa para ele executar. Resolveremos o problema de como traduzir os conceitos em código.

Vamos continuar no projeto `meu_primeiro_crewai` que estruturamos.

**(Passo a Passo no Vídeo, mostrando a tela e o terminal/IDE):**

1.  **Abrir o Projeto na IDE:** Abra a pasta `meu_primeiro_crewai` na sua IDE favorita.
2.  **Instalar o CrewAI:** Primeiro, precisamos instalar a biblioteca.
    *   Abra o terminal *na pasta raiz do projeto (`meu_primeiro_crewai/`)*.
    *   Atualize o arquivo `requirements.txt` adicionando a linha `crewai`.
    *   Comando de instalação: `pip install -r requirements.txt` (ou use `uv` ou Poetry se já estiver configurado, mas para iniciantes, `pip` é simples e comum). Explique rapidamente que este comando lê o `requirements.txt` e instala as bibliotecas listadas.
    *   (Opcional, mas recomendado) Crie um ambiente virtual primeiro: `python -m venv venv` e depois ative: `source venv/bin/activate` (Linux/macOS) ou `.\venv\Scripts\activate` (Windows PowerShell). Instale as libs dentro do ambiente virtual. Explique que ambientes virtuais mantêm as instalações de bibliotecas separadas para cada projeto. Adicione a pasta `venv/` ao `.gitignore`.
3.  **Definir o Agente (`config/agents.yaml`):**
    *   Abra o arquivo `src/meu_primeiro_crewai/config/agents.yaml`.
    *   Vamos definir um agente simples, por exemplo, um "Escritor de Rascunhos". Digite o seguinte YAML:
        ```yaml
        rascunhador:
          role: >
            Escritor de Rascunhos Criativos
          goal: >
            Criar rascunhos iniciais para diferentes tipos de conteúdo.
          backstory: >
            Você é um escritor habilidoso que gera rapidamente ideias e estruturas para textos.
          verbose: true # Para ver o que o agente está pensando (opcional, mas útil para debug)
        ```
    *   Explique cada parte: `rascunhador` é um nome identificador para o agente. `role` é o papel (quem ele é). `goal` é o objetivo geral dele. `backstory` dá um contexto. `verbose: true` é uma configuração útil.
4.  **Definir a Tarefa (`config/tasks.yaml`):**
    *   Abra o arquivo `src/meu_primeiro_crewai/config/tasks.yaml`.
    *   Vamos definir uma tarefa para o rascunhador. Digite o seguinte YAML:
        ```yaml
        rascunhar_ideia:
          description: >
            Gere 3 ideias criativas para um post de blog sobre os benefícios de aprender CrewAI.
            Liste as ideias como bullet points curtos.
          expected_output: >
            Uma lista com 3 bullet points, cada um descrevendo uma ideia de post.
          agent: rascunhador # Atribui esta tarefa ao agente 'rascunhador'
          output_file: ideias_blog.md # Salva o resultado em um arquivo (opcional)
          verbose: true # Para ver o que a tarefa está fazendo (opcional)
        ```
    *   Explique cada parte: `rascunhar_ideia` é um nome identificador para a tarefa. `description` é o que deve ser feito. `expected_output` é o que esperamos como resultado. `agent: rascunhador` é crucial, pois atribui esta tarefa ao agente que definimos. `output_file` salva o resultado.
5.  **Instanciar o Crew (`crew.py`):**
    *   Abra o arquivo `src/meu_primeiro_crewai/crew.py`.
    *   Vamos usar a estrutura básica gerada pela CLI (`crewai create crew`), se você a usou na Aula 3, ou vamos criá-la. Para simplicidade e iniciantes, vamos mostrar como importar o agente e a tarefa e criar o Crew.
    *   Apague o conteúdo existente e adicione o seguinte:
        ```python
        import os
        from crewai import Agent, Task, Crew, Process
        from dotenv import load_dotenv

        # Carregar variáveis de ambiente do arquivo .env
        load_dotenv()

        # Certifique-se de que sua chave da OpenAI está definida no arquivo .env
        # OPENAI_API_KEY='your-api-key'
        # Pode ser necessário definir OPENAI_MODEL_NAME='gpt-4o' ou outro modelo compatível
        # Se estiver usando outro LLM, configure a variável de ambiente correspondente ou no código

        # TODO: Na próxima aula, vamos carregar as definições de agentes e tarefas dos arquivos YAML
        # Por enquanto, vamos definir diretamente no código para simplificar

        # 1. Define os Agentes
        # Lembre-se de que o "role", "goal" e "backstory" vêm do nosso agents.yaml (ver passo 3)
        # No CrewAI, geralmente definimos o Agent no código e passamos o "config" do YAML
        # Para este Hands-on inicial, vamos definir diretamente no código para simplificar a demonstração
        rascunhador = Agent(
          role='Escritor de Rascunhos Criativos',
          goal='Criar rascunhos iniciais para diferentes tipos de conteúdo.',
          backstory='Você é um escritor habilidoso que gera rapidamente ideias e estruturas para textos.',
          verbose=True,
          allow_delegation=False, # Agente simples não delega tarefas
          # Ferramentas podem ser adicionadas aqui, se tivéssemos alguma
          # tools=[minha_ferramenta]
        )

        # 2. Define as Tarefas
        # Lembre-se que a "description" e "expected_output" vêm do nosso tasks.yaml (ver passo 4)
        # No CrewAI, geralmente definimos a Task no código e passamos o "config" do YAML
        # Para este Hands-on inicial, vamos definir diretamente no código para simplificar a demonstração
        rascunhar_ideia = Task(
          description='Gere 3 ideias criativas para um post de blog sobre os benefícios de aprender CrewAI. Liste as ideias como bullet points curtos.',
          expected_output='Uma lista com 3 bullet points, cada um descrevendo uma ideia de post.',
          agent=rascunhador, # Atribui a tarefa ao agente rascunhador
          output_file='ideias_blog.md' # Salva o resultado em um arquivo (opcional)
        )

        # 3. Instancia o Crew com um processo sequencial
        # Process.sequential significa que as tarefas serão executadas uma após a outra na ordem em que forem listadas
        meu_crew = Crew(
          agents=[rascunhador], # Lista dos agentes que fazem parte desta tripulação
          tasks=[rascunhar_ideia], # Lista das tarefas a serem executadas
          process=Process.sequential, # Define o tipo de processo (sequencial, hierárquico)
          verbose=True # Mostra o progresso e o raciocínio do crew
        )

        # Agora, para rodar, precisaríamos de uma função main que chame meu_crew.kickoff()
        # Isso estará no main.py na próxima etapa!
        ```
    *   Explique o código: Importamos as classes `Agent`, `Task`, `Crew`. Definimos o agente `rascunhador` com suas propriedades (role, goal, backstory, verbose). Definimos a tarefa `rascunhar_ideia` com descrição, resultado esperado e atribuímos ao agente `rascunhador`. Criamos o `Crew` chamado `meu_crew`, passando a lista de agentes e a lista de tarefas, e definindo o processo como sequencial. Mentionar `load_dotenv()` para carregar a chave de API do `.env` (lembrar os alunos de colocar a chave lá!). *Nota: A CLI do CrewAI gera um código `crew.py` que carrega a config do YAML. Para iniciantes, definir diretamente no código neste momento pode ser mais claro para entender a relação entre Agente, Tarefa e Crew. Mencionar que a abordagem com YAML será coberta em cursos futuros ou módulos mais avançados (embora a CLI a gere no iniciante, mostrá-la diretamente no código neste hands-on reforça o conceito básico).* Manterei a definição direta no código para simplificar este hands-on focado nos conceitos.
6.  **Executar o Crew (`main.py`):**
    *   Abra o arquivo `src/meu_primeiro_crewai/main.py`.
    *   Adicione o seguinte código:
        ```python
        #!/usr/bin/env python
        from meu_primeiro_crewai.crew import meu_crew # Importa o crew que definimos

        def run():
          """
          Executa o crew.
          """
          print("## Iniciando a execução do Crew...")
          # O método kickoff() inicia o processo da tripulação
          # Podemos passar inputs se a descrição da tarefa usar placeholders como {topico}
          # Nossa tarefa não usa inputs por enquanto, mas é bom saber
          resultados = meu_crew.kickoff()

          print("\n## Execução concluída!")
          print("## Resultados:")
          print(resultados)

        if __name__ == "__main__":
          run()
        ```
    *   Explique o código: Importamos o `meu_crew` do nosso arquivo `crew.py`. A função `run()` simplesmente chama `meu_crew.kickoff()`, que é o método que inicia a execução das tarefas pelos agentes. O bloco `if __name__ == "__main__": run()` garante que a função `run` seja chamada quando executamos o script `main.py` diretamente.
7.  **Revisar e Preparar para Execução:**
    *   Verificar se a chave de API da OpenAI (ou outro LLM) está no arquivo `.env`. Se não tiver, o CrewAI não vai conseguir usar um modelo de linguagem e não funcionará. Reforçar a importância de proteger chaves de API.
    *   Verificar se o ambiente virtual está ativado (se usou um).
    *   Salvar todos os arquivos.

**Recapitulando:**
Nesta prática, demos os primeiros passos concretos no CrewAI! Instalamos a biblioteca, definimos nosso primeiro agente com um papel e objetivo, criamos uma tarefa simples para ele e montamos a estrutura básica do nosso `Crew` para executar essa tarefa. Preparamos o projeto para ser executado.

Na próxima aula, vamos *executar* este projeto que montamos e ver o agente em ação, além de explorar as aplicações e benefícios gerais do CrewAI.
