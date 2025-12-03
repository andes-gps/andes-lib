Documentação Andes-Lib

Andes-Lib é uma biblioteca TypeScript projetada para auxiliar no desenvolvimento de aplicações Andes. Ela fornece um framework abrangente para modelagem de projetos, geração de código e criação de documentação. A biblioteca é baseada em três metodologias principais: ANDES (requisitos e análise), SPARK (modelagem de domínio) e MADE (gestão de projetos).

Link de acesso ao repositório no GITHUB: https://github.com/guigneto/andes-lib

Propósito Central do ANDES

A biblioteca transforma definições estruturadas de projetos em múltiplos formatos de saída:

    Arquivos .spark (DSL de modelo de domínio)
    Arquivos .made (DSL de gestão de projetos)
    Documentação Docusaurus (baseada em markdown)

Camadas da Arquitetura
1. Camada de Modelo (src/model/)
        A camada de modelo define as estruturas de dados para as três metodologias: 
Tipos Base (supertypes.d.ts & superclasses.ts)
Interfaces:
    BaseSuperType — Interface base com identifier e description opcional
    NameableSuperType — Estende BaseSuperType com a propriedade name
    DependableSuperType<T> — Adiciona gerenciamento de dependências com array depends
    NameSpaceSuperType — Fornece funcionalidade de referência a namespace

Classes:
    NameSpaceStarter — Elemento raiz do namespace
    NameSpacePertencer — Membro de namespace que referencia um namespace pai

Metodologia ANDES (src/model/andes/)

Focada em engenharia de requisitos e análise de sistemas:
Requisitos (RequirimentsClass.ts):
    RequirimentsBaseClass — Classe base para todos os requisitos
    FunctionalRequirimentType — Requisitos funcionais (FR)
    NonFunctionalRequirimentType — Requisitos não funcionais (NFR)
    BuisinessRuleType — Regras de negócio (BR)
    RequirimentAgregationClass — Agrupa FR, NFR e BR

Análise (AnalisysTypes.d.ts):
    ActorType — Atores do sistema com mapeamento opcional para entidades
    UseCaseClass — Casos de uso com requisitos, executores, eventos e dependências
    EventType — Eventos dentro de casos de uso com ações e executores

Estrutura de Projeto (ProjectTypes.d.ts):
    ProjectOverviewType — Metadados do projeto (nome, propósito, mini-mundo, arquitetura)
    ProjectModuleType — Definição de módulo com requisitos, atores, casos de uso e pacotes
    ProjectType — Projeto completo com visão geral e módulos

Metodologia SPARK (src/model/spark/)
Modelagem de domínio e definição de entidades:

Entidades (EntityTypes.d.ts):
    AttributeType — Atributos de entidade com tipo e restrições (blank, unique, min, max)
    EnumAttributeType — Atributos baseados em enumeração
    RelationType — Relacionamentos entre entidades com cardinalidade
    EntityType — Definição completa de entidade

Enums (EnumTypes.d.ts):
    EnumEntityType — Definições de enumerações com opções

Pacotes (PackageTypes.d.ts):    
    PackageType — Estrutura de pacote contendo entidades, enums e subpacotes

Metodologia MADE (src/model/made/)
    Gestão de projetos e desenvolvimento ágil:

Backlog (BacklogClass.ts):
    TaskClass — Tarefas individuais com dependências e entregáveis
    StoryClass — Histórias de usuário com tarefas, critérios de aceitação e observações
    EpicClass — Épicos contendo histórias e tarefas
    BacklogClass — Backlog completo com épicos, histórias e tarefas

Processo (ProcessClass.ts):
    AcivityClass — Atividades de processo com tarefas e critérios
    ProcessClass — Definição de processo com atividades

Roadmap (RoadmapClass.ts):
    ReleaseClass — Planejamento de releases com versão, datas, status e itens
    MilstoneClass — Marcos contendo múltiplos releases
    RoadmapClass — Roadmap completo com marcos

Equipe (TeamTypes.d.ts):
    TeamMemberType — Membro da equipe com informações de contato
    TeamType — Composição da equipe

Sprint (SprintTypes.d.ts):
    SprintBacklogItemType — Itens de backlog da sprint com responsável e status
    SprintBacklogType — Coleção de itens da sprint
    SprintType — Sprint com datas, status e backlog

2. Camada de Aplicação (src/application/)
    Orquestra a criação dos artefatos:

        Classes Principais:
            ApplicationCreator.ts — Orquestrador principal
                Cria arquivos Spark (modelo de domínio)
                Cria documentação Docusaurus
                Cria arquivos Made (gestão de projetos)
                Organiza a saída na pasta artifacts/

            DocusaurusCreator.ts — Gerador de documentação
                Cria documentação baseada em Docusaurus
                Processa módulos do projeto em markdown

            IO.ts — Utilitários de sistema de arquivos
                createFolderAndFile() — Cria diretórios e escreve arquivos

3. Camada de Renderização (src/renders/)
    Transforma modelos em formatos de saída:

        Renders de DSL (src/renders/dsl/)
        Renders Spark:
            SparkFileRender.ts — Geração completa do arquivo Spark
            SparkPackageRender.ts — Renderização de pacotes
            SparkEntytiRender.ts — Renderização de entidades
            SparkEnumEntityRender.ts — Renderização de enums
            SparkConfigRender.ts — Renderização de configurações

        Renders Made:
            MadeFileRender.ts — Geração completa do arquivo Made
            MadeBacklogRender.ts — Renderização de backlog
            MadeProcessRender.ts — Renderização de processos
            MadeRoadmapRender.ts — Renderização de roadmap
            MadeTaskRender.ts — Renderização de tarefas
            MadeTeamRender.ts — Renderização de equipe
            MadeProjectRender.ts — Renderização de projeto
            MadeModuleConfigRender.ts — Configuração de módulos

        Renders Base:
            NameSpaceRender.ts — Renderização de namespaces
            NameSpaceItemRender.ts — Renderização de itens de namespace


        Renders Markdown (src/renders/markdown/)
        Markdown Principal:
            MarkdownRender.ts — Renderização base
            FileRender.ts — Markdown de arquivos
            PageHandler.ts — Gerenciamento de páginas
            SectionRender.ts — Renderização de seções
            ParagraphRender.ts — Renderização de parágrafos
            TableRender.ts — Renderização de tabelas

        Diagramas Mermaid:
            MermaidRender.ts — Renderizador base para Mermaid
            Suporte a fluxogramas
            Suporte a máquinas de estados

        Diagramas PlantUML:
            PlantUmlRender.ts — Renderizador base para PlantUML
            Suporte a diagramas de classes

        Interface:
            IRender.d.ts — Contrato de renderização com método render(identationStartLevel)

4. Camada de Grafo (src/graph/)
    Análise e visualização de dependências:

        Classe Graph (graph.ts):
            Estrutura de grafo baseada em lista de adjacência
            Detecção de ciclos usando DFS
            Ordenação topológica com algoritmo de Kahn
            Geração de diagramas Mermaid
            Geração de tabelas Markdown
            Rastreamento de relacionamentos entre atores

        Métodos Principais:
            addVertex() — Adiciona nós com descrição e atores
            addEdge() — Adiciona dependências
            containsCycle() — Detecta dependências circulares
            topologicalSort() — Ordena nós por dependências
            generateMermaidDiagram() — Gera grafo visual
            generateMarkdownTable() — Gera tabela de dependências
            createAnalysis() — Análise completa com ciclos e visualização

5. Camada de Utilitários (src/util/)
    Funções auxiliares:

        dateUtils.ts:
            dateToIsoString() — Converte Date para ISO (YYYY-MM-DD)
            getTodayInIsoDate() — Retorna a data atual em formato ISO

        expandToString.ts:
            expandToString() — Processador de template strings com indentação inteligente
            expandWithNewLines() — Template com quebra de linha final
            Trata valores null/undefined
            Alinhamento automático de indentação
            Limpeza e formatação de linhas

        generator-utils.ts:
            capitalizeString() — Capitaliza primeira letra
            createPath() — Cria diretórios se não existirem
            ident_size — Constante de indentação (4 espaços)
            base_ident — String base de indentação

        Identation.ts:
            Gerenciamento de indentação para saída renderizada

6. Camada de Documentação (src/documentation/)
    Serviços de geração de documentação:

        application.ts — Documentação da aplicação
        Pasta docsaurus/:
            DocksaurusService.ts — Serviço Docusaurus
            ClassDiagram.ts — Geração de diagramas de classe
            ModelUseCases.ts — Documentação de modelos de caso de uso

    Formatos de Arquivo
        Arquivos de Entrada
            .andes — Arquivos de definição do projeto Andes
            .made — Arquivos de gestão de projetos MADE

        Arquivos de Saída
            .spark — DSL de modelo de domínio
            .made — DSL de gestão de projetos
            Arquivos Markdown — Documentação Docusaurus

    Configuração de Build e Testes
        Ferramentas de Build:
            TypeScript 5.8.3
            tsup — Empacotador rápido de TypeScript
            Sistema de módulos ESNext

        Testes:
            Vitest para testes unitários
            Jest para relatórios de cobertura
            Comandos de teste: npm test, npm run test:watch, npm run test:coverage

        Scripts:
            npm run build — Compila a distribuição
            npm run dev — Modo de desenvolvimento com watch
            npm run testBuild — Verifica a compilação TypeScript

        Padrões de Projeto
            Namespace Pattern — Organização hierárquica com NameSpaceStarter e NameSpacePertencer
            Render Pattern — Interface consistente via IRender
            Builder Pattern — Construção incremental de objetos complexos
            Strategy Pattern — Estratégias de renderização diferentes para DSL e Markdown
            Graph Pattern — Análise de dependências e ordenação topológica

        Dependências
        Runtime:
            commitizen — Commits convencionais
            @vitest/coverage-v8 — Cobertura de testes

        Desenvolvimento:
            Ferramentas TypeScript
            Frameworks Jest & Vitest
            ts-node para desenvolvimento

        Fluxo de Uso
            Entrada: Analisar arquivo .andes
            Modelagem: Criar modelo interno usando classes ANDES, SPARK e MADE
            Processamento: Analisar dependências usando utilitários de grafo
            Renderização: Transformar modelos em DSL e Markdown
            Saída: Gerar arquivos .spark, .made e documentação

        Estrutura de Exportação
            A biblioteca exporta todas as principais classes e tipos via src/index.ts:
            Criadores de aplicação
            Utilitários de grafo
            Todos os tipos e classes de modelo
            Superclasses e supertypes

        Integração
            A Andes-Lib foi projetada para ser utilizada pelo pacote npm andes-tools-leds, que fornece a interface de linha de comando da metodologia Andes.