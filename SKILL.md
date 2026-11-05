---
name: lovable
description: Abre e opera o Open Lovable do estúdio (cópia própria do Lovable que roda no PC, pasta Desktop/open-lovable). Use quando a Simone disser "/lovable", "abre o lovable", "o lovable que nós fizemos", "fazer um app/site no lovable", ou pedir para criar uma página/app a partir de um site de referência no Open Lovable.
---

# Open Lovable — o "Lovable nosso"

Fica em `C:\Users\Simone\Desktop\open-lovable` (Next.js, `npm run dev`, porta **3000**).
Atalho dela: `Desktop\Open Lovable.lnk` → `ABRIR-OPEN-LOVABLE.cmd`.
Manual das chaves (para ela): `Desktop\open-lovable\MANUAL-DAS-CHAVES.html`.

## 1. Conferir as chaves ANTES de abrir

Mostrar só os NOMES preenchidos, nunca o valor:

```bash
cd /c/Users/Simone/Desktop/open-lovable && grep -E '^[A-Z_]+=.+' .env.local | sed 's/=.*/=(preenchida)/'
```

São 3 chaves necessárias:
- `FIRECRAWL_API_KEY` (lê o site de referência)
- uma IA: `GEMINI_API_KEY` ou `ANTHROPIC_API_KEY` / `OPENAI_API_KEY` / `GROQ_API_KEY` / `AI_GATEWAY_API_KEY`
- a caixa onde o app roda: `SANDBOX_PROVIDER=e2b` precisa de `E2B_API_KEY` (ou `vercel` precisa de `VERCEL_OIDC_TOKEN`/`VERCEL_TOKEN`)

Se faltar alguma, diga QUAL falta e abra o manual (`start "" MANUAL-DAS-CHAVES.html`).
A chave quem cola no `.env.local` é ELA, com o Bloco de Notas. A chave nunca passa pelo chat.
Depois de mexer no `.env.local`, é preciso reiniciar o Open Lovable.

## 2. Abrir

```powershell
$p = Get-NetTCPConnection -LocalPort 3000 -State Listen -ErrorAction SilentlyContinue
if ($p) { Start-Process "http://localhost:3000" } else { Start-Process "$env:USERPROFILE\Desktop\Open Lovable.lnk" }
```

Se a porta 3000 estiver ocupada por OUTRA coisa (o Vetto também usa a 3000 no `npm run dev`), avise antes de fechar qualquer coisa.
Lembre a ela: a janela preta "Open Lovable" precisa ficar aberta enquanto usa.

## 3. Usar

1. Na tela inicial, colar o link do site de referência OU descrever o app.
2. Escolher o modelo de IA no seletor (o que tiver chave).
3. Ele gera o código e mostra a prévia ao lado. Os pedidos de ajuste vão no chat da direita.
4. Para levar o resultado embora, use o botão de baixar (zip). Depois o código entra no fluxo normal do estúdio (GitHub → Netlify com `--site`).

## Regras do estúdio que valem aqui

- **Custo:** cada geração gasta créditos de IA, do Firecrawl e do E2B. Não fique gerando em loop. Antes de fazer muitas gerações, pergunte o teto de gasto a ela ([[feedback_sem_retorno_nao_gasta]]).
- **Referência ≠ clone:** pode usar a estrutura e o ritmo. Nunca copie marca, textos ou fotos de terceiros. O que sai daqui precisa ser autoral.
- Antes de mostrar a ela ou a um cliente, o que sai do Open Lovable passa pela `revisao-premium`. Antes de publicar, pela auditoria de 12 pontos.
- Erros: leia a janela preta (o terminal do `npm run dev`) antes de chutar. Se for "API key", é chave faltando. Se for "sandbox", é E2B/Vercel.
