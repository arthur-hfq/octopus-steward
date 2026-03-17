# 🐙 octopus-steward
> **Financial Governance & Decision Engine**

O **Octopus Steward** é um motor de governança financeira e estratégica que integra o Telegram ao ecossistema Google (Sheets e Drive). O sistema atua como um middleware inteligente que normaliza entradas informais em dados estruturados para análise avançada no Looker Studio.

## 🏗️ Arquitetura do Sistema
O sistema opera como uma **Data-Driven Application**, onde as regras de negócio e a interface do usuário (botões do bot) são definidas dinamicamente via Google Sheets, permitindo manutenção sem alteração de código.

* **Interface:** Telegram Bot API (Async).
* **Core Engine:** Python 3.10+.
* **Persistence Layer:** Google Sheets API (Database relacional).
* **File Storage:** Google Drive API (Blob storage para comprovantes).

## 📊 Modelagem de Dados
A estrutura é composta por 5 entidades principais que garantem a integridade dos dados:

1.  **`opts`**: Schema de configuração. Armazena IDs de usuários autorizados, tokens e flags de ambiente (Debug/Prod).
2.  **`budgets`**: Camada de Estratégia. Define os limites percentuais de gastos baseados no holerite e regras de cálculo de saldo.
3.  **`categories`**: Camada de UX e Normalização. Mapeia subcategorias, ícones e vincula cada item a uma "Categoria Pai" (FK) na aba de budgets.
4.  **`accounts`**: Controle de Custódia. Gerencia o saldo entre diferentes contas (Corrente, Investimentos, Espécie).
5.  **`releases`**: O **Ledger** (Livro-razão). Histórico imutável de transações com geração de **UUID** para rastreabilidade.

## 🔒 Segurança e Integridade
* **Acesso Restrito:** Validação de `USER_ID` via middleware para impedir interações não autorizadas.
* **Environment Variables:** Gestão de chaves sensíveis via arquivos `.env` protegidos pelo `.gitignore`.
* **Idempotência:** Lógica de processamento que evita duplicidade em lançamentos de transferências entre contas.

## 🔧 Setup Técnico

### Pré-requisitos
* Python 3.10+
* Google Cloud Console Project com APIs de **Sheets** e **Drive** ativadas.
* Arquivo `credentials.json` da Service Account na raiz do projeto.

### Instalação
1.  **Clonar repositório:**
    ```bash
    git clone [https://github.com/arthur-hfq/octopus-steward.git](https://github.com/arthur-hfq/octopus-steward.git)
    cd octopus-steward
    ```

2.  **Ambiente Virtual:**
    ```bash
    python -m venv .venv
    # Ativar (Windows): .venv\Scripts\activate | (Linux/Mac): source .venv/bin/activate
    ```

3.  **Dependências:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Configuração de Variáveis:**
    Crie um arquivo `.env` na raiz seguindo o modelo do `.env.example`.

## 🛠️ Tecnologias Principais
* `python-telegram-bot`: Comunicação em tempo real.
* `gspread`: Manipulação de tabelas via API.
* `pandas`: Processamento de dados e cálculos de saldo.
* `python-dotenv`: Segurança de variáveis de ambiente.

---
Desenvolvido por [Arthur-hfq](https://github.com/arthur-hfq)
