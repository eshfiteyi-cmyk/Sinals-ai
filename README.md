# Sinals-ai

Projeto: Chatbot Sinals-ai (interface Next.js + proxy de inferência para Gemini)

Descrição

Este repositório contém a interface e um endpoint servidor-side para conectar com o modelo Gemini (Gemini 1.5 Pro) via API do Google. A implementação adicionada aqui inclui arquivos base do projeto (package.json, TypeScript config, .gitignore) e um endpoint SSE (`/api/chat`) que faz proxy das requisições para a API do Gemini e retransmite a resposta em streaming para o cliente (Server-Sent Events).

Aviso: O código de proxy espera uma chave de API definida na variável de ambiente `GEMINI_API_KEY`. Para uso em produção, proteja adequadamente a chave e reveja políticas de segurança.

Começando

1. Clone o repositório

   git clone https://github.com/eshfiteyi-cmyk/Sinals-ai.git
   cd Sinals-ai

2. Instale dependências

   npm install

3. Variáveis de ambiente

Crie um arquivo `.env.local` (ou configure em seu host) com a variável:

```
GEMINI_API_KEY=YOUR_GOOGLE_GEMINI_API_KEY
# Opcional: configure a URL da API do Gemini (se diferente)
# GEMINI_API_URL=https://generativemodels.googleapis.com/v1/models
```

4. Rodando em desenvolvimento

   npm run dev

5. Chamando o endpoint de chat

O endpoint POST `/api/chat` aceita JSON com o formato:

```json
{
  "messages": [
    {"role": "user", "content": "Olá"}
  ],
  "model": "gemini-1.5-pro"
}
```

A resposta é enviada em streaming via SSE. O cliente deve conectar e tratar eventos do tipo `message`.

Arquitetura básica adicionada

- pages/api/chat.ts — API route (Next.js) que expõe `/api/chat` e retransmite streaming SSE
- lib/gemini.ts — wrapper mínimo que encaminha requisições para a API do provedor (Gemini). Ajuste a URL se necessário.
- package.json, tsconfig.json, .gitignore — configuração base do projeto

Próximos passos sugeridos

- Implementar UI (chat) que consome `/api/chat` via EventSource/Fetch streaming
- Adicionar gestão de contexto (janela deslizante) e persistência de conversas
- Adicionar mecanismos de retry, logs e métricas
