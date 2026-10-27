# Fichas RPG — Véu Corrompido

Protótipo inicial de fichas de RPG com estética dark/gótica, sincronização via Firebase Firestore e autenticação por e-mail/senha.

## O que já tem
- Vida atual/máxima, mana atual/máxima, dinheiro, arma, dano, habilidades e itens.
- Ficha especial Ludwig com caixas independentes de Calor e Corrupção.
- Painel do mestre com visão das fichas e atualizações em tempo real.
- Autenticação por e-mail/senha.

## Configuração necessária antes de compartilhar

### 1. Ativar login por e-mail
No Firebase Console: Authentication → Começar / Get started → Sign-in method → Email/Password → Ativar → Salvar.

### 2. Pegar UID da conta do mestre
1. Crie uma conta de mestre pelo site publicado (ou localmente).
2. Firebase Console → Authentication → Users.
3. Copie o UID dessa conta.
4. Abra `firestore.rules` e substitua `COLE_AQUI_UID_DO_MESTRE` pelo UID real.
5. Publique as regras em Firestore Database → Regras (Rules).

### 3. Tornar essa conta mestre
Depois de publicar as regras, no Firestore crie manualmente uma coleção `roles`, com um documento cujo ID seja o UID da conta do mestre e campo:
- `role` (string): `master`

O documento de `roles` é lido pelo site para mostrar o painel. A autorização real de mestre nas regras é determinada pelo UID fixo em `firestore.rules`.

### 4. Publicar o site
Suba `index.html` para um repositório GitHub. Em Settings → Pages, escolha publicar a partir da branch `main` e pasta `/(root)`. Aguarde o link ficar disponível.

## Segurança importante
- Não use regras abertas ao público.
- Cada jogador só deve conseguir ler/editar a própria ficha; o mestre pode ler/editar todas as fichas depois que o UID estiver configurado nas regras.
- Não compartilhe o UID do mestre publicamente se não for necessário.
- A configuração `firebaseConfig` no HTML identifica o projeto web; ela não substitui regras de segurança.
- Teste primeiro com contas de teste antes de mandar o link à mesa.

## Limitações atuais do protótipo
- O mestre vê todas as fichas em tempo real. A edição direta de fichas de outros jogadores ainda precisa de uma interface própria; por enquanto, o mestre pode acompanhar o estado de todos.
- Cada conta cria uma ficha com um nome. A ficha especial é ativada quando o nome do personagem é exatamente `Ludwig`.
- Os campos salvam automaticamente ao serem alterados.
