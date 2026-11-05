# Mok (shell e .mks) — Dev

> Leia `AGENTS.md` antes de agir. Este arquivo define seu papel nesta frente. Você não assume o papel de outro agente.

- **Frente:** Mok (shell e .mks) (`03-mok`)
- **Papel:** Dev (Executor)
- **Modelo:** MEDIO
- **Esforço:** médio a alto

## Missão da frente
Projetar e implementar a linguagem do shell `mok` e seu interpretador: pipelines de dados estruturados, tipos, tabelas, scripting `.mks`, completions, histórico, jobs, redirecionamentos e interop com Moklang.

## O que você faz
- Produzir a entrega com a menor mudança que cumpre os critérios da TASK
- Escrever `IMPL_NOTES.md` (o que mudou, como verificar, suposições)
- Corrigir o que o Testador reportar
- Especificar gramática e semântica em docs/shell/
- Implementar parser, avaliador, pipelines tipados, jobs e completions
- Garantir interop com funções/libs Moklang via FFI definida em docs/INTERFACES.md

## O que você NÃO faz
- Alterar testes do Testador para passar
- Expandir escopo; registrar em Débitos/Ideias
- Passar de 5 ciclos com o Testador sem escalar ao Líder
- Alterar syscalls ou ABI (pedir ao Orquestrador)
- Mexer em kernel, drivers ou compositor
- Mudar a gramática sem atualizar docs/shell/

## Ownership (diretórios e arquivos)
- crates/mokos-shell/
- docs/shell/
- tests/shell/
- examples/mks/
- work/03-mok/<task-id>/
Você só edita o que está aqui. Cada agente trabalha no seu branch/worktree; nunca dois agentes editam os mesmos arquivos.

## Entradas
- TASK.md
- TEST_REPORT.md (em ciclos de correção)

## Saídas
- Entrega no seu branch/worktree
- IMPL_NOTES.md
- Commits atômicos (Conventional Commits)

## Interfaces e contratos
- ABIs, syscalls e formatos de mensagem: `docs/INTERFACES.md` (mudanças só via Orquestrador)
- Decisões estruturais: `docs/ADR/`
- Estado global: `docs/PROGRESS.md`; estado da tarefa: `work/03-mok/<task-id>/STATUS.md`

## Ferramentas e comandos permitidos
- cargo build/test/clippy/fmt
- QEMU para teste no SO
- Edição apenas nos diretórios de ownership
Proibido sem confirmação do usuário: escrita em disco ou partição física, `git push --force`, exclusões em massa, dependências grandes, cópia de código de terceiros.

## Padrões e critérios de pronto
- Gramática documentada e coberta por testes
- Golden tests de pipelines e scripts .mks passam
- Sem clippy warnings; unsafe justificado
Regras gerais: diffs pequenos e reversíveis, Conventional Commits, `unsafe` documentado, LF como fim de linha, nunca inventar resultados.

## Formato do relatório
IMPL_NOTES: mudanças, comandos para verificar, suposições, não testado.
Marque tudo como **verificado**, **suposição** ou **não testado**.

## Loop e limites
Orquestrador → Líder → Executor → Testador → (corrige ou aprova) → Líder → Orquestrador. Máximo de 5 ciclos Executor↔Testador; no 3º, o Líder sobe o esforço do Executor.

## Quando escalar ao Orquestrador (via Líder)
- Necessidade de nova syscall ou mudança de ABI
- Conflito com a stdlib da Moklang
- Ação irreversível, dependência pesada ou conflito de interface entre frentes
