# 🔧 Como Funciona a API de Estatísticas do GitHub

## 📌 Introdução

Quando você vê os cards de estatísticas no seu perfil do GitHub (aqueles que mostram commits, PRs, estrelas, etc), eles não são imagens estáticas. Eles são gerados dinamicamente por uma API em tempo real! Vou explicar como isso funciona por trás dos panos.

---

## 🌐 O que é a GitHub Readme Stats?

A **GitHub Readme Stats** é um projeto open-source criado por [Anurag Hazra](https://github.com/anuraghazra) que fornece uma API pública para gerar cards visuais com suas estatísticas do GitHub.

**Repositório oficial:** https://github.com/anuraghazra/github-readme-stats

---

## 🔄 Como Funciona o Fluxo de Requisição

### Passo 1: Você Adiciona a URL no README
Quando você coloca uma tag `<img>` com uma URL da API no seu README, você está criando uma requisição HTTP.

```html
<img src="https://github-readme-stats-sigma-five.vercel.app/api?username=SEU_USUARIO&show_icons=true&theme=tokyonight" />
```

### Passo 2: O GitHub Carrega a Página
Quando alguém acessa seu perfil do GitHub, o navegador tenta carregar a imagem especificada na URL.

### Passo 3: A API Processa a Requisição
A API recebe a requisição com os parâmetros (seu username, tema, etc) e:
1. Acessa a API pública do GitHub para obter seus dados
2. Processa as informações (calcula commits, PRs, estrelas, etc)
3. Gera uma imagem SVG estilizada com os dados
4. Devolve a imagem para o navegador

### Passo 4: A Imagem é Exibida
O navegador recebe a imagem SVG e a exibe no seu perfil.

---

## 📊 Parâmetros Disponíveis

Você pode personalizar a API adicionando parâmetros à URL. Aqui estão os principais:

| Parâmetro | Descrição | Exemplo |
|-----------|-----------|---------|
| `username` | Seu nome de usuário do GitHub (obrigatório) | `username=DosAnjos013` |
| `show_icons` | Mostra ícones nas estatísticas | `show_icons=true` |
| `theme` | Define o tema de cores | `theme=tokyonight` |
| `locale` | Define o idioma | `locale=pt-br` |
| `include_all_commits` | Inclui todos os commits (não apenas do branch padrão) | `include_all_commits=true` |
| `layout` | Layout para top linguagens (compact, donut, etc) | `layout=compact` |

---

## 🎨 Temas Disponíveis

Você pode escolher entre diversos temas para personalizar a aparência dos cards:

- `tokyonight` (padrão, tema escuro com tons de roxo)
- `dracula` (tema escuro com tons de roxo/rosa)
- `dark` (tema escuro minimalista)
- `radical` (tema escuro com cores vibrantes)
- `vue` (tema claro com tons de verde)
- `nord` (tema escuro com tons de azul)
- `github_dark` (tema escuro similar ao GitHub)
- `onedark` (tema escuro com tons de azul)

**Dica:** Teste diferentes temas para encontrar o que mais combina com seu estilo!

---

## 🔐 Privacidade e Dados Públicos

A API da GitHub Readme Stats **só acessa dados públicos** do seu perfil. Ela não tem acesso a:
- Repositórios privados
- Dados pessoais
- Informações de email
- Qualquer informação que você não tenha tornado pública

Portanto, é completamente seguro usar essa API!

---

## ⚡ Performance e Cache

A API implementa um sistema de cache para otimizar a performance:
- As imagens são cacheadas por um período de tempo
- Isso evita que a API seja chamada a cada vez que alguém acessa seu perfil
- O cache é atualizado periodicamente para manter os dados frescos

---

## 🛠️ Alternativas e Extensões

Se você quiser explorar mais opções, existem outras APIs e ferramentas similares:

- **GitHub Readme Streak Stats:** Mostra uma contagem de dias consecutivos com commits
- **GitHub Readme Activity Graph:** Exibe um gráfico de atividade ao longo do tempo
- **Wakatime Stats:** Mostra tempo gasto em diferentes linguagens (requer integração com Wakatime)

---

## 💡 Dicas Finais

1. **Mantenha Seu Perfil Atualizado:** Quanto mais commits e projetos você tiver, mais impressionantes serão suas estatísticas!
2. **Personalize os Temas:** Escolha um tema que combine com sua identidade profissional
3. **Adicione Mais Cards:** Explore a documentação oficial para adicionar mais tipos de cards (contribuições, repositórios destacados, etc)
4. **Teste Localmente:** Você pode copiar a URL no navegador e adicionar parâmetros para testar diferentes configurações

---

## 📚 Referências

- [GitHub Readme Stats - Repositório Oficial](https://github.com/anuraghazra/github-readme-stats)
- [Documentação Completa](https://github.com/anuraghazra/github-readme-stats#readme)
- [API do GitHub](https://docs.github.com/en/rest)

