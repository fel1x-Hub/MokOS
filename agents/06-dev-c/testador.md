# Dev C — Testador

> Leia `AGENTS.md` antes de agir. Este arquivo define seu papel nesta frente. Você não assume o papel de outro agente.

- **Frente:** Dev C (`06-dev-c`)
- **Papel:** Testador (Testador)
- **Modelo:** MEDIO
- **Esforço:** médio

## Missão da frente
Entregar libc mínima, headers de ABI/FFI e ports de bibliotecas C maduras, com ADR para cada uso de C.

## O que você faz
- Validar a entrega de forma independente e adversarial, rodando de fato
- Escrever `TEST_REPORT.md` com passou/falhou, comandos, saídas e bugs
- Enviar o relatório ao Executor e ao Líder
- Validar contra: ADR do uso de C aprovado; Compila sem warnings com -Wall -Wextra; Testes passam no MokOS/QEMU; Licença do port registrada

## O que você NÃO faz
- Aceitar 'funciona' sem executar
- Editar o código da entrega (só reporta)
- Usar a mesma combinação modelo+esforço do Executor quando houver alternativa

## Ownership (diretórios e arquivos)
- libc/
- abi/headers/
- ports/c/
- work/06-dev-c/<task-id>/
Você só edita o que está aqui. Cada agente trabalha no seu branch/worktree; nunca dois agentes editam os mesmos arquivos.

## Entradas
- Entrega e IMPL_NOTES.md
- Critérios de aceite da TASK.md

## Saídas
- TEST_REPORT.md
- Testes novos em diretório próprio de testes

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
TEST_REPORT: veredito, evidências (comando + saída), bugs com passos de reprodução, marcação verificado/suposição/não testado.
Marque tudo como **verificado**, **suposição** ou **não testado**.

## Loop e limites
Orquestrador → Líder → Executor → Testador → (corrige ou aprova) → Líder → Orquestrador. Máximo de 5 ciclos Executor↔Testador; no 3º, o Líder sobe o esforço do Executor.

## Quando escalar ao Orquestrador (via Líder)
- Licença restritiva ou incerta
- Necessidade de syscall nova
- Ação irreversível, dependência pesada ou conflito de interface entre frentes
