Ajuda com Estudos - Workflow Inteligente com n8n e IA Generativa

Descrição

O projeto Ajuda com Estudos é um workflow desenvolvido no n8n com o objetivo de auxiliar estudantes na organização de tarefas de estudo.

A automação utiliza uma planilha do Google Sheets como entrada de dados. Quando uma nova linha é adicionada na aba Entradas, o n8n inicia automaticamente o fluxo, processa as informações recebidas, envia os dados para um AI Agent e gera um plano de estudos personalizado com apoio de IA generativa.
O resultado gerado pela IA é salvo automaticamente na aba Resultados da mesma planilha.

Problema abordado

Muitos estudantes têm dificuldade para organizar seus estudos, principalmente quando precisam lidar com diferentes matérias, prazos e níveis de dificuldade. Em muitos casos, o aluno sabe o que precisa estudar, mas não sabe como dividir o conteúdo em etapas, definir uma prioridade ou estimar o tempo necessário para cada parte.
Esse problema pode causar perda de tempo, falta de organização e dificuldade para acompanhar as tarefas acadêmicas.
Solução proposta
A solução proposta foi criar um workflow automatizado no n8n. O usuário adiciona uma tarefa de estudo em uma planilha do Google Sheets, informando:

•	matéria;
•	tema;
•	prazo;
•	dificuldade.

A partir dessas informações, o workflow é iniciado automaticamente pelo Google Sheets Trigger. Em seguida, o nó Edit Fields realiza o processamento dos dados, organizando as informações, removendo espaços desnecessários e criando uma prioridade base de acordo com a dificuldade informada.
Depois disso, os dados processados são enviados para o AI Agent, que utiliza o Google Gemini Chat Model para gerar um plano de estudos com resumo, prioridade final, etapas, tempo estimado e checklist com pontos de atenção.
Por fim, o plano gerado é salvo automaticamente na aba Resultados da planilha.
Tecnologias utilizadas

•	n8n
•	Docker
•	Google Sheets
•	Google Sheets Trigger
•	Edit Fields
•	AI Agent
•	Google Gemini Chat Model
•	Google Gemini(PaLM) API
•	Calculator Tool
•	GitHub

Estrutura do workflow

O workflow é composto pelos seguintes nós:

1. Google Sheets Trigger
Responsável por iniciar o workflow automaticamente quando uma nova linha é adicionada na aba Entradas da planilha.

2. Edit Fields
Responsável pelo processamento dos dados recebidos da planilha. Esse nó remove espaços desnecessários, organiza os campos principais, cria uma prioridade base e monta um campo com os dados processados.

3. AI Agent
Responsável por receber os dados processados e gerar um plano de estudos organizado com apoio de inteligência artificial.

4. Google Gemini Chat Model
Modelo de IA utilizado pelo AI Agent para interpretar os dados recebidos e gerar o plano de estudos.

5. Calculator Tool
Ferramenta auxiliar conectada ao AI Agent para apoiar possíveis estimativas simples.

6. Google Sheets - Append Row
Responsável por salvar o plano de estudos gerado na aba Resultados da planilha.

Fluxo da automação

Google Sheets Trigger
        ↓
Edit Fields
        ↓
AI Agent
   ├── Google Gemini Chat Model
   └── Calculator Tool
        ↓
Google Sheets - Append Row

Funcionamento
1.	O usuário adiciona uma nova linha na aba Entradas do Google Sheets.
2.	O Google Sheets Trigger identifica a nova entrada.
3.	O nó Edit Fields processa e organiza os dados recebidos.
4.	O AI Agent recebe os dados processados.
5.	O Google Gemini Chat Model gera um plano de estudos personalizado.
6.	A Calculator Tool fica disponível como ferramenta auxiliar do agente.
7.	O nó Google Sheets adiciona uma nova linha na aba Resultados com o plano gerado.

Processamento de dados
O processamento de dados é realizado pelo nó Edit Fields.
Nessa etapa, o workflow:

•	remove espaços desnecessários dos campos recebidos;
•	organiza os campos materia, tema, prazo e dificuldade;
•	cria uma prioridade base com base na dificuldade informada;
•	monta o campo dados_processados, que reúne as informações em um formato organizado para o AI Agent.

A prioridade base é definida da seguinte forma:

•	dificuldade Alta gera prioridade base Alta;
•	dificuldade Média gera prioridade base Média;
•	demais valores geram prioridade base Baixa.

Exemplo de entrada

materia	tema	prazo	 dificuldade
Programação	Workflow com n8n e IA	3 dias	Média

Exemplo de saída:
O AI Agent gera um plano de estudos contendo:

Resumo:
Estudar os conceitos básicos de n8n, automação de workflows, triggers, nós e uso de IA generativa.

Prioridade:
Média

Plano de estudos:
1. Entender o que é n8n
2. Estudar triggers e nós
3. Configurar o AI Agent
4. Testar o workflow
5. Revisar o funcionamento da automação

Checklist:
[ ] Entender o conceito de workflow
[ ] Configurar o Google Sheets Trigger
[ ] Processar dados com Edit Fields
[ ] Configurar o AI Agent
[ ] Testar a automação
[ ] Conferir o resultado na planilha

Estrutura do repositório

N8N-DesenvolvFramework3/
│
│
├── Documento/
│   └── Analise do Problema.md
│
├── Imagens/
│   ├── ai-agent.png
│   ├── edit-fields.png
│   ├── gemini-chat-model.png
│   ├── google-sheets-trigger.png
│   ├── planilha-entradas.png
│   ├── planilha-resultados.png
│   └── workflow-completo.png
│
├── workflow/
│   └── Ajuda com Estudos - Workflow.json
|
└── README.md

Como importar o workflow

1.	Abra o n8n.
2.	Crie um novo workflow.
3.	Clique na opção de importar workflow.
4.	Selecione o arquivo JSON localizado na pasta workflow.
5.	Configure as credenciais do Google Sheets.
6.	Configure a credencial do Google Gemini(PaLM) API.
7.	Salve o workflow.
8.	Execute o teste adicionando uma nova linha na aba Entradas da planilha.

Credenciais necessárias

Para executar o projeto, é necessário configurar as seguintes credenciais no n8n:

•	Google Sheets OAuth2, para acessar a planilha;
•	Google Gemini(PaLM) API, para utilizar o modelo de IA generativa.

As chaves de API, tokens e credenciais não estão incluídos no repositório por questões de segurança.

Capturas de tela
As capturas de tela do workflow, da configuração dos nós e das evidências de execução estão disponíveis na pasta Imagens.

Evidências de execução
O workflow foi testado com uma nova tarefa adicionada na aba Entradas da planilha. Após a execução, o AI Agent gerou um plano de estudos e o resultado foi salvo automaticamente na aba Resultados.

Segurança
As credenciais, chaves de API, tokens e senhas foram removidos do arquivo exportado antes da publicação no GitHub. Para executar o workflow, cada usuário deve configurar suas próprias credenciais no n8n.

Conclusão
O projeto Ajuda com Estudos demonstra o uso do n8n para automatizar um processo real do cotidiano, integrando Google Sheets e inteligência artificial generativa.

A solução atende ao objetivo da atividade ao utilizar um gatilho de aplicativo, processamento de dados, AI Agent, modelo de IA, ferramenta auxiliar e saída automatizada em um serviço externo.
