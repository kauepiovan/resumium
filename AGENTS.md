<!-- BEGIN:nextjs-agent-rules -->

## This is NOT the Next.js you know

This version has breaking changes — APIs, conventions, and file structure may all differ from your training data. Read the relevant guide in `node_modules/next/dist/docs/` (resolved from this file's directory; in monorepos the `next` package may not be visible from the repo root) before writing any code. Heed deprecation notices.

This block is written and re-added by `next dev` — verify at `node_modules/next/dist/server/lib/generate-agent-files.js`. Removing it from a diff only re-creates the uncommitted change; committing it with your work keeps the tree clean.

<!-- END:nextjs-agent-rules -->

## RESUMIUM

As especificações e regras dos domínios da aplicação estão em [docs/domains.md](docs/domains.md). Leia essa documentação antes de criar ou alterar comportamentos de negócio.

## Workflow de desenvolvimento

Este projeto adota desenvolvimento orientado por especificação. Salvo quando o usuário autorizar explicitamente a combinação de etapas, todo trabalho deve seguir a ordem abaixo e respeitar os critérios de saída de cada fase.

### 1. Especificar o comportamento

- Começar pela necessidade do usuário e pelo comportamento esperado, não pela solução técnica.
- Inspecionar a documentação e a implementação existentes antes de propor mudanças.
- Definir objetivo, atores, fluxo principal, regras de negócio, dados de entrada e saída, erros, casos-limite, escopo e critérios de aceitação.
- Apresentar alternativas e seus impactos quando houver decisões relevantes ainda abertas.
- Registrar em [docs/domains.md](docs/domains.md) toda decisão permanente sobre domínios, contratos e regras de negócio aprovada pelo usuário.
- Tratar rascunhos e propostas como material em revisão; eles só se tornam fonte de verdade após a aprovação do usuário.

**Critério de saída:** comportamento compreendido, decisões relevantes resolvidas, critérios de aceitação definidos e documentação revisada.

### 2. Elaborar o plano de ação

- Explorar o código atual e as restrições técnicas aplicáveis antes de planejar.
- Produzir um plano fechado para decisão, descrevendo mudanças por comportamento ou subsistema, contratos e tipos afetados, fluxo de dados, casos de falha, compatibilidade e forma de verificação.
- Relacionar o plano às regras de negócio documentadas e indicar qualquer documentação que precise ser atualizada.
- Não implementar código quando o pedido for apenas para analisar, discutir, especificar, propor ou planejar.

**Critério de saída:** plano revisado pelo usuário, sem decisões importantes deixadas para a implementação, seguido de autorização explícita para executá-lo.

### 3. Revisar antes de implementar

- Incorporar observações e correções do usuário primeiro na especificação e depois no plano.
- Considerar a versão aprovada mais recente como substituta das versões anteriores.
- Voltar à fase de especificação quando uma correção mudar comportamento, contrato ou regra de negócio.
- Não antecipar a implementação enquanto houver decisão relevante em revisão.

**Critério de saída:** especificação e plano coerentes entre si e aprovados para implementação.

### 4. Implementar a feature

- Implementar somente o escopo autorizado, seguindo a documentação e o plano aprovados.
- Manter contratos, tipos, validações e mensagens de erro alinhados às regras de negócio.
- Não alterar silenciosamente uma regra aprovada para facilitar a implementação.
- Interromper a parte afetada e retornar à especificação ou ao plano quando surgir uma contradição, uma decisão de produto ausente ou a necessidade de ampliar materialmente o escopo.
- Manter a documentação sincronizada quando a implementação aprovada exigir ajustes nela.

**Critério de saída:** comportamento implementado conforme o contrato documentado, sem mudanças de escopo não aprovadas.

### 5. Verificar e entregar

- Verificar todos os critérios de aceitação e os casos de sucesso, erro e limite definidos no plano.
- Executar as verificações técnicas proporcionais à mudança, como análise estática, lint, testes e build, quando aplicáveis ao escopo.
- Conferir que documentação, tipos, validações e comportamento final descrevem a mesma regra.
- Informar o que mudou, como foi verificado e qualquer limitação ou trabalho pendente.

**Critério de conclusão:** critérios de aceitação atendidos, verificações relevantes aprovadas e documentação consistente com a implementação.

### Interpretação dos pedidos

- **“Analisar”, “discutir”, “rascunhar”, “especificar” ou “propor”** autoriza investigação e documentação da proposta, sem implementação da feature.
- **“Planejar”** autoriza a elaboração ou revisão do plano, sem implementação da feature.
- **“Revisar” ou “corrigir”** mantém o trabalho na fase atual, salvo autorização explícita para avançar.
- **“Implementar”, “aplicar” ou “executar o plano”** autoriza mudanças dentro do escopo já aprovado.
- Uma instrução explícita do usuário pode combinar fases ou alterar este fluxo para uma tarefa específica.

### Fontes de verdade

- `docs/domains.md`: comportamentos, contratos e regras de negócio permanentes.
- `AGENTS.md`: instruções operacionais, workflow e referências para agentes.
- `tasks.md`: acompanhamento de trabalho e backlog; não substitui a documentação de domínio.
- Código e validações: implementação da especificação aprovada; divergências devem ser resolvidas antes de concluir a feature.

## Padrões de codificação

Estes padrões se aplicam a todo código novo ou alterado. Código legado fora do escopo não deve ser refatorado silenciosamente, mas também não deve servir de justificativa para repetir um padrão inadequado.

### Princípios gerais

- Priorizar legibilidade, clareza de intenção e facilidade de manutenção acima da redução de linhas ou caracteres.
- Escrever para revisão humana: o código deve permitir que outra pessoa entenda seu propósito, fluxo e decisões sem depender do autor.
- Usar Clean Code e SOLID como referências de design, aplicando julgamento técnico em vez de seguir regras de forma mecânica.
- Preferir a solução mais simples que satisfaça o comportamento aprovado. Evitar otimização prematura, abstrações especulativas e complexidade sem benefício demonstrável.
- Seguir as recomendações oficiais e atuais das tecnologias utilizadas, respeitando primeiro as restrições específicas deste projeto.
- Manter cada mudança pequena e coesa, sem misturar a feature autorizada com reorganizações ou melhorias não relacionadas.

### Idioma e nomenclatura

- Escrever em inglês nomes de arquivos de código, diretórios de código, variáveis, funções, componentes, classes, tipos, interfaces, schemas, constantes e demais identificadores.
- Usar nomes completos e orientados ao domínio. Evitar abreviações obscuras, nomes genéricos e detalhes de implementação que escondam a intenção.
- Nomear booleanos com prefixos que indiquem uma pergunta, como `is`, `has`, `can` ou `should`.
- Manter o mesmo conceito com o mesmo nome em documentação, contratos, tipos, validações e implementação.
- Textos exibidos ao usuário devem seguir o idioma e as regras de produto definidos para a interface; eles não precisam ser traduzidos para inglês por serem parte do código.

### Estrutura e design

- Dar a funções, componentes e módulos uma responsabilidade principal clara e manter juntas apenas responsabilidades que mudam pelo mesmo motivo.
- Separar regras de negócio de apresentação, persistência, integrações externas e detalhes do framework.
- Direcionar dependências para contratos e regras estáveis do domínio, evitando que o domínio dependa da interface ou da infraestrutura.
- Preferir composição a herança e fluxo de dados explícito a estado implícito ou compartilhado sem necessidade.
- Criar abstrações somente quando houver uma responsabilidade ou variação real. Uma pequena duplicação é preferível a uma abstração incorreta ou prematura.
- Manter efeitos colaterais nas bordas do sistema e favorecer funções determinísticas para transformações e regras de negócio.
- Substituir valores mágicos por constantes nomeadas quando o valor tiver significado de negócio ou for reutilizado.

### TypeScript, dados e erros

- Preservar o modo estrito do TypeScript e modelar estados válidos nos tipos sempre que possível.
- Não usar `any` para contornar o sistema de tipos. Usar `unknown` em fronteiras não confiáveis e validar antes de acessar os dados.
- Não usar type assertions, non-null assertions ou coerções apenas para silenciar erros; quando forem realmente necessárias, justificar a segurança da operação.
- Validar dados nas fronteiras da aplicação, especialmente entradas do usuário, respostas externas, variáveis de ambiente e dados persistidos.
- Tratar erros de forma explícita e manter mensagens úteis para diagnóstico, sem expor segredos ou dados pessoais do currículo em logs.
- Preferir imutabilidade, `const` e transformações sem mutação quando isso tornar o fluxo mais previsível.

### Comentários e documentação no código

- Comentários são permitidos quando melhoram o entendimento e podem ser escritos em português do Brasil.
- Usar comentários para explicar motivos, regras não óbvias, invariantes, decisões, limitações ou workarounds. Não repetir em texto aquilo que o código já expressa claramente.
- Manter comentários próximos do código relevante e atualizá-los junto com a implementação. Comentário desatualizado deve ser corrigido ou removido.
- Documentar APIs, contratos ou comportamentos compartilhados quando seu uso correto não puder ser entendido somente pelos tipos e nomes.
- Não deixar `TODO`, `FIXME` ou comentários temporários sem contexto suficiente para explicar o problema e a condição para resolvê-lo.

### Qualidade e revisão

- Preservar o comportamento existente fora do escopo aprovado e manter compatibilidade quando ela fizer parte dos requisitos.
- Evitar código morto, imports não utilizados, caminhos silenciosos de erro e exceções engolidas.
- Planejar verificações para os critérios de aceitação e para riscos introduzidos pela mudança.
- Revisar o diff final como um revisor humano: conferir nomes, fluxo, duplicação, complexidade, tratamento de erros, segurança dos dados e aderência à documentação.

### Violações e refatorações

- Ao encontrar código que viole estes padrões, informar o usuário em vez de iniciar uma refatoração não autorizada.
- Apresentar evidências concretas, explicar o impacto atual, os riscos de manter o código e o benefício esperado da refatoração.
- Propor um plano separado com escopo, áreas afetadas, estratégia para preservar comportamento, riscos e forma de verificação.
- Aguardar aprovação ou recusa explícita antes de implementar a refatoração.
- Se a violação impedir a implementação segura da feature atual, pausar somente a parte afetada e explicar o bloqueio. Se for independente, concluir o trabalho autorizado e registrar a proposta separadamente.
- Se a refatoração for recusada, preservar a decisão do usuário e não ampliar o escopo, sem introduzir novas violações no código criado ou alterado.
