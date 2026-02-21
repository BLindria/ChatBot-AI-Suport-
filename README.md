# Orquestrador de Agentes IA para Suporte ERP

Descrição do Projeto:
Este projeto consiste em uma ecossistema de agentes inteligentes integrados via n8n, projetado para automatizar a triagem e o suporte técnico do ERP WinThor. O sistema atua como uma interface de "autoatendimento" inteligente para analistas de suporte, fornecendo checklists de SLA, apoio em scripts SQL e consultas sobre processos de negócio.

O Problema:
O suporte a sistemas complexos como o WMS WinThor exige que o analista colete uma série de evidências (Checklist de SLA) antes de escalar um problema para o time de produto.

Gargalo: O tempo gasto buscando essas diretrizes em planilhas manuais e documentações extensas.

Solução: Um bot que entrega o diagnóstico exato e os comandos SQL necessários em segundos.

Arquitetura do Sistema:
O projeto utiliza o padrão de Agentes Especialistas Orquestrados:

Agente Master (Router): Atua como o cérebro da operação. Ele recebe a entrada do usuário via Webhook e, através de processamento de linguagem natural, decide qual especialista deve assumir a tarefa.
Especialista SLA: Integrado à API do Google Sheets para extrair checklists específicos de cada rotina do sistema.
Especialista SQL: Focado na geração e validação de scripts para banco de dados Oracle.
Especialista Dúvidas: Utiliza IA Generativa para explicar fluxos e regras de negócio baseadas em conhecimento de domínio.

Técnicas de IA Aplicadas
RAG (Retrieval-Augmented Generation): Implementação de busca de contexto externo via API para mitigar alucinações. O agente não "tenta adivinhar" o SLA; ele recupera o dado exato da planilha antes de gerar a resposta.
Chain-of-Thought (CoT): Prompts estruturados para forçar o agente a "raciocinar" por etapas (Identificar rotina -> Consultar ferramenta -> Formatar checklist).
Multi-Agent Orchestration: Separação de responsabilidades (Separation of Concerns) usando um Agente Roteador para gerenciar o fluxo de tokens e a especialização de tarefas.
Entity Extraction: Processamento de linguagem natural (NLP) para extrair parâmetros específicos (números de rotinas) de frases não estruturadas dos usuários.

Stack Técnica:
Orquestração: n8n
Modelos de IA: Google Gemini (via AI Agent nodes) ou ChatGPT.
Banco de Conhecimento: Google Sheets API
Frontend/Integração: TamperMonkey (Injetado diretamente na interface do usuário)
Lógica: JavaScript (Expressões condicionais e tratamento de strings)

Desafio Técnico & Aprendizados (Onde estou trabalhando)
Desafio Atual: Sincronização de tipagem e extração de entidades.
Detalhes: Atualmente, estou refinando a lógica de filtro entre o Agente Master e a ferramenta de Google Sheets. O desafio reside em garantir que a extração de números de rotinas no texto (entidades) seja enviada de forma sanitizada para o filtro de busca, evitando erros de "não encontrado" causados por divergência de tipos (String vs Number) ou espaços em branco.
