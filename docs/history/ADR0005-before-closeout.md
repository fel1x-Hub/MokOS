# ADR 0005 — referência virtual e aceleração
## Adendo aprovado de ambiente — 2026-11-05
Usuário informou não possuir administrador no Windows e autorizou explicitamente Linux remoto e atualização das instruções; escolheu GitHub Codespaces. Este adendo substitui a exigência WSL/WHPX da decisão histórica abaixo, sem aprovar demais ADRs nem concluir Etapa A.

- Execução no Linux remoto, preferindo Ubuntu; versão e arquitetura reais pendentes de inventário. No Codespaces, repositório no filesystem persistente /workspaces/<repositorio>, caminho a registrar após acesso.
- QEMU headless x86_64 primário e aarch64 emulado. TCG é baseline documental; KVM exige disponibilidade/permissões e teste real. Nenhum perfil executado. WHPX não integra o perfil Linux remoto.
- Somente imagens de disco em arquivos regulares; nenhuma escrita em dispositivo físico nem alteração privilegiada do host. Boot, firmware, ISO e Ventoy no Codespaces ainda não testados. Avaliar limites reais antes de escolher outro host.
- Escolha do provedor autorizada; acesso remoto ainda não conectado. Plano pago, cobrança adicional e CI/prebuilds não autorizados. Não supor acesso dos demais agentes ou persistência fora do workspace.
- Reversão: mover workspace/documentação para outro Linux e repetir inventário/baselines. Não há código ou ABI acoplado à mudança. A troca futura para provedor pago requer definição de orçamento.

Fonte primária consultada em 2026-11-05: [aceleradores do QEMU](https://www.qemu.org/docs/master/system/introduction.html). TCG suporta Linux; KVM é específico de host Linux e WHPX de Windows. A fonte não comprova recursos disponíveis na conta do usuário. Adendo ainda sem revisão independente; aprovação do usuário cobre ambiente, não resultado operacional.

## Histórico anterior ao adendo
Status: provisório, aguarda aprovação do usuário
Classificação: hardware solicitado verificado na instrução; perfis concretos e aceleração local não testados. Documento preparado, não integrado.

## Decisão
Manter QEMU x86_64 primário e aarch64 em emulação pura como referência, Windows 11 com WSL2 Ubuntu e projeto ~/mokos. Para QEMU Linux dentro de WSL, usar TCG como baseline candidato; WHPX permanece perfil Windows condicional, não presumido como backend do binário Linux. Não mudar a regra de build/scripts/testes em WSL nesta sessão.
O ambiente WSL está ausente, logo nenhum perfil foi provisionado ou executado. Não fixar CPU, firmware/hash, RAM ou versão sem artefatos disponíveis. Pesquisa sugere pc-i440fx/OVMF e virt/AAVMF como candidatos a validar.

## Alternativas
- QEMU Linux/WSL com TCG para x86_64 e aarch64: segue o local de execução, sem pressupor KVM; tempos de emulação não representam desempenho nativo.
- QEMU Windows x86_64 com WHPX: alinhado ao acelerador solicitado, mas depende de disponibilidade e resolução do fluxo/regra de testes no WSL; instalação Windows fora da lista noturna.
- Hardware físico primário: adiado por custo/reprodutibilidade e fora da autorização de escrita em dispositivos.
Fontes: https://www.qemu.org/docs/master/system/introduction.html , https://www.qemu.org/docs/master/system/whpx.html , https://www.qemu.org/docs/master/system/arm/virt.html . QEMU separa aceleradores por host; isto não comprova disponibilidade nesta máquina.

## Reversão
Perfis de teste são substituíveis; trocar máquina/acelerador exige nova baseline e revalidação, sem alterar ABI do SO. Antes de instalar/executar QEMU Windows ou alterar o fluxo, registrar aprovação do usuário. Não presumir KVM; não habilitar recursos do Windows nesta noite.
## Proveniência e limite
Relatórios preparados, não integrados:
- Ideação: C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/76273b66-47c3-4f75-8927-350f2233deef/work/01-ideacao/A-DECISIONS/RELATORIO.md
- Pesquisa: C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/b48a6ac2-d737-469c-bd3d-d6d73f133b39/work/02-pesquisa/A-SOURCES/REPORT.md
Crítica/verificação independente ainda em curso quando este rascunho foi preparado. Aceite posterior deve ser consultado em docs/PROGRESS.md. Não há aprovação do usuário nem evidência experimental. Esta ADR não autoriza aquisição de terceiros, instalação fora da lista ou alteração de ABI estável.

Adendo de encerramento: Ideação aceita documentalmente; Pesquisa com critérios técnicos aprovados, mas sem aceite integral por R1. Ver caminhos e vereditos em ../PROGRESS.md e ../MORNING.md. Esta ADR não foi revalidada independentemente.
