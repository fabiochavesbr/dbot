# dbot

Bot de Discord em Python. Responde a comandos por mensagem; `$question` consulta a OpenAI e responde "como um pirata".

## Estrutura
- `mybot.py` — bot principal: `$hello` e `$question <texto>` (chama a OpenAI, modelo `gpt-4o`)
- `discord_only.py` — bot mínimo, só `$hello`, sem OpenAI
- `requirements.txt` — dependências: `discord.py`, `python-dotenv`, `openai`
- `.env` — segredos locais (`TOKEN`, `OPENAI_KEY`); nunca versionar

## Comandos
- Instalar: `pip install -r requirements.txt`
- Rodar bot completo: `python mybot.py`
- Rodar bot mínimo: `python discord_only.py`
- Não há testes automatizados nem linter configurados; validar com `python -m py_compile mybot.py discord_only.py`

## Segurança (obrigatório)
- Nunca commitar `.env`, tokens do Discord ou chaves da OpenAI; nunca exibi-los em saída, logs ou mensagens
- Segredos são lidos só via `os.getenv` após `load_dotenv()`; não colocar valores no código
- Antes de qualquer commit, conferir `git status` e garantir que `.env` não está staged
- Se um segredo vazar, avisar imediatamente: o token deve ser regenerado no Discord Developer Portal

## Convenções de código
- Python 3, `discord.Client` com `intents.message_content = True`
- Comandos são prefixos `$` tratados em `on_message`; ignorar mensagens do próprio bot
- Manter o estilo atual (funções simples, sem frameworks extras); `discord.ext.commands` só se for pedido
- Chamadas à OpenAI são síncronas hoje; se mudar, usar o cliente assíncrono (`AsyncOpenAI`) para não bloquear o loop do Discord
- Respostas do Discord têm limite de 2000 caracteres; tratar ao alterar respostas longas

## Git
- Mensagens de commit curtas e descritivas, em português
- Branch principal: `main`
