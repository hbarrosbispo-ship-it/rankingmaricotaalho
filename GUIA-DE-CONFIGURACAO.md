# Guia de configuração — Ranking de Metas

## O que mudou nesta versão

- Removida a atividade "Leitura de material" (os registros antigos continuam no histórico, mas não valem mais pontos novos).
- Nova atividade **🎥 Vídeo-aula**: 1 ponto por hora.
- Nova atividade **📄 Leitura de PDF**: 2 pontos por hora.
- **Foto opcional** ao registrar uma atividade (comprimida no navegador e salva direto no Firestore — sem usar Firebase Storage, que hoje exige plano pago). No celular, o campo de foto já abre a câmera direto (usa o atributo `capture="environment"` do input) em vez de pedir pra escolher da galeria.
- **Feed**: mostra as atividades recentes com foto (clique pra ver em tamanho grande), reações (👍❤️🔥👏😂😮🎉💪) e comentários.
- **Bate-papo**: agora é um widget flutuante (bolha 💬 no canto inferior direito), não uma aba — abre por cima da tela sem sair de onde você está, com uma bolinha vermelha quando chega mensagem nova.
- **Conquistas (badges)**: todas as 11 medalhas aparecem sempre, em cinza; quando conquistadas, ganham cor. São elas: sequência de dias (Pegando o ritmo / Maratonista / Lenda), 100% (3+ atividades num mesmo dia), Centena/Milhar (pontos acumulados), Mestre das questões, Maratona de vídeo-aulas, Leitor voraz, Documentado (5+ fotos) e Comunicativo (10+ comentários).
- **Loja**: 8 prêmios (filme 60, série 100, sobremesa 120, jantar 150, café 250, massagem com as duas mãos de 10 minutos 200, passeio 350, presente surpresa 500). Pontos acumulados (histórico total menos o que já foi resgatado) podem ser trocados. Itens e custos ficam em `STORE_ITEMS` no `index.html`.
- **Meta do casal progressiva**: em vez de uma meta fixa, começa em 20 pontos na primeira semana e sobe a cada semana seguinte (configurável em `META_CASAL_DATA_INICIO`, `META_CASAL_PONTOS_INICIAL` e `META_CASAL_INCREMENTO_SEMANAL` no `index.html`). Quando a meta da semana é batida, aparecem fogos de artifício na tela e uma mensagem de parabéns (uma vez por semana).
- **Simulado** agora vale 4 pontos por vez (era 5).
- **Sono**: só perde ponto se dormir menos de 7h ou mais de 9h (antes só valia 0 pontos dormindo exatamente 8h).
- **Vídeo-aula e Leitura de PDF agora são em minutos, não em horas** (a taxa de pontos continua a mesma, só o jeito de informar o tempo mudou). ⚠️ Registros antigos dessas duas atividades foram lançados em horas — eles continuam no histórico, mas agora são recalculados como se o número fosse minutos, então o total de pontos deles cai bastante. Se isso incomodar, me avise que ajustamos manualmente esses registros antigos.
- **Colar print em qualquer campo do formulário**: clique em qualquer campo do "Registrar atividade" (não precisa ser no campo Foto) e aperte Ctrl+V (ou Cmd+V no Mac) que a imagem da área de transferência é anexada na hora, com prévia aparecendo e um aviso confirmando ("📎 Print colado!").
- Corrigido: a bolinha vermelha do bate-papo agora só aparece quando chega mensagem nova de verdade (antes aparecia sempre, mesmo sem novidade).
- **Editar atividade já publicada**: registros que você mesmo criou agora têm um botão "editar" no Feed, ao lado de "excluir". Abre o mesmo formulário preenchido com os dados atuais pra corrigir valor, data, atividade ou foto.
- **Reações com nome de quem reagiu**: abaixo dos emojis de reação no Feed aparece quem reagiu com cada um (ex: "❤️ Hélio").

## Passos para ativar tudo no Firebase

1. **Firestore > Regras**: cole o conteúdo de `firestore.rules` (substitui o que já estava lá — agora também libera a edição de atividades pelo próprio autor, além da coleção `resgates` usada pela loja).
2. Publique.

Não é preciso ativar o Firebase Storage — as fotos são reduzidas e comprimidas no próprio navegador (redimensionadas para no máximo 900px e convertidas para JPEG de qualidade média) e guardadas como texto dentro do próprio registro no Firestore, que já está no plano gratuito.

Sem o passo 1, o botão "editar" e a Loja vão dar erro de "permissão negada" (o Ranking, Feed, Bate-papo e o registro de novas atividades continuam funcionando normalmente).

## Fluxo de atualização a partir de agora

O projeto está ligado a um repositório GitHub. Para pedir uma mudança, é só falar comigo no chat — eu edito o `index.html`, dou commit e push, e o Netlify publica sozinho em cerca de 1 minuto (contanto que o site esteja linkado ao repositório em Netlify > Site settings > Build & deploy > Link repository).

## Instalar como app no iPhone (PWA)

1. Abra o site no **Safari** (precisa ser o Safari, não o Chrome).
2. Toque no botão de **Compartilhar** (quadrado com seta) e depois em **Adicionar à Tela de Início**.
3. O ícone do 🏆 aparece na tela inicial e o app abre em tela cheia, sem a barra do navegador.

No Android (Chrome): menu ⋮ > **Instalar app**.

Arquivos do PWA: `manifest.webmanifest`, `sw.js` (service worker) e a pasta `icons/`. Se mudar o `index.html`, o app pega a versão nova sozinho quando está online.

## Rebranding "Maricota & Alho" (Temporada 1, 12/11/2026)

- **Novo visual "Aurora"**: tema escuro e claro (botão 🌙/☀️ no topo), cartões com vidro, avatares coloridos, anel de progresso da meta, barra de abas embaixo e botão **+** central para registrar atividade.
- **Reset por temporada**: nada foi apagado. O app só conta registros e resgates feitos depois do `SEASON.corte` (constante no começo do script do `index.html`). O que veio antes aparece em Início > Hall da fama. Para um novo reset no futuro, é só mudar `numero`, `nome`, `inicio` e `corte` (timestamp em ms do momento do reset).
- **Medalhas em 4 níveis** (bronze, prata, ouro, platina) em 4 categorias, mais 4 medalhas secretas. Definidas em `BADGE_DEFS`.
- **Loja nova** com categorias (Mimos, Programinhas, Grandes prêmios, Lendárias), **Cofre da temporada** (meta da dupla, `COFRE`) e **Baú da semana** (sorteio grátis semanal, `BAU_PREMIOS`; o resultado aparece no bate-papo).
- Backup da versão anterior em `backup_pre_rebranding/`.
- Não precisa mudar as regras do Firestore.

## Pacote 2 (engajamento)

- **Sequência com congelador** 🧊: cada semana fechada com 4+ dias ativos dá 1 congelador (máx. 2). Um dia sem registro gasta um congelador em vez de zerar a sequência. Calculado a partir dos registros, sem salvar nada.
- **XP e nível**: 1 ponto = 10 XP, mais 40 XP por missão e 60 XP de bônus por semana com as 3 missões. 11 níveis, de Novato a Imortal (`LEVELS`).
- **Missões semanais**: 3 por semana, giram sozinhas (`MISSION_POOL`). Cada pessoa tem as suas.
- **Duelo da semana**: placar entre os dois, com histórico de vitórias na temporada.
- **Meta pessoal**: só você vê, fica salva neste aparelho (botão "editar").
- **Cutucada** 👋 no ranking (vai para o bate-papo, 1 por dia por pessoa) e **aviso gentil** na tela inicial (depois das 17h sem registro, ou quando falta pouco para a meta da dupla).
- Duas medalhas novas: Missionário e Duelista.

## Pacote 3 (acompanhamento)

- **Aba Painel** (📊): estatísticas por pessoa (pontos, dias ativos, média, melhor dia, tempo de estudo, questões, flashcards, semana vs anterior), gráfico de pontos por dia (14 dias) e por semana, pontos por atividade e **mapa de calor** das últimas 17 semanas (usa todo o histórico, inclusive a temporada anterior).
- **Cronômetro de estudo** ⏱️ com modo pomodoro opcional. Ao parar, abre o formulário já preenchido com os minutos. O estado fica salvo no aparelho, então sobrevive a fechar o app, e uma barra no topo mostra o tempo rodando.
- **Retrospectiva** da semana atual, da semana passada ou do mês, com botão de compartilhar (usa a folha de compartilhamento do iPhone).
- **Exportar dados**: backup em JSON e registros em CSV (sem as fotos).
- Ainda não feitos, porque exigem configuração no Firebase: atividades personalizáveis (precisa mudar as regras do Firestore) e notificações push (precisa do Firebase Cloud Messaging e de um servidor).

## Novo visual (inspirado em apps de estudo reais)

O visual "Aurora" (degradês e vidro) foi trocado por um mais sóbrio: fundo cinza claro, cartões brancos com borda fina, verde-menta como cor principal e roxo de apoio, títulos pequenos em maiúsculas, ícones de linha e medalhas hexagonais. O tema escuro continua disponível (botão no topo) e segue o aparelho na primeira vez. Em tela larga os cartões se dividem em duas colunas.

- Início: indicadores (pontos hoje, sequência, saldo, nível), faixa de **Constância** com os últimos 14 dias, metas semanais em barras.
- Medalhas: hexágono colorido pelo nível, com a meta do nível no centro.
- Versão anterior guardada em `backup_pre_rebranding/index_aurora.html`.

## Ideias de outros apps de estudo (Estugram, Lilo)

- **Desafio da semana**: gira sozinho entre 4 modelos (`DESAFIOS`): metas somadas da dupla, "os dois em 5 dias" e uma **corrida** (quem chega primeiro a 6h de estudo). Dá +50 XP (na corrida, só para quem chega primeiro). Nada é salvo: tudo é calculado dos registros.
- **Interação da semana** (aba Feed): comentário vale 2 pontos e reação 1, só nos registros do outro.
- **Missão com foto**: "Registrar 2 atividades com foto" entrou no sorteio de missões.
- Ainda não feito: "Estudando agora" (mostrar o cronômetro do outro ao vivo) e desafios criados por vocês. Precisam de novos dados no Firebase e, portanto, de mudar as regras.

## Visual v3: mais fiel à plataforma de referência (Estudei)

Reconstruído a partir das telas públicas do Estudei (site, App Store e páginas de divulgação):

- **Barra lateral** no computador (Início, Ranking, Estatísticas, Conquistas, Recompensas, Histórico) e **barra inferior com botão + central** no celular (Início, Ranking, +, Estatísticas, Conquistas, Mais).
- **Cabeçalho de página** com título e subtítulo, botão verde "+ Registrar" e nome do usuário no canto.
- **Início**: 4 indicadores com ícone em quadradinho colorido (pontos da semana com ▲▼ vs semana passada, sequência, saldo, nível), faixa de **Constância** com caixinhas ✓, missões com ícones pastel.
- **Ranking** (página própria): abas Pontos / Questões / Flashcards / Tempo de estudo, pódio com coroa, lista com "a X do 1º", cartão "Sua semana", "Sua evolução" e aviso verde "Mais X pts e você passa…".
- **Estatísticas**: gráfico de pizza com cores pastel e legenda pontilhada, período Hoje/Semana/Mês/Total, heatmap com meses e dias.
- **Conquistas**: hexágonos com o número da meta, título de categoria com "X de Y" e barrinha.
- **Botões flutuantes**: bate-papo (branco) e **cronômetro (verde)**, que abre o foco com anel de progresso.
- Fontes Nunito (títulos) e Open Sans (texto). Versões anteriores em `backup_pre_rebranding/` (`index_aurora.html`, `index_sobrio.html`).
