Atualizacao 2026-11-05: escrita e inventario reais confirmados em /workspaces/MokOS, Ubuntu 24.04.5 x86_64. Adequacao operacional a QEMU/boot/ISO/Ventoy permanece nao testada; Etapa A parcial.

# MokOS — especificação inicial
Estado: proposta preparada, não integrada. Requisitos do usuário verificados por leitura; implementação não testada.

## Produto
Sistema operacional de kernel próprio, UX original inspirada no macOS, shell mok (.mks), linguagem Moklang (.mkl), compilador mklc nativo e distribuição live/instalador com dual boot. Rust é padrão; assembly só na camada de arquitetura. Uso de C/C++ exige ADR. Não copiar assets nem código de terceiros.

## Requisitos
- R1: kernel independente de Linux/BSD/XNU; unsafe isolado e invariantes documentadas.
- R2: M0 demonstra hello em x86_64 e aarch64 sob QEMU, com comandos reproduzíveis e logs reais.
- R3: build com toolchain fixada, entradas documentadas e duas execuções limpas com hashes idênticos dos artefatos determinísticos.
- R4: ISO UEFI mokos-<versão>-<arch>.iso, checksum SHA256 e assinatura; pipeline just iso; M0 inclui boot via Ventoy em QEMU.
- R5: Linux remoto GitHub Codespaces autorizado e acessivel em /workspaces/MokOS; Ubuntu 24.04.5 x86_64. Windows somente cliente. QEMU headless TCG baseline; aarch64 emulacao pura; KVM somente apos teste real. Inventario atual em ENVIRONMENT.md; boot MokOS nao testado.
- R6: nenhuma escrita em dispositivo físico; imagens virtuais regulares são permitidas. Instalador fora desta sessão.
- R7: arquitetura registrada antes da implementação; decisões noturnas provisórias, com alternativas, custo de reversão e plano de retorno.
- R8: entregas independentes por Executor/Testador, aprovação do Líder e passagem pela Integração antes do tronco.
- R9: no máximo três trios ativos; até cinco ciclos por tarefa, reavaliar na terceira falha idêntica; nenhum agente xhigh/Astra.
- R10: não alterar ABI estável, dependências grandes/restritivas, CI/infra ou adquirir terceiros fora da autorização.

## Aceite da Etapa A
Inventário real dentro do Linux remoto; documentos SPEC/INTERFACES/ROADMAP e templates; 33 perfis das 11 frentes; catálogo de modelos confirmado ou limitação explicitada; recomendações de Ideação e Pesquisa com revisão independente e ADRs provisórios.
Estado atual: ferramentas e inventario concluidos; revisao focal final pendente. Ver PROGRESS.md para aceite A; historico anterior de acesso nao e bloqueio atual.

## Aceite de M0
1. Toolchain e versões/targets registrados.
2. Builds limpos repetidos: hashes, comandos e resultados reais.
3. Hello x86_64 em QEMU e tempo de boot; acelerador real registrado.
4. Hello aarch64 em QEMU TCG e tempo de boot.
5. ISO UEFI em QEMU; depois ISO via Ventoy em imagem virtual existente/autorizada, com logs e comandos.
6. Testador independente aprova; Integração reexecuta; docs e demo atualizadas.
Nenhum destes testes foi executado. ISO direta não comprova Ventoy. Aplicativo UEFI que imprime hello não comprova kernel após ExitBootServices; a fronteira deve ser definida no ADR de boot.

## Critérios documentais dos marcos futuros — rascunho, sem trabalho autorizado nesta noite
Os critérios abaixo rastreiam a visão de AGENTS.md e serão refinados com interfaces/testes antes de cada marco. Não foram executados.
- M1: memória, interrupções, timer, escalonador e userspace executam demo com syscalls mínimas versionadas, logs e teste independente QEMU.
- M2: dois processos demonstram IPC e operações VFS/FS; mok executa .mks com resultado reproduzível.
- M3: especificação Moklang v0 aprovada e mklc bootstrap compila exemplos de terminal com golden tests.
- M4: compositor/framebuffer, janela e input demonstrados; toolkit UI Moklang com critério visual reproduzível.
- M5: live e instalador com dry-run, reutilização restrita de ESP, rollback/desinstalação; imagens vazias/Windows/Linux/dois discos preservadas byte a byte fora da área autorizada; hardware real depende de permissão própria.
- M6: menu global, Dock, launcher e file manager com design original e testes de navegação.
- M7: rede/TLS/HTTP e bibliotecas de dados/automação/Kubernetes demonstradas por testes definidos antes do marco; dependências sujeitas a autorização.
- M8: mklc recompila a si no MokOS, com LSP e mklpkg demonstrados e bootstrap reproduzível.
- M9: hardware autorizado, profiling e hardening; otimizações exigem medições antes/depois e testes de regressão.
Fonte normativa completa: AGENTS.md da raiz, incluindo segurança/capabilities, stdlib, distribuição e proteção de dados. Não há compromisso público de ABI nesta especificação inicial.
