# Códice & Memoria — Guia de Publicação

Este é o seu arquivo público de estudos médicos. Ele foi construído pra funcionar como um site **estático** (sem servidor, sem banco de dados), o que significa:

- ✅ **Hospedagem 100% grátis e permanente** (GitHub Pages, Netlify, Cloudflare Pages)
- ✅ **Rápido** — carrega instantaneamente
- ✅ **Zero manutenção** — não tem servidor pra cair
- ✅ **Editável com um arquivo só** (`artefatos.json`)

---

## 📂 Arquivos do projeto

| Arquivo | O que é |
|---|---|
| `index.html` | O site em si. Não precisa editar. |
| `artefatos.json` | **O banco de dados.** Edite este arquivo para adicionar, remover ou modificar artefatos. |
| `README.md` | Este guia. |

---

## 🚀 Como publicar (passo-a-passo)

### Opção 1 — GitHub Pages (recomendado, 5 minutos)

1. **Crie uma conta no GitHub** (se ainda não tem): https://github.com/signup
2. **Crie um novo repositório público** chamado, por exemplo, `codice-med`
3. **Faça upload dos 3 arquivos** (`index.html`, `artefatos.json`, `README.md`) — pode arrastar direto no navegador, na tela do repositório recém-criado
4. No repositório, vá em **Settings → Pages**
5. Em "Source", selecione **"Deploy from a branch"**, branch **"main"**, pasta **"/ (root)"**, e clique em **Save**
6. Aguarde ~1 minuto. Seu site estará no ar em: `https://SEU-USUARIO.github.io/codice-med/`

**Para atualizar depois:** basta editar `artefatos.json` direto no GitHub (botão do lápis) e fazer commit. O site atualiza em 30 segundos.

### Opção 2 — Netlify Drop (30 segundos, sem conta)

1. Vá em https://app.netlify.com/drop
2. Arraste a **pasta inteira** com os 3 arquivos pra janela
3. Pronto. Netlify te dá uma URL tipo `https://kalume-med.netlify.app`

Boa pra testar. Pra publicar "de verdade" e atualizar facilmente, use GitHub Pages.

---

## ✏️ Como adicionar um novo artefato

Abra `artefatos.json` e adicione um novo objeto dentro do array `"artefatos"`:

```json
{
  "id": "nome-curto-unico",
  "titulo": "Título do Artefato",
  "resumo": "Descrição de uma ou duas linhas sobre o conteúdo.",
  "ciclo": "sem-3",
  "materia": "patologia",
  "tags": ["quiz", "prova"],
  "url": "https://link-do-seu-artefato.com",
  "dataPublicacao": "2025-11-28",
  "duracaoEstimada": 45,
  "destaque": false
}
```

**Campos:**

| Campo | Obrigatório | Descrição |
|---|---|---|
| `id` | ✅ | Identificador único (sem espaços, use `-`). Vira parte da URL. |
| `titulo` | ✅ | Nome do artefato |
| `resumo` | ✅ | 1-2 linhas sobre o conteúdo |
| `ciclo` | ✅ | ID do ciclo (ver array `ciclos` no JSON) |
| `materia` | ✅ | ID da matéria (ver array `materias`) |
| `tags` | recomendado | Array de strings |
| `url` | recomendado | Link do artefato hospedado |
| `dataPublicacao` | ✅ | Formato `YYYY-MM-DD` |
| `duracaoEstimada` | opcional | Em minutos |
| `destaque` | opcional | `true` coloca na seção "Destaques" (máx. 3) |

### Onde hospedar os artefatos em si (os HTMLs)

Os artefatos interativos (quizzes, mind maps, etc.) podem ficar em qualquer lugar com URL pública:

- **Mesmo repositório do GitHub Pages** → `https://seu-usuario.github.io/codice-med/artefatos/tuberculose.html` (recomendado — tudo junto)
- **Google Drive** → compartilhe público, pegue o link direto
- **Netlify Drop individual** → cada artefato como um site próprio

### Adicionar uma nova matéria ou ciclo

No JSON, edite o array `"materias"`:

```json
{ "id": "anatomia", "nome": "Anatomia", "cor": "#b87a4f", "icone": "microscope" }
```

Ou `"ciclos"`:

```json
{ "id": "sem-4", "nome": "4º Semestre", "ordem": 4, "periodo": "2026.1" }
```

---

## 💬 Ativando comentários (opcional — via Giscus)

O site já tem espaço reservado para comentários. Para ativar de verdade:

1. Vá em https://giscus.app
2. Escolha seu repositório GitHub (precisa ser público)
3. Ative **GitHub Discussions** no repositório (em Settings → Features)
4. Siga o wizard do Giscus — ele te dá um script pra copiar
5. No `index.html`, procure por `<div class="comments-section">` dentro do `renderDetail()` e substitua pelo container do Giscus

Vantagens:
- Grátis para sempre
- Comentaristas precisam de conta GitHub (zero spam)
- Os comentários ficam salvos no próprio Discussions do repositório

---

## 🎨 Personalização rápida

**Mudar seu nome, bio, localidade:** edite o objeto `"autor"` no JSON:

```json
"autor": {
  "nome": "Seu Nome",
  "bio": "Estudante de Medicina",
  "localidade": "Sua Cidade, UF",
  "github": "seu-usuario"
}
```

**Mudar cores do tema:** no `index.html`, procure `:root[data-theme="dark"]` e ajuste as variáveis CSS (`--accent`, `--bg`, etc.).

---

## 🔧 Recursos implementados

- ✨ **3 visualizações**: grade, linha do tempo, mapa de conhecimento (SVG)
- 🔍 Busca em tempo real (título, resumo, tags, matéria)
- 🏷️ Nuvem de tags clicáveis
- 📊 Estatísticas animadas
- ⭐ Seção de destaques
- 🌓 Modo claro/escuro (salvo no navegador)
- ❤️ Sistema de curtidas (local, por visitante)
- 📈 Contador de visualizações (local, por visitante)
- 📱 Responsivo (celular/tablet/desktop)
- 🔗 URLs compartilháveis (`#/a/tuberculose-quiz`)
- 📤 Botão de compartilhar nativo (Web Share API)
- 🎭 Animações suaves de entrada
- ⌨️ Acessível via teclado

---

## ❓ Dúvidas frequentes

**Se eu não editar `artefatos.json`, só o `index.html`, funciona?**  
Sim, mas o site vai carregar vazio (com um exemplo só, como fallback). Você **precisa** servir `artefatos.json` junto.

**Posso testar localmente antes de publicar?**  
Abrir o `index.html` direto no navegador (file://) pode falhar ao carregar o JSON por CORS. Melhor usar um servidor local simples:
- Se tiver Python: `python3 -m http.server` na pasta do projeto
- Ou VS Code com extensão "Live Server"

**Posso ter um domínio próprio tipo `kalume.med.br`?**  
Sim. No GitHub Pages é só apontar o DNS do domínio e configurar em Settings → Pages → Custom domain.

**Como faço backup?**  
Se usar GitHub, o próprio repositório já é o backup. Toda alteração fica versionada.

---

*Feito com paciência e tipografia serifada.*
