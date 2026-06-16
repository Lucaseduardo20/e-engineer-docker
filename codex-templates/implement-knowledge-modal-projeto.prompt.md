# Prompt para Implementação — Experiência de Knowledge do Projeto com Modal de Gestão

## Contexto da tarefa
O fluxo atual de conhecimentos aplicados no projeto está fraco do ponto de vista de experiência do usuário e não comunica bem o valor que as knowledge items trazem para o projeto.

A meta é transformar isso em uma experiência clara, útil e fácil de usar, com foco em mostrar valor logo de cara e reduzir atrito na gestão de knowledges do projeto.

## Objetivo
Criar uma experiência de gestão de knowledges do projeto que seja:
- muito mais visível;
- fácil de entender;
- fluida no uso;
- com valor percebido imediato;
- simples de manter e explorar.

## O que deve ser feito
1. Adicionar um botão bem visível na tela de detalhe do projeto para acessar a gestão de knowledges do projeto.
2. Ao clicar no botão, abrir uma modal (ou painel modal) com fluxo estruturado para gerenciar as knowledges do projeto.
3. Na própria tela do projeto, exibir um resumo claro e estratégico do conhecimento aplicado do projeto, para sinalizar valor sem sobrecarregar a tela principal.
4. O core da experiência de gestão deve ficar nesse fluxo/modal estruturado, com etapas e organização que facilitem a utilização.

## Direção de UX / valor para o usuário
A experiência precisa ser pensada para que o usuário perceba rapidamente:
- por que as knowledges importam;
- como elas ajudam o projeto;
- como ele pode usar esse recurso sem esforço.

A interface deve:
- parecer moderna, clara e de alto valor;
- destacar ação principal com um botão forte e visível;
- reduzir fricção e ruído técnico;
- guiar o usuário por etapas simples e intuitivas;
- apresentar o conteúdo de forma útil, não apenas como lista genérica.

## Regras de experiência esperadas
- O botão de gestão deve ser o ponto de entrada principal e visualmente evidente na tela do projeto.
- A modal deve ser o centro da experiência de conhecimento aplicado, não apenas um complemento secundário.
- A tela principal deve mostrar um resumo do conhecimento aplicado do projeto, mas sem duplicar todo o fluxo.
- O fluxo da modal deve ser estruturado e facilitado, com organização clara de etapas ou blocos de uso.
- A experiência deve ser simples e produtiva, evitando parecer “tela técnica” ou excessivamente burocrática.
- O usuário deve conseguir entender rapidamente o valor das knowledges e como explorá-las no contexto do projeto.

## Funcionalidades esperadas
No mínimo, a solução deve contemplar:
- botão de acesso visível e destacável;
- modal de gestão com fluxo organizado;
- visão resumida do conhecimento aplicado no projeto;
- possibilidade de visualizar, associar, criar ou gerenciar knowledges no contexto do projeto;
- navegação/organização clara do conteúdo dentro do modal;
- estados de vazio/ajuda que orientem o usuário quando ainda não houver knowledges;
- consistência visual com a plataforma.

## Critérios de valor e usabilidade
A implementação deve melhorar a experiência percebida do usuário. O Codex deve considerar:
- clareza da informação;
- facilidade de identificação da ação principal;
- redução de complexidade;
- organização visual do workflow;
- sensação de que o recurso realmente ajuda o projeto.

## Regras arquiteturais e de projeto
- Respeitar a arquitetura existente do frontend e do backend.
- Seguir os padrões e módulos já adotados no projeto.
- Não inventar soluções fora do modelo atual sem justificativa.
- Se for necessário criar ou ajustar endpoints, manter a mudança mínima e consistente com a arquitetura.
- Respeitar permissões, contexto do projeto e regras de negócio já existentes.

## Entrega esperada
Ao finalizar, o Codex deve:
1. explicar a proposta de UX e a abordagem adotada;
2. listar os arquivos que pretende criar/alterar;
3. implementar a melhoria com foco em usabilidade e clareza;
4. validar a solução com os cenários relevantes;
5. citar explicitamente os casos de teste executados ou considerados ao fim, para demonstrar que a tarefa foi concluída com validação.

## Observação importante
A prioridade aqui não é apenas “colocar um botão”. A prioridade é criar uma experiência que faça o usuário perceber valor real nas knowledges do projeto e que torne o uso desse recurso simples, intuitivo e útil no dia a dia.
