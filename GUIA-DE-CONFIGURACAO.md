# Guia de configuração — Ranking de Metas

## O que mudou nesta versão

- Nova atividade **🎥 Vídeo-aula**: 1 ponto por hora.
- Nova atividade **📄 Leitura de PDF**: 2 pontos por hora.
- **Foto opcional** ao registrar uma atividade (fica salva no Firebase Storage).
- **Feed**: mostra as atividades recentes com foto, reações (👍❤️🔥👏) e comentários.
- **Bate-papo**: mensagens em tempo real entre vocês dois.
- **Conquistas (badges)**: Maratonista (7 dias seguidos), Sem enrolação (começou antes das 8h), 100% (3+ atividades num mesmo dia).
- **Meta do casal**: barra de progresso somando os pontos dos dois na semana (meta configurável em `META_SEMANAL_CASAL` no `index.html`).

## Passos para ativar tudo no Firebase

1. **Firestore > Regras**: cole o conteúdo de `firestore.rules` (substitui o que já estava lá — adiciona as coleções `messages`, `reactions` e `comments`, e libera as duas novas atividades).
2. **Storage**: se ainda não tiver ativado, vá em Firebase Console > Storage > "Get started" para criar o bucket (usa o plano gratuito, é só liberar).
3. **Storage > Regras**: cole o conteúdo de `storage.rules`.
4. Publique as regras em ambos os lugares.

Sem o passo 1, o Feed, o Bate-papo, as reações e os comentários vão dar erro de "permissão negada" (o Ranking e o registro de atividades continuam funcionando normalmente, pois usam a coleção antiga `entries`).

Sem o passo 2/3, o upload de foto falha (mas o registro de atividade sem foto continua funcionando).

## Fluxo de atualização a partir de agora

O projeto está ligado a um repositório GitHub. Para pedir uma mudança, é só falar comigo no chat — eu edito o `index.html`, dou commit e push, e o Netlify publica sozinho em cerca de 1 minuto (contanto que o site esteja linkado ao repositório em Netlify > Site settings > Build & deploy > Link repository).
