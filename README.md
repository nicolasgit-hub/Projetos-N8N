# Projetos-N8N
Projetos-N8N


### 🍔 1. Autobot.IA - Agente de Delivery Autônomo
**Arquivos:** `Agente_Delivery.json`, `atualizaEndereco.json`, `link_de_pagamento.json`, `Agente_Cardapio.json`

**Visão Geral:**
Um assistente virtual autônomo construído para realizar o atendimento ponta a ponta de uma hamburgueria via WhatsApp. O agente é capaz de transcrever áudios, consultar regras de negócio dinâmicas, calcular valores e registrar o pedido final sem intervenção humana.

**Arquitetura e Fluxos de Execução:**
* **Ingestão Omnichannel:** Recebimento de mensagens de texto, imagens e áudios via webhook através da Evolution API. Áudios são convertidos e transcritos utilizando a API da OpenAI.
* **Gerenciamento de Estado:** Utilização de Redis para agrupar mensagens fragmentadas do usuário (debounce), evitando execuções duplicadas e reduzindo o custo de tokens.
* **RAG (Retrieval-Augmented Generation):** Integração com o Google Drive para leitura de documentos PDF, gerando embeddings na OpenAI e armazenando no Supabase (Vector Store) para que o agente consulte cardápios e informações operacionais em tempo real.
* **Orquestração de Ferramentas (LangChain):** O agente GPT-4.1 possui acesso a um toolkit customizado para:
  * Consultar e enviar o cardápio em PDF.
  * Atualizar o endereço do cliente no banco de dados relacional.
  * Gerar links de pagamento integrados via API do Asaas.
  * Buscar pedidos ativos e atualizar status.
  * Registrar o pedido final no Supabase.

**🛠️ Stack Técnica:** n8n, LangChain, OpenAI (GPT-4.1 & Whisper), Supabase (PostgreSQL & pgvector), Redis, Evolution API, Asaas API.



### 🦷 2. Autobot.IA - Gestão e Agendamento de Clínicas
**Arquivos:** `AGENDAMENTO_CLINICA.json`, `TOOLS_AGENDA.json`, `ENVIA_EMAIL.json`, `FOLLOW_UP.json`

**Visão Geral:**
Sistema avançado de atendimento e agendamento odontológico que cruza a disponibilidade de diversos profissionais em tempo real, gerencia o calendário de consultas e executa rotinas de engajamento com o paciente.

**Arquitetura e Fluxos de Execução:**
* **Agendamento Dinâmico:** O agente de IA interpreta a intenção do paciente e utiliza ferramentas conectadas à API do Google Calendar para ler (listar slots disponíveis), criar, atualizar ou deletar eventos, sempre checando conflitos de horário.
* **Memória de Longo Prazo:** Implementação de uma ferramenta analítica que condensa as informações do paciente (histórico de dores, preferências de horário, objeções) em um resumo atualizado no banco de dados, garantindo contexto para contatos futuros.
* **Comunicação Multicanal:** Além de responder no WhatsApp (Evolution API) enviando e recebendo áudios processados via ElevenLabs e OpenAI, o fluxo dispara automaticamente e-mails de confirmação contendo data, hora e local da consulta.
* **Follow-up e Lembretes Ativos:** Um cron job roda rotinas em background para reengajar clientes que abandonaram a conversa no meio do funil de atendimento e envia lembretes automáticos um dia antes da consulta agendada.

**🛠️ Stack Técnica:** n8n, LangChain, Google Calendar API, Supabase, Redis, Gmail API, Evolution API, ElevenLabs (Text-to-Speech).
