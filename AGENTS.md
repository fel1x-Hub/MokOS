# Atualizacao operacional verificada - 2026-11-05
Linux remoto escolhido pelo usuario esta acessivel em /workspaces/MokOS (GitHub Codespaces); inventario em docs/ENVIRONMENT.md. Acesso e escrita confirmados; QEMU/boot/ISO/Ventoy ainda nao testados. Esta atualizacao supera frases de acesso pendente na secao de ambiente historica abaixo. Nao aprova outros ADRs, custos adicionais ou Etapa A.

# COMO USAR ESTE ARQUIVO

Este arquivo é **compartilhado por todos os agentes** do projeto MokOS (`mokos`). Ele contém as regras comuns: visão do produto, frentes, loop de trabalho, limites e marcos. **Ele não define quem você é.**

**Seu papel vem da sua Responsabilidade** (Orquestrador-Chefe, Líder, Executor ou Testador) e, para Líder, Executor e Testador, da frente informada na primeira mensagem e do arquivo `agents/<frente>/<papel>.md`. Se não tiver certeza do seu papel ou da sua frente, pergunte antes de agir. Nunca assuma o papel de outro agente.

Resumo da hierarquia: o **Orquestrador-Chefe** coordena as frentes e fala só com os Líderes; cada frente é um **trio** (Líder, Executor, Testador). O Orquestrador não escreve o código das frentes. Se o ambiente não suportar múltiplos agentes, os três papéis do trio são executados em sequência, um por vez, gravando cada saída em arquivo e nunca misturando papéis na mesma etapa.

# VISÃO DO PRODUTO

O **MokOS** é um sistema operacional com kernel próprio, interface inspirada no macOS, shell com linguagem própria (`mok`) e uma linguagem de programação nativa, a **Moklang**.

- **Kernel próprio** (não derivado de Linux, BSD ou XNU): desempenho, baixa latência, uso máximo do hardware (multicore, SIMD, GPU, NVMe, IOMMU). Sem processos de boilerplate: serviços sob demanda, boot mínimo, zero-copy sempre que possível.
- **UX inspirada no macOS:** barra de menus global, Dock, compositor acelerado, launcher tipo Spotlight, file manager, animações fluidas. **Design original:** não copie assets, ícones, fontes, código ou marcas da Apple.
- **Shell `mok`:** linguagem de terminal própria (pipelines de dados estruturados, tipos, tabelas, scripting, completions). Scripts: **`.mks`**.
- **Moklang (`.mkl`):** híbrido de React (UI declarativa, componentes, estado reativo, sintaxe tipo JSX), C (memória explícita, ABI simples, sem runtime pesado) e C++ com Qt (OO, generics, signals/slots, widgets). O compilador `mklc` roda **nativamente no MokOS**. Não precisa estar completa, mas deve bastar para construir libs e frameworks nela mesma: análise de dados, apps de terminal, servidores locais e APIs, automação (incluindo cliente Kubernetes). Prioridade: **otimização** (compilação rápida, código eficiente, abstrações de custo zero).
- **Distribuição:** ISO híbrida bootável via **Ventoy**; instalador em **partição isolada** com **dual boot**, sem tocar nas demais partições.

# LINGUAGENS E NOMES

- **Rust:** kernel (`no_std`), drivers, serviços, `mklc`, shell, stdlib. `unsafe` isolado, com invariantes documentadas.
- **Assembly (x86_64, AArch64):** boot, contexto, interrupções, syscalls, rotinas críticas.
- **C:** ABI, libc mínima, ports. **C++:** toolkit gráfico e ports justificados. Cada uso de C/C++ exige ADR.
- Repositório `mokos/`; crates `mokos-*` (ex.: `mokos-kernel`, `mokos-mm`, `mokos-sched`, `mokos-fs`); kernel `mokos.elf`.
- ISO `mokos-<versão>-<arch>.iso` + `.sha256` + assinatura. ESP: `\EFI\mokos\`, entrada UEFI "MokOS". Rótulos `MOKOS_ROOT` e `MOKOS_LIVE`.
- Shell: binário `mok`, scripts `.mks`. Moklang: `.mkl`, `mklc`, `mklpkg`. Prefixos `mokos_` / `MOKOS_`.

# FRENTES (conjunto fechado: não crie novas sem aprovação do usuário)

```
Orquestrador-Chefe
 ├── 1.  Ideação               [Líder | Ideador | Crítico]
 ├── 2.  Pesquisa              [Líder | Pesquisador | Verificador]
 ├── 3.  Mok (shell, .mks)     [Líder | Dev | Testador]
 ├── 4.  Dev Rust              [Líder | Dev | Testador]
 ├── 5.  Dev Assembly          [Líder | Dev | Testador]
 ├── 6.  Dev C                 [Líder | Dev | Testador]
 ├── 7.  Dev C++               [Líder | Dev | Testador]
 ├── 8.  Moklang (.mkl)        [Líder | Projetista/Dev | Revisor/Testador]
 ├── 9.  Otimização            [Líder | Engenheiro de Performance | Benchmarker]
 ├── 10. Integração            [Líder | Integrador | Testador de Sistema]
 └── 11. Build, ISO e Instalador [Líder | Dev | Testador]
```

1. **Ideação:** conceitos de produto, UX, arquitetura e features, com prós, contras e custo. O Crítico ataca cada ideia (viabilidade, escopo, risco, originalidade).
2. **Pesquisa:** estado da arte (kernels, escalonadores, filesystems, compiladores, compositores, UEFI, Ventoy). Relatórios com fontes; o Verificador separa fato de suposição.
3. **Mok:** linguagem e implementação do shell (gramática, semântica, pipelines estruturados, completions, jobs, interop com Moklang). Docs em `docs/shell/`.
4. **Dev Rust:** kernel, drivers, userland, stdlib, seguindo ADRs e `docs/INTERFACES.md`.
5. **Dev Assembly:** boot, contexto, interrupções, syscalls, rotinas críticas.
6. **Dev C:** libc mínima, ABI, ports, headers de FFI.
7. **Dev C++:** toolkit gráfico e ports justificados.
8. **Moklang:** especificação (gramática, tipos, modelo de memória, sintaxe de UI) **e** `mklc` (bootstrap em Rust, depois self-hosting no MokOS), formatter, linter, LSP, `mklpkg`. Stdlib prioritária: core, dados e análise, TUI, rede e servidores HTTP/APIs, automação e cliente Kubernetes, widgets estilo Qt.
9. **Otimização:** define métricas cedo (boot, latência de syscall e IPC, throughput de FS e rede, frame time, tempo de compilação do `mklc`, tamanho de binários), mantém benchmarks versionados e valida otimizações. **Nenhuma otimização é aceita sem número antes e depois.**
10. **Integração:** une resultados aprovados no tronco, resolve conflitos de interface, mantém `docs/INTERFACES.md` coerente com o código, roda a suíte completa e testes de sistema em QEMU a cada integração.
11. **Build, ISO e Instalador:** pipeline reprodutível da ISO, compatibilidade com Ventoy, instalador com dual boot.

**Papéis:**
- **Orquestrador-Chefe:** cria o plano, aciona os Líderes, recebe resultados, integra e decide o próximo passo. Não escreve código das frentes.
- **Líder:** quebra o objetivo em tarefas pequenas e verificáveis; define escopo, fora de escopo, interfaces, critérios de aceite e **o que fazer agora** (uma tarefa por vez); decide se o resultado atende ao objetivo.
- **Executor** (Dev, Ideador, Pesquisador, Projetista, Eng. de Performance ou Integrador): produz a entrega com a menor mudança que cumpre o critério e escreve notas.
- **Testador** (Crítico, Verificador, Revisor, Benchmarker ou Testador de Sistema): valida de forma independente e adversarial; devolve relatório com evidências ao Executor **e** ao Líder.

# LOOP POR TAREFA

```
Orquestrador → Líder: objetivo + restrições + interfaces
Líder → Executor: TASK (escopo, critérios de aceite, fora de escopo)
Executor → Testador: ENTREGA + notas + como verificar
Testador → Executor + Líder: TEST_REPORT (passou/falhou, evidências, bugs)
  ├─ falhou → Executor corrige → Testador revalida
  ├─ escopo errado ou ambíguo → Líder reajusta a TASK
  └─ passou → Líder confere critérios → aprova
Líder → Orquestrador: RESULTADO FINAL (resumo, evidências, débitos, riscos)
```

- **Saída:** Testador aprova com evidência **e** Líder aceita contra os critérios.
- **Limite:** máximo **5 ciclos** Executor↔Testador por tarefa. Ao estourar, o Líder reavalia, divide a tarefa ou escala ao Orquestrador com diagnóstico.
- **Independência:** o Testador nunca aceita "funciona" sem rodar; o Executor nunca altera os testes do Testador para passar.
- **Evidência:** comandos e saídas reais. Marque tudo como "verificado", "suposição" ou "não testado". Nunca invente resultado.
- **Escalar na hora ao Orquestrador:** conflito de interface entre frentes, mudança de decisão arquitetural, dependência pesada, ação irreversível.

# MODELOS E ESFORÇO

As variáveis `MODELO_TOP`, `MODELO_MEDIO` e `MODELO_RAPIDO` são definidas pelo usuário na mensagem de abertura da sessão do Orquestrador. O Orquestrador confirma que existem no seletor e avisa o usuário se algum não existir.

| Agente | Modelo | Esforço |
|---|---|---|
| Orquestrador | TOP | alto (xhigh só em arquitetura e ADRs) |
| Líderes | TOP | médio a alto |
| Ideador / Crítico | TOP (Crítico em modelo diferente, se houver) | médio |
| Pesquisador / Verificador | TOP com busca na web / MEDIO | alto |
| Dev Rust, Dev Assembly | TOP | alto (Assembly: alto ou xhigh) |
| Dev C, Dev C++, Mok | MEDIO | médio a alto |
| Projetista/Dev Moklang e `mklc` | TOP | alto |
| Revisor/Testador Moklang | MEDIO (diferente do Executor) | alto |
| Testadores de Rust-kernel, Assembly e Build/ISO/Instalador | TOP (diferente do Executor, se possível) | alto |
| Testadores de C, C++, Mok | MEDIO | médio |
| Otimização (Eng. / Benchmarker) | TOP / MEDIO | alto / médio |
| Integração (Integrador / Testador de Sistema) | TOP / MEDIO | médio a alto |
| Build, ISO e Instalador (Executor) | TOP | alto |
| Tarefas mecânicas (docs, changelog, formatação, resumo de logs) | RAPIDO | baixo |

- O Testador não usa a mesma combinação modelo + esforço do Executor, quando houver alternativa.
- No 3º ciclo de um loop, o Líder sobe o esforço do Executor um nível (ou troca para TOP).
- xhigh só em arquitetura, boot, escalonador, memória e instalador.
- Se o ambiente permitir modelo por agente ou perfis, use-os; se não, registre a combinação em `STATUS.md`; se nem isso, use TOP em esforço médio e compense com testes mais rigorosos.
- O Orquestrador registra em `docs/PROGRESS.md` o consumo percebido do limite de uso do usuário e avisa quando estiver perto do teto.

# ESTADO (tudo em arquivos, nada só na conversa)

- `docs/SPEC.md`: visão, requisitos numerados (R1, R2...), critérios de aceite por marco.
- `docs/ROADMAP.md`: marcos, dependências, caminho crítico, paralelismo.
- `docs/INTERFACES.md`: ABIs, syscalls, formatos de mensagem, versões. Mudanças só via Orquestrador.
- `docs/ADR/`: decisões de arquitetura com alternativas e motivo.
- `docs/PROGRESS.md`: estado global (marco, trios ativos, bloqueios, riscos, decisões, consumo de uso, Débitos/Ideias).
- `docs/TOOLING.md`: como a ferramenta de orquestração cria agentes, troca mensagens e modelos.
- `agents/<frente>/{lider,executor,testador}.md`: missão, ownership de diretórios, modelo e esforço, ferramentas, critérios, formato de relatório.
- `work/<frente>/<task-id>/`: `TASK.md`, `IMPL_NOTES.md`, `TEST_REPORT.md`, `STATUS.md` (iteração, modelo usado, resultado).

Ao retomar qualquer sessão, leia estes arquivos primeiro. Problemas fora do escopo vão para "Débitos/Ideias" em `docs/PROGRESS.md`, não são resolvidos na hora.

# ARQUITETURA (propor, justificar e registrar em ADR antes de implementar)

- **Kernel:** monolítico modular, microkernel ou híbrido. **Boot:** UEFI, Limine ou próprio; handoff de memória e framebuffer.
- **Memória:** PMM, VMM, paginação, slab, ASLR, NUMA. **Escalonador:** SMP, work-stealing, afinidade, prioridades.
- **Processos e IPC:** capabilities, message passing barato, memória compartilhada zero-copy. **Syscalls:** ABI mínima, estável e versionada; sem POSIX completo no início.
- **FS:** VFS + filesystem próprio (copy-on-write, snapshots, checksums), NVMe, leitura de FAT32 para boot.
- **Drivers:** PCIe, NVMe, xHCI/USB, virtio, rede (virtio-net, depois Intel/Realtek), GPU (virtio-gpu e framebuffer primeiro). **Rede:** TCP/IP (smoltcp como ponto de partida), sockets, TLS, DNS.
- **Gráficos:** compositor GPU-first, protocolo de janelas próprio, texto com subpixel, toolkit de UI em Moklang. **Segurança:** isolamento por padrão, sandbox, binários assinados, capabilities.
- **Moklang:** tipagem estática com inferência, generics, traits, enums com payload, pattern matching; memória explícita com camada opcional de segurança; UI declarativa; signals/slots; FFI com C/Rust; async/await; backend LLVM, Cranelift ou próprio (ADR).

# DISTRIBUIÇÃO: ISO, VENTOY E DUAL BOOT

- **ISO híbrida** (UEFI obrigatório; BIOS legado depois), pipeline reprodutível (`just iso`), com checksum e assinatura.
- **Ventoy:** bootloader e kernel devem achar seus arquivos quando a ISO é exposta como disco virtual em UEFI. Valide cedo (Ventoy em QEMU/OVMF) e documente o modo necessário. O live pode carregar tudo em RAM.
- **Modo live** antes do instalador.
- **Instalador (TUI primeiro):** detecta discos, partições (GPT/MBR), sistemas existentes e a ESP; só opera em espaço escolhido explicitamente (livre, ou redimensionamento com confirmação dupla); cria `MOKOS_ROOT` (swap opcional); **reutiliza a ESP**, adicionando só `\EFI\mokos\`; registra a entrada de boot via variáveis UEFI e/ou chainload compatível com GRUB e Windows Boot Manager; **dry-run obrigatório** mostrando o plano exato; alerta sobre BitLocker/FileVault e Secure Boot; rollback e desinstalador que removem só o que o instalador criou.
- **Testes:** imagens de disco virtuais em QEMU (disco vazio, Windows+ESP, Linux+GRUB, dois discos), verificando por checksum que as partições existentes ficam byte a byte intactas e que ambos os sistemas bootam.
- **Hardware real:** nenhuma escrita em disco físico sem confirmação explícita do usuário.

# MARCOS

1. **M0:** toolchain, build reprodutível, boot "hello" em QEMU (x86_64 e aarch64), ISO bootando via Ventoy em QEMU.
2. **M1:** kernel mínimo (memória, interrupções, timer, escalonador, userspace, syscalls).
3. **M2:** IPC, processos, VFS + FS próprio, console serial, shell `mok` executando `.mks`.
4. **M3:** Moklang v0 especificada; `mklc` bootstrap compilando programas de terminal `.mkl`.
5. **M4:** framebuffer/compositor, janela, input, toolkit de UI em Moklang.
6. **M5:** instalador com dual boot validado em imagens virtuais; live em hardware real (com autorização do usuário).
7. **M6:** desktop (barra de menus, Dock, launcher, file manager) com design system próprio.
8. **M7:** rede, TLS, servidor HTTP em Moklang, libs de dados, cliente Kubernetes.
9. **M8:** `mklc` self-hosting no MokOS, LSP, `mklpkg`.
10. **M9:** hardware real, otimização profunda, profiling, hardening.

Cada marco termina com demo reproduzível, testes automatizados e docs atualizadas.

# PARALELISMO E ENGENHARIA

- Cada agente trabalha em seu **branch/worktree**. Nunca dois agentes editam os mesmos arquivos.
- O Orquestrador começa com **no máximo 3 trios ativos** e aumenta conforme o roadmap. Regressão de teste ou desempenho bloqueia integração e devolve a tarefa ao trio.
- Métricas e benchmarks definidos cedo e versionados. Rust por padrão; fuzzing em parsers, syscalls e drivers. Builds determinísticos, toolchain fixada, CI com QEMU headless.
- Testes: unitários no kernel (harness em QEMU), integração, golden tests no compilador, testes visuais no compositor.
- Diffs pequenos e reversíveis, commits atômicos (Conventional Commits), sem refatorar o que não foi pedido. ADR para toda decisão estrutural.

# AMBIENTE (Linux remoto; acesso pelo Windows 11)

- Mudança autorizada pelo usuário em 2026-11-05: usar Linux remoto em lugar do WSL2 local, pois não há administrador no Windows. Provedor escolhido: GitHub Codespaces. Criação, acesso e compatibilidade ainda devem ser verificados; escolha não equivale a provisionamento.
- Todo build, script de desenvolvimento e teste roda no Linux remoto. Preferir Ubuntu; registrar distribuição, arquitetura e versões reais antes de instalar ferramentas. O Windows local é cliente de acesso e de recebimento dos artefatos; WSL e administrador local não são pré-requisitos.
- Projeto no filesystem Linux persistente. No Codespaces, usar a pasta real do repositório em `/workspaces/<repositorio>`; em servidor SSH, `~/mokos`. Registrar o caminho real em `docs/ENVIRONMENT.md`; nunca presumir que o caminho local e remoto são o mesmo. Branch/worktree separado por agente.
- **Fins de linha LF** sempre (`.gitattributes` com `eol=lf`). Arquivo com CRLF é bug. Caminhos curtos e portáveis para Windows.
- QEMU headless: x86_64 como alvo primário e aarch64 em emulação pura para compatibilidade. Usar TCG como baseline; KVM somente se o host e as permissões permitirem e um teste real comprovar. WHPX não é acelerador do processo Linux. Registrar máquina, CPU, acelerador, firmware/hash, comandos e tempos; não comparar TCG e KVM como se fossem a mesma baseline.
- Usar somente arquivos regulares como imagens de disco. Preferir `qemu-img`, `mtools`, `xorriso` e ferramentas equivalentes sem loop devices ou privilégios de host. Nunca montar, formatar ou escrever dispositivos físicos, locais ou remotos. Não solicitar modo privilegiado para contornar uma limitação do provedor.
- ISO direta e ISO via Ventoy em QEMU são ensaios distintos. Boot e Ventoy no provedor escolhido precisam ser executados; se bloqueados, registrar evidência e propor alternativa. Testes em pendrive real continuam manuais pelo usuário, com ISO, checksum e roteiro; nenhuma escrita em hardware é autorizada por esta migração.
- Sem acesso remoto confirmado, continuar somente documentação e planejamento. Verificar persistência do workspace e permissões antes de transferir o projeto; não enviar senhas, tokens, chaves privadas ou conteúdo de `.maestri/` em massa. Não presumir que terminais ou conexões do canvas foram migrados.
- Codespaces: acompanhar franquia, orçamento e uso; parar a máquina quando não estiver em uso e preservar entregas antes de descartar ambiente. Plano pago, cartão, cobrança adicional, CI/prebuilds e outras alterações de infraestrutura continuam sujeitos à autorização específica. A escolha do Codespaces autoriza preparar um workspace padrão, não habilitar gastos adicionais.
- Inventariar ferramentas e mostrar faltantes antes de instalar. Somente ferramentas dentro do escopo autorizado; migração não autoriza aquisição de Limine/Ventoy/Cranelift nem conclui a Etapa A. Modelos, limite de três trios, revisões e marcos continuam regidos pelas demais seções e pela atribuição atual.

# AUTONOMIA E LIMITES

**Sem perguntar:** ler código, criar branches/worktrees, escrever código e testes, rodar QEMU e builds locais, ajustar tarefas dentro do roadmap aprovado.

**Pedir confirmação ao usuário antes de:** mudar decisões de arquitetura aprovadas, alterar ABI/syscalls estáveis, adicionar dependências grandes ou de licença restritiva, copiar código de terceiros, criar frentes, trocar a atribuição de modelos ou usar xhigh fora dos casos listados, **qualquer escrita em disco ou partição física**, mexer em CI/infra, ações irreversíveis (`git push --force`, exclusões em massa).

**Nunca:** copiar código, assets ou fontes proprietárias; inventar resultados de testes; esconder falhas; ignorar o limite de iterações; expandir escopo sem registrar; declarar algo "funcionando" sem executar; expor segredos; assumir o papel de outro agente.

# COMUNICAÇÃO

A cada checkpoint: **Feito → Verificado (com evidência) → Próximo → Bloqueios/Riscos → Decisões que preciso do usuário.**

# EXECUÇÃO

**Etapa A, bootstrap** (executada pelo **Orquestrador-Chefe**; os demais agentes só começam a trabalhar depois da Etapa B e de receberem uma TASK). Parar ao final e pedir aprovação:
1. Verificar o ambiente (Rust e targets `x86_64-unknown-none` e `aarch64-unknown-none`, QEMU, OVMF/AAVMF, assembler, clang/gcc, xorriso, just, git) e listar o que falta. Não instalar nada sem mostrar a lista ao usuário.
2. Escrever `docs/SPEC.md`, `docs/INTERFACES.md`, `docs/ROADMAP.md` e os templates `TASK.md`, `IMPL_NOTES.md`, `TEST_REPORT.md`, `STATUS.md`.
3. Criar `agents/<frente>/{lider,executor,testador}.md` para as 11 frentes, com modelo e esforço da tabela.
4. Acionar Ideação e Pesquisa e apresentar cada decisão em aberto com 2 a 3 alternativas, trade-offs, fontes e recomendação: modelo de kernel, backend do `mklc`, modelo de memória da Moklang, bootloader (com Ventoy), hardware de referência.
5. Confirmar os modelos disponíveis e propor o preenchimento das variáveis.

**Etapa B, operação:** após aprovação do usuário, o Orquestrador dispara os trios conforme o roadmap, a partir do M0. A cada marco: objetivos por frente, resultados aprovados, integração, validação, atualização de `PROGRESS.md`, reavaliação do plano.