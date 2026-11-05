# ADR 0005 - referencia virtual e ambiente
Status: ambiente Linux remoto autorizado; perfis QEMU verificados somente para inicializacao pausada; boot MokOS nao testado. Data: 2026-11-05.
## Decisao e evidencia atual
GitHub Codespaces, Ubuntu 24.04.5 x86_64, /workspaces/MokOS; acesso/escrita/ferramentas confirmados. QEMU 8.2.2 TCG como baseline. Perfis inicializados: x86_64 pc-i440fx-8.2, 256M, OVMF CODE_4M + copia VARS via pflash; aarch64 virt-8.2/cortex-a72, 256M, AAVMF CODE.no-secboot + copia VARS. Hashes/comandos em ../evidence/2026-11-05-toolchain-inventory.json.
CPU pausada nos dois ensaios: prova inicializacao, nao execucao de firmware/kernel. KVM somente apos ensaio real; /dev/kvm existir nao basta. WHPX e acelerador de host Windows e nao integra o perfil Linux.
## Alternativas e trade-offs
- Linux remoto/TCG: elimina dependencia de administrador Windows, permite repeticao por arquivos; tempos nao representam hardware nativo e quotas/persistencia dependem do provedor.
- Linux remoto/KVM: candidato de aceleracao x86_64 se acesso/virtualizacao funcionar; nao presumir em Codespaces, sem ensaio agora.
- Windows/WSL ou hardware: alternativas historicas, exigem ambiente/permissoes indisponiveis ou autorizacao propria; nenhum teste fisico nesta fase.
## Reversao e limites
Mover workspace para outro Linux exige inventario, hashes e baselines novos, sem alterar ABI. Provedor pago precisa orcamento especifico. Nenhum plano pago, CI/prebuild ou dispositivo fisico autorizado. WSL e administrador local deixaram de ser requisitos por decisao do usuario.
Historico anterior preservado em ../history/ADR0005-before-closeout.md, inclusive adendo de autorizacao e fontes originais; suas pendencias de acesso estao superadas. Outros ADRs continuam candidatos/adiamentos, sem aprovacao de semantica ou subsistemas implicita.
## Fontes primarias
https://www.qemu.org/docs/master/system/introduction.html
https://www.qemu.org/docs/master/system/invocation.html
https://www.qemu.org/docs/master/system/arm/virt.html
https://raw.githubusercontent.com/tianocore/edk2/master/OvmfPkg/README
Fontes sustentam mecanismos; disponibilidade local foi verificada somente pelos ensaios descritos. Sem alegacoes de seguranca/desempenho/compatibilidade M0.
