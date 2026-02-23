# Alma 11:11 Audio — Portfolio Website

Site institucional e portfólio para a **Alma 11:11 Audio**, empresa de produção musical para publicidade e conteúdo com prêmios em Cannes Lions, Clios, El Ojo e mais de 65 prêmios internacionais.

![Preview](public.html/images/logo.png)

---

## Sobre o Projeto

Site desenvolvido com foco em performance, elegância visual e facilidade de gestão de conteúdo. Os sócios podem adicionar, editar e remover trabalhos diretamente pelo painel admin, sem precisar mexer em código.

---

## Funcionalidades

- **Carrossel hero** com vídeos do Vimeo em background (autoplay, mudo)
- **Grid de works** com filtro por categoria, paginação de 6 itens e thumbnail estática por padrão
- **Preview de vídeo no hover** — carrega o iframe apenas ao passar o mouse (otimização de performance)
- **Lightbox** para reprodução do vídeo em tela cheia
- **Sistema de prêmios** — tags douradas com estrela em cada work
- **Navegação lateral** estilo agenda, com marcador de progresso ao scroll
- **Formulário de contato** em modal integrado com Formspree
- **Painel Admin** protegido por autenticação Firebase
  - Adicionar, editar e remover works
  - Reordenar via botões ↑↓
  - Campo de prêmios com tags editáveis
  - Preview ao vivo do vídeo ao cadastrar
  - Sugestão automática de categorias já cadastradas
- **Responsivo** — mobile, tablet e desktop

---

## Stack

| Camada | Tecnologia |
|---|---|
| Frontend | HTML5, CSS3, JavaScript (ES Modules) |
| Banco de dados | Firebase Firestore |
| Autenticação | Firebase Authentication |
| Vídeos | Vimeo Player API |
| Thumbnails | Vumbnail.com |
| Formulário | Formspree |
| Hospedagem | Hostinger |

Sem frameworks, sem build process — arquivos estáticos puros.

---

## Estrutura

```
/
├── index.html        # Site público
├── login.html        # Autenticação dos parceiros
├── admin.html        # Painel de gestão de works
├── images/
│   ├── logo.png
│   └── foto4_footer.png
├── .gitignore
└── README.md
```

---

## Configuração

### 1. Firebase

1. Crie um projeto em [console.firebase.google.com](https://console.firebase.google.com)
2. Ative o **Firestore Database** (modo produção)
3. Ative o **Authentication → Email/Password**
4. Crie os usuários admin na aba Authentication
5. Configure as regras do Firestore:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /works/{document=**} {
      allow read: if true;
      allow write: if request.auth != null;
    }
  }
}
```

6. Copie o `firebaseConfig` de **Project Settings → Your apps → Web**
7. Cole o config nos três arquivos HTML onde indicado (`COLE SEU firebaseConfig AQUI`)

### 2. Formspree

1. Crie uma conta em [formspree.io](https://formspree.io)
2. Crie um novo formulário
3. Substitua o endpoint em `index.html`:

```javascript
fetch('https://formspree.io/f/SEU_ID_AQUI', ...)
```

### 3. Deploy na Hostinger

Suba os arquivos via File Manager ou FTP para a pasta `public_html`.

---

## Dados dos Works (Firestore)

Coleção: `works`

| Campo | Tipo | Descrição |
|---|---|---|
| `vimeoId` | string | ID do vídeo no Vimeo |
| `title` | string | Título do work |
| `category` | string | Categoria (ex: Advertising) |
| `featured` | boolean | Aparece no carrossel hero |
| `awards` | array | Lista de prêmios ganhos |
| `order` | number | Ordem de exibição no grid |

---

## Desenvolvimento

**Rodando localmente:**

Use um servidor HTTP local — não abra os arquivos diretamente no browser (`file://`) pois o Firebase Auth não funciona nesse protocolo.

Opções rápidas:
```bash
# Python
python3 -m http.server 8080

# VS Code
# Instale a extensão Live Server e clique em "Go Live"

# Node
npx serve .
```

Acesse em `http://localhost:8080`

---

## Créditos

- **Alma 11:11 Audio** — [alma1111audio.com.br](https://alma1111audio.com.br)
- **WebDev** — [RPaplaus](https://paplauskas.com.br)

---

## Licença

Projeto proprietário. Todos os direitos reservados © 2026 Alma 11:11 Audio.
