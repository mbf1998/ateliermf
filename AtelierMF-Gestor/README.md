# AtelierMF · Gestor

Gestor do Atelier Mariana Fragoso (peças, materiais, horas, vendas e relatórios).
Todos os dados são gravados no **Firebase (Firestore)** e o acesso é protegido por **login (Authentication)**.

## Estrutura
- `public/index.html`: o sistema (logo já embutida)
- `public/firebase-config.js`: **suas chaves do Firebase** (único arquivo a editar)
- `public/manifest.webmanifest`, `public/sw.js`, `public/icons/`: deixam o gestor instalável no celular
- `firestore.rules`: regras de segurança (troque o e-mail)
- `firebase.json`, `.firebaserc`, `firestore.indexes.json`: configuração de deploy

## Passo a passo
1. Em https://console.firebase.google.com crie um projeto.
2. **Build > Authentication**: ative "E-mail/senha" e crie o usuário da Mariana (Users > Add user).
3. **Build > Firestore Database**: crie o banco (modo produção).
4. **Configurações do projeto > Seus apps > Web (</>)**: registre o app e copie o `firebaseConfig` para `public/firebase-config.js`.
5. Em `firestore.rules`, troque `SEU-EMAIL@EXEMPLO.COM` pelo e-mail do passo 2.
6. Em `.firebaserc`, troque pelo ID do projeto.
7. No terminal, dentro desta pasta:
   ```
   npm install -g firebase-tools
   firebase login
   firebase deploy
   ```
   O `deploy` publica o site (Hosting) e as regras (Firestore).

O site fica em `https://SEU-PROJETO.web.app`. Teste local: `firebase emulators:start --only hosting`
(o login só funciona em `localhost` ou no endereço publicado, não abrindo o arquivo direto).

## Coleções no Firestore
`pecas`, `materiais`, `horas`, `producoes`, `vendas`, `lotes`, `despesas` e o documento `config/geral`
(categorias das peças, valor da hora e metas ficam em `config/geral`).
Fotos das peças são reduzidas (~520 px) e guardadas dentro do documento da peça.

## Observações
- Com `apiKey` vazio, o sistema abre em modo demonstração (dados de exemplo só no navegador).
- Em Ajustes há backup em JSON para baixar e restaurar.

## Recursos
- **Peças secando:** na peça, "Colocar para secar" cria um lote com data de pronto; o painel avisa quando é hora de pintar.
- **Despesas e custos fixos:** em Relatórios. Mensais (MEI, internet...) e avulsas (feiras). Entram no lucro real.
- **Metas:** vendas por mês e horas por semana (Ajustes).
- **Catálogo:** texto para WhatsApp ou PDF com fotos (Peças > Catálogo).
- **Etiquetas de preço:** impressão em folha A4 (Peças > Etiquetas).
- **Categorias das peças:** Ajustes > Categorias das peças.
- **Tema escuro:** Ajustes > Aparência (ou botão na barra lateral).
- **App no celular:** Ajustes > Instalar no celular. Funciona no endereço publicado (https).
- O Firestore mantém cache offline: se a internet cair, o que você registrar sincroniza quando voltar.
