# CP3-_-Prompt-Chatbot
# 🔌 EV ChargeOps — Integração GoodWe (EV Challenge 2026)

Este repositório contém a implementação de um assistente virtual inteligente baseado na arquitetura **RAG (Retrieval-Augmented Generation)** desenvolvido para o **EV Challenge 2026**. O objetivo principal do sistema é auxiliar operadores e utilizadores na gestão de infraestruturas de recarga de veículos elétricos (VE) corporativos integrados ao ecossistema de inversores e armazenamento de energia (BESS) da **GoodWe**.

---

## 👤 Identificação do Desenvolvedor

* **Nome:** Pedro Soares de Souza
* **RM:** 571285
* **Contexto do Grupo:** EV ChargeOps / ChargeGrid Intelligence

---

## 🚀 Arquitetura do RAG Implementado

O pipeline de inteligência artificial foi construído inteiramente de forma local e focada em privacidade, utilizando a seguinte estrutura:

1. **Base de Conhecimento Vetorial:** Uma base de dados técnica com 12 diretrizes operacionais cruciais (envolvendo protocolos OCPP 1.6J/2.0.1, ISO 15118, telemetria MQTT/HTTPS e estratégias de *Smart Charging* / *Peak Shaving*).
2. **Banco de Dados Vetorial (ChromaDB):** Utilizado para indexar os documentos técnicos e realizar a busca por similaridade semântica (Embedding).
3. **Engenharia de Prompt Adaptativa:** Ajustada estrategicamente para modelos leves (1B), permitindo flexibilidade na interpretação sem perder a restrição ao escopo técnico do projeto.
4. **Modelo de Linguagem Local (LLM):** Executado através do **Ollama** utilizando o modelo **Llama 3.2:1b** (1 bilhão de parâmetros), garantindo respostas eficientes e rápidas em tempo de execução.

---

## 📊 Tabela de Validação e Testes (RAG)

O sistema foi submetido a uma bateria de testes rigorosos para validar a precisão técnica e a sua capacidade de gerir o escopo com sucesso:

| Tipo de Pergunta | Pergunta de Teste | Comportamento Esperado do Bot | Status |
| :--- | :--- | :--- | :--- |
| **Dentro do Escopo** | "Qual é o protocolo de comunicação padrão e a frequência de envio dos dados de telemetria?" | Responde com precisão citando OCPP 1.6J/2.0.1 e envio a cada 10s via HTTPS/MQTT. | ✅ Passou |
| **Dentro do Escopo** | "Como os inversores híbridos da GoodWe atuam junto com o ChargeOps na recarga de EVs?" | Explica o direcionamento do excedente solar (linhas ET/ST) para priorizar a recarga dos VEs. | ✅ Passou |
| **Dentro do Escopo** | "O que o sistema faz caso a estação de recarga perca a conexão com a internet local?" | Explica a arquitetura *Store-and-Forward* (fila de mensagens offline). | ✅ Passou |
| **Fora do Escopo ❌** | "Qual é a receita anual da Tesla com a venda de créditos de carbono nos Estados Unidos?" | Bloqueia a resposta e exibe a mensagem padrão de falta de dados na base. | ✅ Passou |
| **Pegadinha / Contexto** | "O sistema usa inteligência artificial para prever o preço das ações da GoodWe na bolsa?" | Deteta que o assunto é financeiro/fora de escopo e recusa a resposta de forma limpa. | ✅ Passou |

---

## 💻 Estrutura do Repositório

* `/notebook`: Contém o arquivo `.ipynb` com o pipeline completo (Instalação, Banco Vetorial, Testes em lote e a Interface Gráfica).
* `/assets`: Imagens e capturas de tela da interface em funcionamento.

---

## 🖼️ Interface do Usuário (IPyWidgets + HTML)

O chat conta com uma interface moderna estilo aplicação de mensagens com balões coloridos em HTML/CSS nativos rodando diretamente na célula do Jupyter Notebook. O cabeçalho identifica claramente o autor e o RM do projeto.

![Interface do Chat](assets/interface.png) *(Nota: Certifica-te de tirar um print do teu chat a funcionar, guardá-lo na pasta `assets` com o nome `interface.png` para que apareça aqui!)*

---

## 🛠️ Como Executar o Projeto

### Passo a Passo no Google Colab / Jupyter
1. Abre o ficheiro do notebook localizado na pasta `/notebook`.
2. Executa as células sequencialmente de cima para baixo.
3. A **Célula 1** configura automaticamente as dependências de sistema (`zstd`), instala o ambiente do **Ollama** em segundo plano e faz o pull do modelo `llama3.2:1b`.
4. A **Célula 2** popula a base vetorial no **ChromaDB**.
5. A **Célula 4** gera a interface gráfica. Introduz a tua dúvida no campo de texto e prime `Enter` ou clica em `Enviar 📨`. Para limpar o histórico de balões, clica em `Limpar Histórico 🗑️`.
