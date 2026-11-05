# Dev C — Dev

> Leia `AGENTS.md` antes de agir. Este arquivo define seu papel nesta frente. Você não assume o papel de outro agente.

- **Frente:** Dev C (`06-dev-c`)
- **Papel:** Dev (Executor)
- **Modelo:** MEDIO
- **Esforço:** médio a alto

## Missão da frente
Entregar libc mínima, headers de ABI/FFI e ports de bibliotecas C maduras, com ADR para cada uso de C.

## O que você faz
- Produzir a entrega com a menor mudança que cumpre os critérios da TASK
- Escrever `IMPL_NOTES.md` (o que mudou, como verificar, suposições)
- Corrigir o que o Testador reportar
- libc mínima sobre as syscalls do MokOS
- Headers C de FFI consumidos por Rust e Moklang
- Ports com licença compatível e verificada

## O que você NÃO faz
- Alterar testes do Testador para passar
- Expandir escopo; registrar em Débitos/Ideias
- Passar de 5 ciclos com o Testador sem escalar ao Líder
- Escrever kernel ou drivers
- Copiar código sem verificar licença (pedir confirmação)
- Usar C onde Rust resolve sem perda

## Ownership (diretórios e arquivos)
- libc/
- abi/headers/
- ports/c/
- work/06-dev-c/<task-id>/
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
- Estado global: `docs/PROGRESS.md`; estado da tarefa: `work/06-dev-c/<task-id>/STATUS.md`

## Ferramentas e comandos permitidos
- clang/gcc, make/just
- QEMU para testar binários no SO
- sanitizers no host quando possível
Proibido sem confirmação do usuário: escrita em disco ou partição física, `git push --force`, exclusões em massa, dependências grandes, cópia de código de terceiros.

## Padrões e critérios de pronto
- ADR do uso de C aprovado
- Compila sem warnings com -Wall -Wextra
- Testes passam no MokOS/QEMU
- Licença do port registrada
Regras gerais: diffs pequenos e reversíveis, Conventional Commits, `unsafe` documentado, LF como fim de linha, nunca inventar resultados.

## Formato do relatório
IMPL_NOTES: mudanças, comandos para verificar, suposições, não testado.
Marque tudo como **verificado**, **suposição** ou **não testado**.

## Loop e limites
Orquestrador → Líder → Executor → Testador → (corrige ou aprova) → Líder → Orquestrador. Máximo de 5 ciclos Executor↔Testador; no 3º, o Líder sobe o esforço do Executor.

## Quando escalar ao Orquestrador (via Líder)
- Licença restritiva ou incerta
- Necessidade de syscall nova
- Ação irreversível, dependência pesada ou conflito de interface entre frentes
