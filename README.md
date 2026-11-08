# Parte 2 · Questão 2 — Tradução com OpenAI

API FastAPI que traduz do inglês para o francês com `gpt-4.1-mini`, usando `ChatOpenAI` do LangChain. A cadeia formata o prompt, faz uma chamada assíncrona e extrai o texto da resposta.

## Como executar

Use Python 3.12. Clone este repositório e entre na pasta.

```bash
git clone https://github.com/yurimorillaprevidas/tp-langchain-q2-openai-fr.git
cd tp-langchain-q2-openai-fr
```

Crie e ative um ambiente virtual.

No Windows, use o PowerShell.

```powershell
py -3.12 -m venv .venv
.\.venv\Scripts\Activate.ps1
```

No macOS ou Linux, use o terminal.

```bash
python3.12 -m venv .venv
source .venv/bin/activate
```

Instale as dependências.

```bash
python -m pip install -r requirements.txt
```

### Chave da OpenAI

Configure uma chave da API com acesso a `gpt-4.1-mini` no mesmo terminal em que o servidor será executado.

Use este comando no PowerShell.

```powershell
$env:OPENAI_API_KEY = "SUA_CHAVE"
```

No macOS ou Linux, use o terminal.

```bash
export OPENAI_API_KEY="SUA_CHAVE"
```

Guarde a chave fora do código e do GitHub.

Inicie o servidor.

```bash
python -m uvicorn main:app
```

O servidor fica em `http://127.0.0.1:8000`.

## Como testar

Abra [a documentação interativa](http://127.0.0.1:8000/docs), selecione **POST /translate**, clique em **Try it out**, cole o JSON e clique em **Execute**.

```json
{
  "text": "The cat is sleeping."
}
```

Exemplo de resposta HTTP 200.

```json
{
  "translation": "Le chat dort."
}
```

O endpoint aceita de 1 a 2.000 caracteres, respeita a janela de contexto do GPT-2 e acrescenta até 48 tokens. A resposta inclui a frase de entrada e sua continuação. Como a geração usa amostragem, o resultado pode variar.,Envie de 1 a 20.000 caracteres em `text`. A aplicação divide parágrafos longos em trechos de até 250 tokens de entrada e reúne as traduções na ordem original. Para testar dois parágrafos, use `{"text":"The cat is sleeping.\n\nThe moon is shining."}`. O JSON de saída mantém a separação entre parágrafos.,As perguntas previstas são `Olá!`, `Qual é o seu nome?` e `Qual é a capital do Brasil?`. Para outras entradas, o chatbot retorna `Ainda não tenho uma resposta para essa pergunta.`. A comparação ignora maiúsculas e pontuação final.,O endpoint aceita de 1 a 4.000 caracteres. Reutiliza a cadeia, configura um timeout de 15 segundos no cliente e faz uma chamada por requisição, sem tentativas automáticas. O HTTP 503 indica ausência da chave, o 429 indica limite de uso, o 504 indica timeout e o 502 indica falha do provedor ou tradução vazia. Uma chamada real consome a cota da sua conta da API.,Envie de 1 a 20.000 caracteres em `text`. A aplicação divide parágrafos longos em trechos de até 250 tokens, envia cada conjunto ao `HuggingFacePipeline` com `.batch()` e reúne as traduções na ordem original.

Uma entrada ausente, vazia ou acima do limite retorna HTTP 422.

[Documentação do modelo ou componente](<https://developers.openai.com/api/docs/models/gpt-4.1-mini>)
