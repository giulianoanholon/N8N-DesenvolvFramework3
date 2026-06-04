Análise do Problema

1. Descrição do problema
O problema identificado é a dificuldade que muitos estudantes têm para organizar suas tarefas de estudo. Em muitas situações, o aluno recebe uma atividade, prova ou conteúdo para estudar, mas não sabe como dividir esse estudo em etapas menores, definir uma prioridade ou estimar o tempo necessário para concluir cada parte.
Esse problema impacta principalmente estudantes que precisam lidar com várias matérias ao mesmo tempo, cada uma com prazos, temas e níveis de dificuldade diferentes. A falta de organização pode fazer com que o estudante perca tempo, deixe conteúdos importantes para depois ou estude de forma pouco eficiente.
Atualmente, essa organização costuma ser feita manualmente, por meio de anotações, listas simples, agendas ou planilhas. Apesar de funcionar em alguns casos, esse processo pode ser demorado e nem sempre gera um planejamento claro.

2. Proposta de solução
A solução proposta é o projeto Ajuda com Estudos, um workflow desenvolvido no n8n com integração ao Google Sheets e uso de Inteligência Artificial Generativa.
O workflow permite que o usuário cadastre uma tarefa de estudo em uma planilha, informando a matéria, o tema, o prazo e o nível de dificuldade. Quando uma nova linha é adicionada na aba Entradas, o n8n identifica automaticamente essa ação e inicia o fluxo.
Depois disso, os dados passam por uma etapa de processamento, são enviados para um AI Agent e a inteligência artificial gera um plano de estudos personalizado. O resultado final é salvo automaticamente na aba Resultados da mesma planilha.

3. Papel da inteligência artificial
A inteligência artificial participa ativamente da solução por meio do nó AI Agent. O agente recebe os dados já processados e transforma essas informações em um plano de estudos organizado.
O AI Agent é responsável por:

•	analisar a matéria informada;
•	interpretar o tema de estudo;
•	considerar o prazo disponível;
•	avaliar a dificuldade informada;
•	utilizar a prioridade base criada no processamento;
•	gerar um resumo do que estudar;
•	criar um plano dividido em etapas;
•	sugerir tempo estimado para cada etapa;
•	montar um checklist final com pontos de atenção.

Dessa forma, a IA não é usada apenas como complemento, mas como parte central da automação, pois ela gera a principal saída do workflow.

4. Fluxo da automação

O workflow segue a seguinte estrutura:

Google Sheets Trigger
↓
Edit Fields
↓
AI Agent
├── Google Gemini Chat Model
└── Calculator
↓
Append row in sheet

5. Etapas do workflow

5.1 Entrada de dados
A entrada de dados ocorre por meio da aba Entradas do Google Sheets. O usuário adiciona uma nova linha contendo as informações da tarefa de estudo.
Os campos utilizados são:

Campo	Descrição
materia Nome da matéria ou disciplina
tema	Tema que será estudado
prazo	Prazo disponível para estudar
dificuldade	Nível de dificuldade da tarefa

Exemplo de entrada:

materia	tema	prazo	dificuldade
Programação	Workflow com n8n e IA	3 dias	Média

5.2 Gatilho da automação
O nó Google Sheets Trigger é responsável por iniciar o workflow automaticamente quando uma nova linha é adicionada na aba Entradas da planilha.
Esse nó atende ao requisito de gatilho do projeto, pois o fluxo começa a partir de um evento em um aplicativo externo.

5.3 Processamento dos dados
O nó Edit Fields é utilizado como etapa de processamento de dados.
Nessa etapa, o workflow organiza as informações recebidas da planilha antes de enviá-las para o AI Agent. O processamento realizado inclui:

•	remoção de espaços desnecessários nos campos;
•	organização dos dados principais;
•	criação de uma prioridade base com base na dificuldade informada;
•	montagem de um campo chamado dados_processados, contendo os dados formatados.

A prioridade base é definida automaticamente de acordo com a dificuldade:

•	se a dificuldade for alta, a prioridade base será Alta;
•	se a dificuldade for média, a prioridade base será Média;
•	nos demais casos, a prioridade base será Baixa.

Esse processamento ajuda a preparar melhor as informações antes da etapa de inteligência artificial.

5.4 Processamento com IA
Após o tratamento dos dados, as informações são enviadas para o nó AI Agent.
O AI Agent utiliza o Google Gemini Chat Model para interpretar os dados recebidos e gerar um plano de estudos personalizado.
A resposta gerada contém:

1.	resumo do que estudar;
2.	prioridade final da tarefa;
3.	plano dividido em etapas;
4.	tempo estimado para cada etapa;
5.	checklist final com pontos de atenção.

5.5 Ferramenta auxiliar
O nó Calculator é conectado ao AI Agent como ferramenta auxiliar. Ele pode apoiar o agente em estimativas simples, como organização de tempo ou divisão de etapas.

5.6 Saída automatizada
O nó Append row in sheet é responsável por salvar a resposta gerada pela IA na aba Resultados do Google Sheets.
A saída contém os dados originais da tarefa e o plano de estudos gerado pelo AI Agent.

6. Função de cada nó utilizado
Google Sheets Trigger
Inicia automaticamente o workflow quando uma nova linha é adicionada na aba Entradas da planilha.

Edit Fields
Processa os dados recebidos da planilha. Esse nó remove espaços extras, organiza os campos principais, cria uma prioridade base e monta um texto estruturado com os dados processados.

AI Agent
Recebe os dados processados e gera um plano de estudos personalizado com apoio de inteligência artificial generativa.

Google Gemini Chat Model
Modelo de IA utilizado pelo AI Agent para gerar a resposta textual.

Calculator
Ferramenta auxiliar conectada ao AI Agent para apoiar possíveis estimativas simples.

Append row in sheet
Salva automaticamente o resultado gerado pela IA na aba Resultados do Google Sheets.

7. Tecnologias utilizadas
As tecnologias utilizadas no projeto foram:

•	n8n;
•	Docker;
•	Google Sheets;
•	Google Sheets Trigger;
•	Edit Fields;
•	AI Agent;
•	Google Gemini Chat Model;
•	Google Gemini(PaLM) API;
•	Calculator Tool;
•	GitHub.

8. Entrada e saída esperadas
Entrada esperada
A entrada esperada é uma nova linha na aba Entradas da planilha, contendo matéria, tema, prazo e dificuldade.
Exemplo:

materia	tema	prazo	dificuldade
Banco de Dados	Modelo Entidade-Relacionamento	2 dias	Alta

Saída esperada

A saída esperada é uma nova linha na aba Resultados, contendo os dados da tarefa e o plano de estudos gerado pela IA.

O plano gerado deve apresentar:

•	resumo do conteúdo;
•	prioridade final;
•	etapas de estudo;
•	tempo estimado;
•	checklist com pontos de atenção.

9. Benefícios da solução
A solução ajuda o estudante a organizar melhor seus estudos, pois transforma uma tarefa simples em um plano mais claro e prático. Com isso, o aluno pode entender melhor o que precisa estudar, quais etapas seguir e quais pontos merecem mais atenção.
Além disso, o uso do n8n permite automatizar o processo, evitando que o estudante precise montar manualmente um plano de estudo toda vez que tiver uma nova tarefa.

10. Conclusão
O projeto Ajuda com Estudos demonstra como o n8n pode ser utilizado para automatizar uma situação real do cotidiano com apoio de inteligência artificial generativa.

O workflow desenvolvido possui entrada de dados, gatilho automático, processamento de dados, uso de AI Agent, integração com Google Sheets e saída automatizada. Dessa forma, a solução atende aos requisitos da atividade e apresenta uma aplicação prática de automação e IA para auxiliar na organização de estudos.
