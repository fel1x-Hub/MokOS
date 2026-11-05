# A-SOURCES — alternativas documentais

Data de consulta: 2026-11-04. Estado: provisório, não integrado, ciclo 1; aguardando revisão independente. Autor: Pesquisa · Pesquisador.

## Como ler

**VD — verificado documentalmente:** a fonte primária consultada sustenta a afirmação; não significa execução local. **S — suposição:** avaliação, proposta ou inferência para MokOS. **NT — não testado:** resultado operacional ainda sem execução. Todas as vantagens, custos e recomendações para MokOS abaixo são S, mesmo quando apoiadas em fatos VD. Nenhuma alternativa é uma decisão arquitetural aprovada. As fontes são exemplos de mecanismos, sem importar código ou derivar o kernel desses projetos.

## 1. Modelo de kernel

| Alternativa | Base documental | Vantagens propostas (S) | Custos e limitações (S) |
|---|---|---|---|
| Monolítico modular, inicialmente com módulos ligados estaticamente | VD K1: Linux documenta módulos internos e externos. Isso comprova a existência do mecanismo de modularidade, não isolamento entre módulos. | Menos infraestrutura inicial de IPC e servidores; caminho curto até M1. Separar subsistemas em Rust permite experimentar fronteiras internas. | Falha de driver em modo kernel pode comprometer o núcleo; modularidade de código não equivale a isolamento. Migrar depois um serviço para userspace exige revisão de ownership e comunicação. |
| Microkernel próprio com serviços em userspace | VD K2: seL4 é um microkernel com verificação formal. As garantias desse projeto não se transferem a MokOS. | Fronteiras explícitas facilitariam isolamento e substituição de serviços. | Exige IPC, política de capabilities e bootstrap de servidores cedo; overhead e esforço dependem da implementação, sem números MokOS. |

Fontes primárias: [K1 — Linux, Building External Modules](https://docs.kernel.org/kbuild/modules.html); [K2 — seL4, What is seL4?](https://sel4.systems/About/).

**Recomendação (S):** menor compromisso inicial: monolítico modular mínimo, sem loader dinâmico de módulos e com dependências internas explícitas. É uma hipótese de menor custo de reversão, não promessa de conversão barata para microkernel. **Incertezas:** prioridades de isolamento, contratos IPC e tamanho da equipe podem inverter a preferência. **NT:** latência, robustez e esforço real de ambas as opções.

## 2. Backend do mklc

| Alternativa | Base documental | Vantagens propostas (S) | Custos e limitações (S) |
|---|---|---|---|
| LLVM AOT | VD B1: documentação descreve geração de código independente de alvo e infraestrutura de otimização. | Opção forte para explorar otimizações e múltiplos alvos sem criar gerador de máquina próprio. | Integração, build e futuro porte do compilador nativo ao MokOS podem aumentar custo; biblioteca não resolve linker, syscalls ou stdlib do novo SO. |
| Cranelift AOT | VD B2: backend escrito em Rust, usado em AOT/JIT e com suporte a x86-64 e aarch64. O projeto prioriza rapidez de compilação e declara otimização menos agressiva que LLVM. | Alinhamento com bootstrap em Rust e iteração rápida do frontend. | Pode limitar otimizações desejadas; suporte à ISA não significa suporte automático ao MokOS nem self-hosting pronto. |

Fontes primárias: [B1 — LLVM Code Generator](https://llvm.org/docs/CodeGenerator.html); [B2 — Cranelift](https://cranelift.dev/).

**Recomendação (S):** protótipo AOT com Cranelift, mantendo a representação tipada e a semântica de memória fora da API específica do backend. Isso reduz acoplamento para uma futura comparação com LLVM; não define interface pública agora. **Incertezas:** tamanho do port nativo, TLS, unwind, objetos e debug precisam de avaliação futura; priorizar código final sobre tempo de compilação pode favorecer LLVM. **NT:** compilação, desempenho, tamanho de binários e execução em ambas as arquiteturas; nenhum ganho numérico é alegado.

## 3. Memória da Moklang

| Alternativa | Base documental | Vantagens propostas (S) | Custos e limitações (S) |
|---|---|---|---|
| Alocação/liberação explícita com arenas e destruição por escopo | VD M1: o livro Rust distingue gestão manual, coleta e ownership. VD M2: FFI requer explicitar responsabilidades de segurança e recursos. Arenas aqui são proposta própria. | Núcleo sem coletor obrigatório e fronteiras de alocação visíveis; implementação inicial limitada. | Uso após liberação e dupla liberação precisam de disciplina; arenas não servem automaticamente a objetos com vidas independentes. Segurança opcional não fica resolvida por esta escolha. |
| Ownership e empréstimos estáticos | VD M1: Rust verifica regras de ownership em compilação. | Pode impedir classes de erros sem coletor obrigatório. | Análise de empréstimos, diagnósticos e integração com estado reativo/FFI ampliam o compilador; copiar a ambição de Rust não entrega suas garantias. |
| Contagem de referências opt-in para grafos de UI | VD M3: Rc compartilha ownership, é de uma thread e ciclos fortes não são liberados; Weak permite quebrar ciclos. Arc atende compartilhamento atômico entre threads. | Ergonomia para componentes e callbacks, sem impor a estratégia ao kernel e a todos os valores. | Contagem tem trabalho em execução; ciclos exigem estratégia e destruição pode produzir cascatas. Rc não é solução de concorrência. |

Fontes primárias: [M1 — Rust Ownership](https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html); [M2 — Rustonomicon FFI](https://doc.rust-lang.org/nomicon/ffi.html); [M3 — Rust std::rc](https://doc.rust-lang.org/std/rc/).

**Recomendação (S):** experimentar um subconjunto explícito com destruição por escopo e arenas locais; manter contagem opt-in como candidata para UI, sem prometer borrow checker completo. Menor custo de reversão requer não congelar sintaxe, layout ou ABI antes de exemplos de UI, FFI e containers. Mudar depois a semântica de ownership pode ser caro mesmo com backend substituível. **Incertezas:** escaping closures, async, ciclos e sharing entre threads. **NT:** segurança, ergonomia, custo e adequação do subconjunto à stdlib.

## 4. Boot UEFI e Ventoy

| Alternativa | Base documental | Vantagens propostas (S) | Custos e limitações (S) |
|---|---|---|---|
| Limine com protocolo versionado | VD U1: protocolo especifica estado de entrada e respostas de boot para x86-64 e aarch64, incluindo mapa de memória e framebuffer. | Evita implementar imediatamente todo o carregador; adaptador interno reduziria dependência direta do kernel. | Exige fixar revisão e tratar validade/reclamação das estruturas; não prova compatibilidade com Ventoy ou firmware local. |
| Loader UEFI próprio | VD U2: Boot Services ficam disponíveis antes de ExitBootServices; a transferência de controle exige observar seus contratos, incluindo mapa de memória. | Controle direto do carregamento e dependência menor de um protocolo de terceiro. | Mais código de boot, manutenção por arquitetura e testes de firmware; não elimina a necessidade de imagem bootável. |

Fontes primárias: [U1 — Limine Boot Protocol](https://github.com/limine-bootloader/limine-protocol/blob/trunk/PROTOCOL.md); [U2 — UEFI 2.11, Boot Services](https://uefi.org/specs/UEFI/2.11/07_Services_Boot_Services.html).

VD V1: Ventoy documenta instalação prévia e posterior cópia de imagens. VD V2: modo normal lê o necessário ao boot; memdisk carrega a imagem inteira, consome RAM adicional e exige não precisar remontar a ISO depois do boot; a documentação indica imagens normalmente menores que 1 GB. Fontes: [V1 — Ventoy Get Started](https://www.ventoy.net/en/doc_start.html), [V2 — Ventoy Memdisk](https://www.ventoy.net/en/doc_memdisk.html).

**Recomendação (S):** experimentar Limine primeiro com tradução do handoff para estruturas internas ainda não públicas. Futuro ensaio Ventoy deve comparar modo normal e, apenas se a ISO cumprir as condições documentadas, memdisk. Carregar o live em RAM é hipótese, não compatibilidade demonstrada. **Incertezas:** leitura da ISO como disco virtual, arquivos necessários após boot, revisões, Secure Boot e diferenças de firmware/arquitetura. **NT:** ISO híbrida, boot direto, Ventoy normal/memdisk e Secure Boot.

**Pré-condição explícita:** teste Ventoy depende de instalação prévia ou imagem virtual existente com Ventoy instalado. ISO isolada anexada como CD-ROM não exerce o caminho Ventoy. Não houve download de artefatos, instalação, criação de imagem ou escrita em dispositivo físico nesta tarefa; se a imagem não existir, o teste futuro fica bloqueado e deve ser encaminhado ao Líder. Não executar instalador apontando a discos reais.

## 5. Hardware e ambiente de referência

VD E1: QEMU separa aceleradores por SO do processo hospedeiro: WHPX para Windows, KVM para Linux e TCG como tradução de CPU. VD E2: WHPX exige o recurso Windows Hypervisor Platform; sua documentação distingue hosts Windows x86-64 e ARM64. Isso não comprova recurso ativo nesta máquina. VD E3: WSL2 oferece configuração de virtualização aninhada, cuja presença não certifica disponibilidade de /dev/kvm nem kernel com suporte utilizável.

| Alternativa | Vantagens propostas (S) | Custos e condições |
|---|---|---|
| QEMU Linux dentro de WSL2 Ubuntu, TCG inicial | Segue o ambiente de build definido no projeto e permite uma base sem pressupor KVM. | NT: WSL2 não foi inspecionado aqui; a TASK informa ausência verificada pelo Orquestrador. Não instalar. KVM só seria candidato com CPU compatível, virtualização aninhada exposta, suporte no kernel WSL e acesso efetivo ao dispositivo, comprovados em execução futura. WHPX não é backend do binário Linux. |
| QEMU Windows nativo com WHPX para guest x86-64 em host x86-64 | Pode acelerar ensaios de boot após disponibilidade confirmada. | VD E2: requer o recurso do Windows. NT: build do QEMU, CPU, firmware e inicialização do acelerador locais. Depende de exceção coordenada ao padrão de executar testes no WSL2; não é autorização para mudar o ambiente. Um executável Windows invocado a partir do WSL continua sendo QEMU Windows. |
| QEMU com TCG para referência entre arquiteturas | Alternativa sem aceleração de hardware e caminho de compatibilidade aarch64 em host x86-64. | S: custo de emulação provavelmente maior; não usar seus tempos para afirmar desempenho nativo. NT: versões e disponibilidade locais. WHPX x86-64 não acelera um guest aarch64; o suporte WHPX ARM64 documentado é para host Windows ARM64 compatível, não tradução x86→Arm. |

Fontes primárias: [E1 — QEMU Introduction](https://www.qemu.org/docs/master/system/introduction.html); [E2 — QEMU WHPX](https://www.qemu.org/docs/master/system/whpx.html); [E3 — Microsoft WSL Configuration](https://learn.microsoft.com/en-us/windows/wsl/wsl-config).

VD E4: máquina Arm virt é virtual, tem UART PL011 e modelos versionados. VD E5: pc-i440fx oferece portas seriais e periféricos PC; seu padrão usa BIOS, portanto selecionar a máquina não fornece UEFI automaticamente. VD E6: OvmfPkg documenta firmware UEFI para máquinas virtuais. Fontes: [E4 — QEMU Arm virt](https://www.qemu.org/docs/master/system/arm/virt.html), [E5 — QEMU PC](https://www.qemu.org/docs/master/system/i386/pc.html), [E6 — TianoCore OvmfPkg README](https://github.com/tianocore/edk2/blob/master/OvmfPkg/README).

**Recomendação (S):** perfil documental mínimo candidato: guest x86-64 com pc-i440fx e firmware OVMF compatível; guest aarch64 com virt, CPU 64-bit explícita e firmware EDK2/AAVMF compatível, ambos com serial e TCG como base de compatibilidade. Fixar versão da máquina/QEMU, CPU, firmware e hashes somente quando os artefatos autorizados existirem. RAM e vCPUs são parâmetros a dimensionar, não hardware constatado. Não usar firmware x86 em Arm. WHPX pode ser perfil posterior separado e aprovado; WSL ausente permanece bloqueio operacional, sem nova sondagem ou instalação aqui. **Incertezas:** host ISA, versões, firmware Arm disponível, aceleração e diferenças de dispositivos. **NT:** todos os boots, tempos, SMP e compatibilidade real; não existe benchmark nesta entrega.

## Encaminhamento

Recomendações permanecem hipóteses de baixo compromisso inicial. Somente o Verificador pode registrar a revisão independente e o Líder conferir o aceite; nenhum item aqui significa aprovação. A principal lacuna é execução futura autorizada, especialmente handoff em duas arquiteturas, port nativo do backend e caminho Ventoy completo.
