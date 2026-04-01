# 🐛 Bug Report: Badges de Seguidores e Estrelas Desatualizadas

## 📝 Descrição do Problema

Ao utilizar badges dinâmicas para exibir o número de seguidores e estrelas no perfil do GitHub, é comum notar que os valores exibidos no `README.md` ficam desatualizados em relação aos números reais.

**Sintoma clássico:** 
- No seu perfil do GitHub mostra: **12 seguidores**
- Na badge do README mostra: **1 seguidor**
- Quando você abre a imagem da badge em uma nova aba, ela mostra o valor correto (12).

---

## 🔍 Causa Raiz: O Cache do GitHub (Camo)

Este não é um erro no código do template, mas sim um comportamento padrão da arquitetura do GitHub.

Para proteger a privacidade dos usuários e economizar banda de rede, o GitHub utiliza um proxy de imagens chamado **Camo**. 

Quando você adiciona uma imagem externa (como as badges do `custom-icon-badges` ou `shields.io`) no seu `README.md`:
1. O GitHub (Camo) baixa a imagem do servidor original.
2. Salva uma cópia nos próprios servidores do GitHub.
3. Exibe essa cópia em cache para todos os visitantes do seu perfil.

O problema é que o Camo possui um tempo de expiração de cache (TTL - Time To Live) que pode variar de 24 horas a vários dias. Durante esse período, o GitHub não buscará a imagem atualizada, resultando em dados obsoletos na sua visualização.

---

## ✅ Soluções Possíveis

Existem três abordagens principais para contornar este comportamento de cache.

### Solução 1: "Cache Busting" com Parâmetro de Versão (Recomendado e Imediato)

A técnica mais simples e eficaz é adicionar um parâmetro inútil (dummy parameter) ao final da URL da imagem. Isso força o GitHub a tratar a URL como uma imagem totalmente nova, ignorando o cache existente.

**Como aplicar:**
Adicione `&v=1` ao final da URL. Quando precisar atualizar novamente no futuro, mude para `&v=2`, `&v=3`, e assim por diante.

**Exemplo:**
```html
<!-- ANTES (Com cache preso) -->
<img src="https://custom-icon-badges.demolab.com/github/followers/SEU_USUARIO?color=236ad3&labelColor=1155ba&style=for-the-badge&logo=github&label=Seguidores&logoColor=white"/>

<!-- DEPOIS (Forçando atualização) -->
<img src="https://custom-icon-badges.demolab.com/github/followers/SEU_USUARIO?color=236ad3&labelColor=1155ba&style=for-the-badge&logo=github&label=Seguidores&logoColor=white&v=1"/>
```

### Solução 2: Migrar para a API Oficial Shields.io (Mais Estável)

O serviço `custom-icon-badges.demolab.com` costuma ter cabeçalhos de cache mais longos. O serviço oficial `shields.io` é otimizado para interagir melhor com o proxy do GitHub.

**Como aplicar:**
Substitua o domínio base das suas badges.

**Exemplo:**
```html
<!-- Seguidores via Shields.io -->
<img src="https://img.shields.io/github/followers/SEU_USUARIO?color=236ad3&labelColor=1155ba&style=for-the-badge&logo=github&label=Seguidores&logoColor=white" />
```

### Solução 3: Purge Manual via API (Avançado)

Se você precisa limpar o cache sem alterar o código do README, pode enviar uma requisição HTTP `PURGE` diretamente para o servidor Camo do GitHub.

**Como aplicar:**
1. Inspecione a imagem no seu perfil do GitHub e copie a URL do `camo.githubusercontent.com`.
2. Execute o comando no terminal:
```bash
curl -X PURGE "https://camo.githubusercontent.com/SUA_URL_AQUI"
```

---

## 💡 Recomendação do Autor

Para manter a consistência do template, recomendo utilizar a **Solução 1**. Ela é a menos intrusiva, não requer troca de provedor de badges e resolve o problema instantaneamente com uma alteração mínima no código.

Consulte a pasta `examples/` neste repositório para ver os códigos corrigidos prontos para uso.
