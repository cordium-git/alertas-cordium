# alertas-cordium

Vigia externo do `cordiumhub.com.br`. Confere o site a cada 5 minutos **de fora da máquina que o
hospeda** — que é todo o ponto: em 2026-09-09 o site ficou quatro horas fora e o monitoramento caiu
junto com ele, porque morava no mesmo host.

Este repositório é público de propósito. A franquia de GitHub Actions é ilimitada em repositório
público e de 2.000 minutos/mês em privado; uma checagem a cada 5 minutos consome cerca de 8.600
minutos por mês. Aqui não há código nem configuração de ninguém: só o workflow, e a URL conferida já
é pública.

## Como ele avisa

Só na **mudança de estado**:

| situação | o que acontece |
|---|---|
| três checagens seguidas falham, sem incidente aberto | abre uma issue, manda o alerta no Discord e **falha o job** (o app do GitHub avisa no celular) |
| o site volta a responder 200 e há incidente aberto | fecha a issue e manda o aviso de volta |
| nada mudou | não faz nada |

Uma queda de quatro horas gera duas mensagens, não quarenta e oito. A issue aberta é, ao mesmo
tempo, o estado do vigia e o registro do incidente.

## Configuração

Um segredo, em **Settings → Secrets and variables → Actions**:

- `DISCORD_WEBHOOK` — a URL do webhook do canal de alertas.

Sem ele o vigia continua funcionando: abre e fecha a issue e falha o job; o que não sai é a mensagem
no Discord.

## Para testar agora

Em **Actions → vigia externo do cordiumhub → Run workflow**. Com o site no ar, a saída esperada é
`sem mudança de estado`.

---

Parte da etapa `E14` da esteira da frota de scraping (`AC-E14-03`).
