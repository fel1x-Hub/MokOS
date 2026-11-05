# A-SOURCES — checagem independente das fontes

Data da sessão: 2026-11-04. Método: web.run open para as 17 URLs da entrega, seguido de find/open nas seções indicadas. Todas retornaram conteúdo legível; nenhum resultado operacional foi testado. As linhas abaixo identificam a saída da ferramenta nesta consulta, não âncoras permanentes da página. Texto de apoio resumido pelo Verificador, sem reprodução de documentos inteiros.

| ID | URL primária efetivamente aberta | Saída observada e classificação |
|---|---|---|
| K1 | https://docs.kernel.org/kbuild/modules.html | Introduction, linhas 2–9: módulos in-tree e out-of-tree. Verificado documentalmente; não comprova isolamento. |
| K2 | https://sel4.systems/About/ | Linhas 135–139: descrição de microkernel com verificação formal. Verificado documentalmente para seL4; sem transferência de garantias a MokOS. |
| B1 | https://llvm.org/docs/CodeGenerator.html | Introduction, linhas 311–325, e SelectionDAG, 569–575: componentes de codegen por alvo e otimizações. Verificado documentalmente. |
| B2 | https://cranelift.dev/ | Linhas 3–10: Rust, AOT/JIT, x86-64/aarch64 e objetivos de compilação/otimização. Verificado documentalmente; nenhum número da página extrapolado a MokOS. |
| M1 | https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html | Linhas 14–15: gestão manual, GC e ownership conferido pelo compilador. Verificado documentalmente. Arenas Moklang permanecem suposição. |
| M2 | https://doc.rust-lang.org/nomicon/ffi.html | Destructors, linhas 202–206, e callbacks, 353: responsabilidades de recursos e validade em FFI. Verificado documentalmente. |
| M3 | https://doc.rust-lang.org/std/rc/ | Linhas 26–32: Rc, contagem não atômica, restrição de thread, Arc e ciclos/Weak. Verificado documentalmente. |
| U1 | https://github.com/limine-bootloader/limine-protocol/blob/trunk/PROTOCOL.md | Linhas 246–251: ABIs x86-64/aarch64; 369–441: memória; 716–741: resposta de framebuffer, inclusive sua possível ausência. Verificado documentalmente; revisão trunk móvel. |
| U2 | https://uefi.org/specs/UEFI/2.11/07_Services_Boot_Services.html | Linhas 14–18 e 2840–2873: Boot Services e exigência de mapa/MapKey atual na saída. Verificado documentalmente. |
| V1 | https://www.ventoy.net/en/doc_start.html | Linhas 132–137: instalação anterior à cópia das imagens. Verificado documentalmente; comandos de instalação não executados. |
| V2 | https://www.ventoy.net/en/doc_memdisk.html | Linhas 92–101: leitura normal, carga integral em RAM e condições de tamanho/remontagem. Verificado documentalmente. |
| E1 | https://www.qemu.org/docs/master/system/introduction.html | Linhas 9–22: diferenças por alvo e tabela KVM/Linux, WHPX/Windows, TCG. Verificado documentalmente. |
| E2 | https://www.qemu.org/docs/master/system/whpx.html | Linhas 7–42: WHPX, recurso Windows exigido, versões mínimas distintas e exemplos para hosts x86-64/arm64. Verificado documentalmente. |
| E3 | https://learn.microsoft.com/en-us/windows/wsl/wsl-config | A página contém aviso de autorização, mas o corpo foi retornado; linha 231 documenta nestedVirtualization. Verificado documentalmente somente quanto à opção, sem prova de KVM local. |
| E4 | https://www.qemu.org/docs/master/system/arm/virt.html | Linhas 7–21: máquina virtual versionada e PL011; 59–89: CPUs e necessidade de escolher CPU para AArch64. Verificado documentalmente. |
| E5 | https://www.qemu.org/docs/master/system/i386/pc.html | Linhas 23 e 45: serial e BIOS SeaBIOS. Verificado documentalmente; pc não entrega UEFI automaticamente. |
| E6 | https://github.com/tianocore/edk2/blob/master/OvmfPkg/README | Linhas 1111–1136: firmware virtual, X64, QEMU e UEFI. Verificado documentalmente para OVMF. A proposta EDK2/AAVMF Arm permanece candidata/suposição, sem firmware Arm validado. |

## Chamadas reais e resultado

1. web.run open: URLs K1–M3 em lote; retorno de conteúdo dos sete documentos.
2. web.run open: U1–E1 em lote; retorno de conteúdo dos cinco documentos.
3. web.run open: E2–E6 em lote; retorno de conteúdo dos cinco documentos.
4. web.run find: Introduction/reusable components (LLVM), destructor (FFI), cycle (rc), aarch64/Framebuffer (Limine), ExitBootServices (UEFI), 1GB (Ventoy), Prerequisites (WHPX), nestedVirtualization (WSL), Overview (OVMF), Copy Image Files (Ventoy).
5. web.run open: seções de QEMU Introduction/WHPX, Ventoy start/memdisk, rc, LLVM e FFI. Resultado sem contradição material às afirmações VD. A primeira abertura de LLVM mostrou navegação; buscas subsequentes localizaram o corpo relevante.

## Classificação das avaliações da entrega

As vantagens, custos, escolhas de kernel/backend/memória/boot/perfil e hipóteses de reversão são suposições explicitamente declaradas na entrega; não confirmadas como desempenho ou custo real. As 17 afirmações documentais identificadas acima foram conferidas. A ressalva local de aceleração/arquitetura decorre da distinção host/target documentada, não de execução nesta máquina. Compatibilidade MokOS/Ventoy, firmware local, segurança de memória, port do backend e todo benchmark: não testados.
