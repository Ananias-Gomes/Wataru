# 渡 (Wataru) — Central Pessoal

Painel pessoal single-page para acompanhar rotina, hábitos, estudos para o exame **MEXT**, carreira em engenharia de software e hobbies — com um sistema de progressão de personagem e integração opcional com Telegram para lembretes.

Não depende de nenhum servidor: é HTML + CSS + JS puro, e os dados ficam salvos no armazenamento do próprio app (nada é enviado para fora, exceto quando você mesmo aciona o envio de mensagem para o Telegram).

## Estrutura do projeto

```
.
├── index.html      # o app inteiro (interface + lógica)
├── manifest.json   # metadados do PWA (nome, ícone, cores)
├── sw.js           # service worker — permite abrir offline depois de instalado
└── icon.svg        # ícone do app
```

Os quatro arquivos precisam ficar **na mesma pasta** — o `index.html` referencia os outros três por caminho relativo.

## Funcionalidades

- **Início** — foco do dia, atalhos rápidos, panorama de progresso geral.
- **Personagem** — nível, título (Aspirante → Ronin → Samurai → Mestre → Lenda) e 6 atributos (Estoicismo, Força, Disciplina, Positividade, Paz, Sabedoria) que sobem conforme você completa tarefas nas outras seções.
- **Dia a dia** — hábitos com selo por dia da semana, planejamento semanal, diário.
- **Rumo ao MEXT** — contagem regressiva até a data do exame + roteiro de estudos.
- **Carreira** — roadmap de metas em engenharia de software.
- **Hobbies** — Leitura, Jogos, Gastronomia, Idiomas, Desenho, Karatê Shotokan e Violão, cada um com checklist, notas, check-in diário e um gráfico de constância (sobe com uso regular, cai sozinho com o tempo parado).
- **Vida** — objetivos do ano, reflexão mensal, lista "antes de morrer".
- **Notificações** — conecta a um bot do Telegram seu para receber mensagens/lembretes manuais.

## Tecnologia

Nenhuma dependência externa além de duas fontes do Google Fonts (Zen Old Mincho, Zen Kaku Gothic New, JetBrains Mono), carregadas via CDN. Tudo o resto é JavaScript puro no navegador.

## Rodando localmente

Basta abrir o `index.html` no navegador. Algumas funções (como o service worker, que ativa o modo offline) só funcionam quando o site está hospedado em `http`/`https` — não funcionam abrindo o arquivo direto do computador (`file://`). Para testar isso localmente antes de publicar, rode um servidor simples na pasta do projeto:

```bash
python3 -m http.server 8000
```

e abra `http://localhost:8000`.

## Publicando no GitHub Pages

Veja o passo a passo completo no final desta conversa, ou resumidamente:

1. Crie um repositório no GitHub (pode ser privado) e suba os 4 arquivos na raiz.
2. Em **Settings → Pages**, escolha a branch `main` e a pasta `/ (root)`.
3. Aguarde alguns minutos — o GitHub gera uma URL do tipo `https://SEU-USUARIO.github.io/NOME-DO-REPO/`.
4. Abra essa URL no celular e toque em **Adicionar à tela de início** para instalar como app.

## Integração com Telegram (opcional)

Na seção **Notificações** dentro do app:

1. Fale com `@BotFather` no Telegram → `/newbot` → copie o token gerado.
2. Envie qualquer mensagem para o seu bot novo.
3. Acesse `https://api.telegram.org/bot<TOKEN>/getUpdates` no navegador para descobrir o seu `chat_id`.
4. Cole token e chat id no app e clique em **Salvar**.

Isso permite enviar mensagens de teste ou as pendências do dia diretamente para o seu Telegram, com um clique.

## Privacidade

Os dados (checklists, hábitos, diário, personagem, etc.) ficam salvos apenas para você, vinculados a este app. O token do Telegram também fica salvo localmente e só é usado para chamadas diretas à API do Telegram feitas pelo seu próprio navegador — nenhum dado passa por terceiros além do Telegram.
