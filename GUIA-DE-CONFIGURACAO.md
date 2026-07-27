# Guia de configuração — Ranking de Metas

## O que mudou nesta versão

- Nova atividade **🎥 Vídeo-aula**: 1 ponto por hora.
- Nova atividade **📄 Leitura de PDF**: 2 pontos por hora.
- **Foto opcional** ao registrar uma atividade (comprimida no navegador e salva direto no Firestore — sem usar Firebase Storage, que hoje exige plano pago).
- **Feed**: mostra as atividades recentes com foto, reações (👍❤️🔥👏) e comentários.
- **Bate-papo**: mensagens em tempo real entre vocês dois.
- **Conquistas (badges)**: Maratonista (7 dias seguidos), Sem enrolação (começou antes das 8h), 100% (3+ atividades num mesmo dia).
- **Meta do casal**: barra de progresso somando os pontos dos dois na semana (meta configurável em `META_SEMANAL_CASAL` no `index.html`).

## Passos para ativar tudo no Firebase

1. **Firestore > Regras**: cole o conteúdo de `firestore.rules` (substitui o que já estava lá — adiciona as coleções `messages`, `reactions` e `comments`, e libera as duas novas atividades).
2. Publique.

Não é preciso ativar o Firebase Storage — as fotos são reduzidas e comprimidas no próprio navegador (redimensionadas para no máximo 900px e convertidas para JPEG de qualidade média) e guardadas como texto dentro do próprio registro no Firestore, que já está no plano gratuito.

Sem o passo 1, o Feed, o Bate-papo, as reações e os comentários vão dar erro de "permissão negada" (o Ranking e o registro de atividades continuam funcionando normalmente, pois usam a coleção antiga `entries`).

## Fluxo de atualização a partir de agora

O projeto está ligado a um repositório GitHub. Para pedir uma mudança, é só falar comigo no chat — eu edito o `index.html`, dou commit e push, e o Netlify publica sozinho em cerca de 1 minuto (contanto que o site esteja linkado ao repositório em Netlify > Site settings > Build & deploy > Link repository).
