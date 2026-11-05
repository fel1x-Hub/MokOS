# Migração para GitHub Codespaces

Data: 2026-11-05. Autorização: usuário sem administrador local aprovou Linux remoto, atualização de AGENTS.md e documentação e escolheu Codespaces. Pediu orientação sobre conectar navegador logado; conexão solicitada diretamente ao Orquestrador geral.

## Entrega preparada
`remote-root/` contém uma árvore documental para o futuro repositório remoto. `MOKOS-REMOTE.zip` será gerado a partir dela. Nenhum arquivo foi aplicado à raiz local, que está fora da área de escrita. Não é implementação de kernel, compilador ou instalador.

- AGENTS.md completo: substituída somente a seção de ambiente, com LF normalizado; restante preservado.
- agents/: 33 perfis originais incluídos. Alterados somente os três perfis Assembly (acelerador) e os três Build/ISO/Instalador (escalada de falha de ambiente).
- .gitattributes: `* text=auto eol=lf` para a árvore documental inicial.
- docs/: pacote atual do Orquestrador, com SPEC/ROADMAP/estado e adendo ADR 0005 alinhados à mudança.
- work/templates/: quatro templates existentes. TASKs históricas de trios não são novas ordens de trabalho e não entram no pacote.

## O que verificar no Codespaces antes de continuar
1. Confirmar conta pessoal, repositório de destino e visibilidade privada; evitar publicar conteúdo como efeito colateral. Workspace padrão autorizado; nenhum plano pago, cartão, orçamento adicional, CI ou prebuild autorizado.
2. Conferir franquia restante e tipo de máquina exibido; começar pela menor opção adequada. Não assumir gratuidade ilimitada. Se a conta não permitir criação dentro da franquia, relatar antes de ação onerosa.
3. Confirmar Linux, caminho real /workspaces/<repositorio>, escrita e persistência. Diretórios home/container podem ser reconstruídos; registrar onde estão fontes, worktrees e artefatos.
4. Transferir pacote somente para repositório novo/vazio ou revisar conflitos de arquivos existentes. Conferir hashes e LF antes de aplicar. Não sobrescrever mudanças do usuário, nem enviar .maestri/ em massa ou credenciais.
5. Inventariar Rust/targets, QEMU x86_64/aarch64, OVMF/AAVMF, assembler, clang/gcc, xorriso, just e Git. Listar faltantes antes de instalação; não usar ações CI como substituição silenciosa do ambiente interativo.
6. Validar limites QEMU/TCG, timeout, RAM e armazenamento. Boot direto, ISO e Ventoy têm evidências separadas. Nenhuma necessidade de KVM é presumida e nenhum teste M0 passou ainda.
7. Registrar transporte real para cada trio; o portal do Orquestrador não transfere automaticamente terminais, permissões ou modelos. Não iniciar implementação até resolver gates da Etapa A e aprovação exigida.

## Histórico e rastreabilidade
MORNING, EVIDENCE e NIGHT-AUTHORIZATION preservam o contexto anterior. Caminhos absolutos de relatórios de outros papéis apontam para arquivos locais originais; não se tornam acessíveis no Codespaces por copiar estes documentos. Os pareceres não cobrem esta migração; revisão independente posterior permanece pendente. A ausência histórica de WSL não é requisito do ambiente novo.

## Fontes consultadas
- [GitHub Codespaces](https://github.com/features/codespaces): acesso pelo navegador e franquia de contas pessoais. A página informa 120 core-hours e 15 GB/mês no plano Free; isso não confirma saldo ou plano do usuário.
- [Uso e franquia](https://docs.github.com/en/codespaces/troubleshooting/troubleshooting-included-usage): máquina parada interrompe computação, mas armazenamento continua consumindo franquia enquanto existir. Acompanhar uso real.
- [Aceleradores QEMU](https://www.qemu.org/docs/master/system/introduction.html): TCG em Linux, KVM condicional ao host. Não comprova QEMU funcional no Codespaces.

Classificação: documentos preparados e autorização verificados; adequação operacional do provedor é suposição; criação, transferência e execução remota não testadas.
