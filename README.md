---
source-git-commit: 6233779ba2e2a99ed229f8aa97497eb8d9d877f7
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 5%

---
# Documentação técnica do Adobe Commerce Intelligence

Agradecemos as contribuições da comunidade e de funcionários da Adobe de fora das equipes de documentação.

## Código de conduta do Adobe Open Source

Este projeto adotou o [Código de conduta de código aberto da Adobe](code-of-conduct.md) ou o [Código de conduta do .NET Foundation](https://dotnetfoundation.org/code-of-conduct). Para obter mais informações, consulte o artigo [Contribuição](contributing.md).

## Sobre suas contribuições para o conteúdo do Adobe

Consulte o [Guia do colaborador do Adobe Docs](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=pt-BR).

A forma como você contribui depende de quem você é e do tipo de alterações com as quais deseja contribuir:

### Pequenas alterações

Se você estiver contribuindo com pequenas atualizações, visite o artigo e clique na área de feedback que aparece na parte inferior do artigo, clique em **Opções de feedback detalhadas** e em **Sugerir uma edição** para ir para o arquivo de origem do Markdown no GitHub. Use a interface do GitHub para fazer suas atualizações. Consulte o [guia geral do colaborador do Adobe Docs](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=pt-BR) para obter mais informações.

Pequenas correções ou esclarecimentos que você envia para documentação e exemplos de código neste repositório são cobertos pelos termos de uso da Adobe.

### Grandes alterações ou novos artigos de membros da comunidade

Se você fizer parte da comunidade da Adobe e quiser criar um novo artigo ou enviar grandes alterações, use a guia Problemas no repositório Git para enviar um problema e iniciar uma conversa com a equipe de documentação. Depois de concordar com um plano, você precisará trabalhar com um funcionário para ajudá-lo a inserir o novo conteúdo por meio de uma combinação de trabalho nos repositórios públicos e privados.

### Grandes mudanças de funcionários da Adobe

Se você for um autor técnico, gerente de programa ou desenvolvedor da equipe de produtos de uma solução da Adobe Experience Cloud e seu trabalho for contribuir com ou criar artigos técnicos, deverá usar o repositório privado em `https://git.corp.adobe.com/AdobeDocs`.

## Ferramentas e configuração

Os colaboradores da comunidade podem usar a interface do usuário do GitHub para a edição básica ou bifurcar o repositório para fazer grandes contribuições.

Consulte o [Guia do colaborador do Adobe Docs](https://experienceleague.adobe.com/docs/contributor/contributor-guide/introduction.html?lang=pt-BR) para obter mais detalhes.

## Como usar marcação para formatar seu tópico

Todos os artigos neste repositório usam GitHub flavored markdown. Se não estiver familiarizado com a marcação, consulte:

- [Noções básicas do Markdown](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)
- [Cheatsheet de markdown para impressão](https://guides.github.com/pdfs/markdown-cheatsheet-online.pdf)

## Ganchos de pré-confirmação para otimização de imagem

Esse repositório inclui ganchos de pré-confirmação automatizados que otimizam imagens antes da confirmação. **Todos os colaboradores devem habilitar esses ganchos** para garantir uma otimização de imagem consistente e um tamanho de repositório reduzido.

### Configuração rápida

Após clonar o repositório, execute:

```bash
.githooks/setup-hooks.sh
```

### O que os ganchos fazem

- Detectar automaticamente arquivos de imagem preparados (PNG, JPG, JPEG, GIF, SVG)
- Executar `image_optim` para compactar e otimizar imagens
- Transferir imagens otimizadas automaticamente
- Garantir que todas as imagens confirmadas estejam corretamente otimizadas

### Benefícios

- Tamanho reduzido do repositório
- Carregamentos de página mais rápidos para a documentação
- Qualidade de imagem consistente em todos os colaboradores
- Não é necessária otimização manual

Para obter instruções detalhadas de instalação, solução de problemas e configuração, consulte [`.githooks/README.md`](.githooks/README.md).
