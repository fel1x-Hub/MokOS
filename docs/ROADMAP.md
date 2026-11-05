Atualizacao 2026-11-05: acesso Codespaces, importacao documental e inventario remoto A0 executados; ferramentas faltantes em ENVIRONMENT.md. Etapa A parcial e nenhum trabalho M0 executado.

# Roadmap da noite
Estado: plano; execução limitada ao M0. Não iniciar M1.

## Caminho crítico
A0 acesso Linux remoto, inventário e documentação → A1 recomendações Ideação/Pesquisa e revisão → A2 ADRs provisórios → B0 ambiente remoto/Git/toolchain → B1 boot x86_64 → B2 boot aarch64 → B3 ISO direta → B4 Ventoy em QEMU → I0 integração e relatório.

## Escalonamento dos trios existentes
- Janela A: Ideação + Pesquisa; terceiro espaço reservado a revisão documental da Integração.
- Após A: Rust + Assembly + Build, somente tarefas com contratos de ownership separados.
- Ao concluir um trio: parar, depois ativar Integração sem ultrapassar três ativos.
- Nenhuma tarefa para Mok/C/C++/Moklang/Otimização esta noite além de decisões documentais necessárias ao M0.

## Tarefas e critérios
- A0: provisionar workspace padrão GitHub Codespaces escolhido pelo usuário, confirmar acesso e persistência, levantar versões e targets dentro do Linux remoto, integrar docs/templates e conferir os 33 perfis. Sem CI/prebuilds ou gasto adicional autorizado.
- A1: cinco decisões, cada uma com 2–3 opções, fontes, recomendação e avaliação independente.
- A2: ADRs provisórios; opções caras de reverter ficam pendentes e não recebem implementação.
- B0: ferramentas autorizadas apenas por gerenciador oficial/rustup, registro de instalação e versões fixadas; branches/worktrees separados.
- B1/B2: hello verificável por serial/log, timeout e tempo medido; Testador executa independentemente.
- B3/B4: duas gerações limpas reproduzíveis, ISO e checksum; Ventoy só com artefato permitido já disponível. Não adquirir Ventoy sem autorização.
- I0: Testador aprova antes do integrador; no tronco somente após revisão e suíte de sistema executada.

## Bloqueios atuais
Atualizado em 2026-11-05: usuário não dispõe de administrador local e autorizou substituir WSL por Linux remoto; escolheu GitHub Codespaces. Navegador, acesso, escrita e inventário foram confirmados; ferramentas instaladas. Ver ENVIRONMENT.md e PROGRESS.md atuais. A raiz Windows continua somente leitura; desenvolvimento autorizado no repositório Git do Codespaces. Pacote já publicado na branch do PR #1; integração ao tronco depende dos aceites. Não reinstalar o bloqueio WSL como requisito. Etapa A segue parcial; nenhum código de kernel, compilador ou instalador antes da aprovação exigida na atribuição atual.

## Marcos futuros, fora do escopo da noite
M1 memória/interrupções/timer/escalonador/userspace; M2 IPC/VFS/shell; M3 mklc inicial; M4 UI; M5 instalador; M6 desktop; M7 rede; M8 self-hosting; M9 hardware/performance.

## Adendo — gates e evidência
Origem da liberação A→B: docs/NIGHT-AUTHORIZATION.md, item 1 do usuário. Gate técnico A ainda incompleto; não houve passagem B por simples inferência de autorização. Cinco decisões: kernel ADR 0001, backend mklc 0002, memória Moklang 0003, bootloader/Ventoy 0004 e hardware de referência 0005; críticas/resultados em PROGRESS.
B3/B4 exigem just iso, ISO híbrida, checksum SHA256 e assinatura conforme SPEC R4. Assinatura não produzida; ferramentas e política de chaves não definidas. Não instalar ferramentas adicionais sem autorização. Nenhuma aquisição de dependência/bootloader é inferida da escolha documental de candidato.
