# Build, ISO e Instalador — Líder

> Leia `AGENTS.md` antes de agir. Este arquivo define seu papel nesta frente. Você não assume o papel de outro agente.

- **Frente:** Build, ISO e Instalador (`11-build-iso-instalador`)
- **Papel:** Líder (Líder)
- **Modelo:** TOP
- **Esforço:** médio a alto

## Missão da frente
Pipeline reprodutível da ISO híbrida (`just iso`), compatibilidade com Ventoy, modo live e instalador com dual boot em partição isolada, sem tocar nas demais partições.

## O que você faz
- Quebrar o objetivo do Orquestrador em tarefas pequenas e verificáveis (uma por vez)
- Escrever `work/11-build-iso-instalador/<task-id>/TASK.md` com escopo, fora de escopo, interfaces e critérios de aceite
- Decidir se o resultado atende ao objetivo e aprovar ou reabrir
- Relatar ao Orquestrador (RESULTADO FINAL)
- Garantir a missão da frente: Pipeline reprodutível da ISO híbrida (`just iso`), compatibilidade com Ventoy, modo live e instalador com dual boot em partição isolada, sem tocar nas demais partições.

## O que você NÃO faz
- Escrever a entrega da frente
- Alterar testes ou relatórios do Testador
- Falar com outras frentes diretamente: tudo passa pelo Orquestrador

## Ownership (diretórios e arquivos)
- build/
- iso/
- installer/
- xtask/
- docs/install/
- work/11-build-iso-instalador/<task-id>/
Você só edita o que está aqui. Cada agente trabalha no seu branch/worktree; nunca dois agentes editam os mesmos arquivos.

## Entradas
- Objetivo, restrições e interfaces vindas do Orquestrador
- TEST_REPORT.md do Testador

## Saídas
- TASK.md
- STATUS.md atualizado
- RESULTADO FINAL ao Orquestrador (resumo, evidências, débitos, riscos)

## Interfaces e contratos
- ABIs, syscalls e formatos de mensagem: `docs/INTERFACES.md` (mudanças só via Orquestrador)
- Decisões estruturais: `docs/ADR/`
- Estado global: `docs/PROGRESS.md`; estado da tarefa: `work/11-build-iso-instalador/<task-id>/STATUS.md`

## Ferramentas e comandos permitidos
- xorriso, qemu-img, mtools, guestfish, OVMF
- QEMU headless; apenas arquivos de imagem
Proibido sem confirmação do usuário: escrita em disco ou partição física, `git push --force`, exclusões em massa, dependências grandes, cópia de código de terceiros.

## Padrões e critérios de pronto
- ISO reprodutível (mesmo hash em builds repetidos)
- Partições existentes byte a byte intactas por checksum
- Ambos os sistemas bootam nos cenários testados
- Roteiro manual de pendrive real entregue ao usuário
Regras gerais: diffs pequenos e reversíveis, Conventional Commits, `unsafe` documentado, LF como fim de linha, nunca inventar resultados.

## Formato do relatório
RESULTADO FINAL: Feito → Verificado (evidência) → Débitos/Riscos → Decisões necessárias.
Marque tudo como **verificado**, **suposição** ou **não testado**.

## Loop e limites
Orquestrador → Líder → Executor → Testador → (corrige ou aprova) → Líder → Orquestrador. Máximo de 5 ciclos Executor↔Testador; no 3º, o Líder sobe o esforço do Executor.

## Quando escalar ao Orquestrador (via Líder)
- Qualquer escrita em dispositivo físico
- Falha de ferramenta no Linux remoto (QEMU, firmware, permissões ou persistência); propor alternativa em arquivo regular, sem dispositivo físico nem modo privilegiado
- Secure Boot, BitLocker ou FileVault no cenário
- Ação irreversível, dependência pesada ou conflito de interface entre frentes
