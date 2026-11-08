# Parte 2 - Questão 2 - Tradução com OpenAI

Traduz do inglês para o francês com `gpt-4.1-mini` via LangChain.

## Como executar

Use Python 3.12. Se já descompactou o projeto, entre na pasta e pule a etapa de clonagem.

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

No macOS ou Linux, rode os comandos abaixo.

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

No macOS ou Linux, rode os comandos abaixo.

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

O campo `text` aceita até 4.000 caracteres. O cliente faz uma chamada por requisição e usa um timeout de 15 segundos. A API retorna HTTP 503 se faltar a chave, 429 para limite de uso, 504 para timeout e 502 se o provedor falhar ou devolver uma tradução vazia.

O FastAPI retorna HTTP 422 se faltar o campo, se ele estiver vazio ou se exceder o limite.

[Documentação do modelo ou componente](<https://developers.openai.com/api/docs/models/gpt-4.1-mini>)
