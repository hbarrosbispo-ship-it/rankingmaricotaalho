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

## Passos para ativar tudo no Firebase

1. **Firestore > Regras**: cole o conteúdo de `firestore.rules` (substitui o que já estava lá — agora também libera a coleção `resgates`, usada pela loja).
2. Publique.

Não é preciso ativar o Firebase Storage — as fotos são reduzidas e comprimidas no próprio navegador (redimensionadas para no máximo 900px e convertidas para JPEG de qualidade média) e guardadas como texto dentro do próprio registro no Firestore, que já está no plano gratuito.

Sem o passo 1, a Loja vai dar erro de "permissão negada" ao tentar resgatar um prêmio (o Ranking, Feed, Bate-papo e o registro de atividades continuam funcionando normalmente).

## Fluxo de atualização a partir de agora

O projeto está ligado a um repositório GitHub. Para pedir uma mudança, é só falar comigo no chat — eu edito o `index.html`, dou commit e push, e o Netlify publica sozinho em cerca de 1 minuto (contanto que o site esteja linkado ao repositório em Netlify > Site settings > Build & deploy > Link repository).
