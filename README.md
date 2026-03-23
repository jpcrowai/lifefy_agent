# 🧬 LifeFy - Assistente Pessoal Multi-Domínio

![n8n](https://img.shields.io/badge/n8n-Workflow-orange?style=for-the-badge&logo=n8n)
![Supabase](https://img.shields.io/badge/Supabase-Database-3ECF8E?style=for-the-badge&logo=supabase)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Memory-336791?style=for-the-badge&logo=postgresql)
![OpenAI](https://img.shields.io/badge/OpenAI-GPT4o-412991?style=for-the-badge&logo=openai)

O **LifeFy** é uma arquitetura modular de automação pessoal baseada em Agentes de LLM independentes. Diferente de fluxos rígidos de perguntas e respostas, o Orquestrador compreende a linguagem do usuário no WhatsApp e aciona instantaneamente **"Life-Tools"** que gerenciam a sua vida através de APIs subjacentes.

---

## 🧭 O que ele orquestra?

O Agente Central (`LifeFy_Orchestrator.json`) analisa a intenção orgânica da sua mensagem e elege um destes sistemas dedicados para operar os seus dados no Supabase:

1. 💰 **Finanças (`LifeFy_Financas.json`)**  
Registra gastos de mercado, almoços, receitas e despesas passivas, categorizando inteligentemente o que sai da sua conta.
2. 📆 **Compromissos (`LifeFy_Compromissos.json`)**  
Gerencia a sua agenda baseada num modelo state-driven de data/hora (Ex: "Tenho urologista na quarta às 14h"). O Agente computa a entidade com cronologia estruturada.
3. ✅ **Tarefas e To-Do's (`LifeFy_Tarefas.json`)**  
Sabe aquelas anotações soltas? O Lifefy absorve as tarefas com prioridades elásticas (Low, Medium, High).
4. 🩺 **Saúde (`LifeFy_Saude.json`)**  
Registra água bebida, metas de ingestão de suplementos, sono. Monitoramento diário nativo.
5. 🎯 **Objetivos Financeiros (`LifeFy_ObjetivosFinanceiros.json`)**  
O ecossistema em que você estipula macros de longo prazo (comprar um carro novo, poupar XX Mil Reais).

## ⏰ CRONs e Hacking de Hábitos

Uma inteligência artificial que te espera enviar algo não é um bom assistente. O diferencial do LifeFy são as lógicas assíncronas agendadas (CRON) que puxam as "pontas soltas" dos seus dados e tomam a iniciativa no seu WhatsApp:
- **`CRON_LIFEFY_FINANCAS_RESUMO_DIARIO`**: Executável todo fim do dia, resume fechamento bancário e oferece insights.
- **`CRON_LIFEFY_COMPROMISSOS_LEMBRETES`**: O bot acorda 15min antes dos seus compromissos cruciais, garantindo assiduidade.
- **`CRON_LIFEFY_SAUDE_LEMBRETES_HABITOS`**: Te notifica de hora em hora sobre água, treino ou constância nos suplementos baseando-se nas triggers cadastradas em banco.

## 🛠️ Banco de Dados / Supabase

Sua infra precisará de suporte nas seguintes tabelas (cada uma com chaves obrigatórias `tenant_id` e `user_id`):
- `finances_transactions`
- `life_appointments`
- `tasks`
- `health_habits` e `health_reminders`
- `financial_goals` e `finances_balances`

---

## 🏃 Como iniciar?
1. Faça o pull desta estrutura para a sua máquina.
2. Dentro do seu painel do n8n, crie workflows em branco e dê o `Import from File` nos submódulos JSON e ferramentas menores primeiro (as terminadas em `.json` além do Orquestrador).
3. Após criar e garantir as ID únicas de cada "toolWorkflow", importe o JSON Principal (`LifeFy_Orchestrator.json`).
4. Reconecte o ID de cada fluxo derivado dentro do coração do Orquestrador para amarrar os módulos e adicione suas credenciais do Supremo Banco de Dados, Redis e OpenAI.
5. Tudo pronto para colocar sua vida no piloto automático 🚗💨

---
*Powered by N8N LangChain capabilities & Custom Product Engineering.*
