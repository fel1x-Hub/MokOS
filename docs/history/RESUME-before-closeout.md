# Checkpoint remoto verificado - 2026-11-05
Workspace: /workspaces/MokOS, Codespaces friendly-space-doodle-p7r4xq4v74pvcrwg4. Origem: https://github.com/fel1x-Hub/MokOS, PUBLICO conforme gh repo view. Branch: docs/remote-codespaces-bootstrap; base main/29fbf31.
Pacote: 57 entradas transferidas via portal, SHA256 e manifesto conferidos antes de extrair; README inicial preservado. Manifesto original e inventario bruto em docs/evidence/.
Ambiente: Ubuntu 24.04.5 LTS x86_64; Git 2.56.0, GNU as 2.42, clang 18.1.3, GCC 13.3.0, Python 3.14.2 e gh 2.103.3 presentes.
Ausentes no PATH: rustc, cargo, rustup, qemu-system-x86_64, qemu-system-aarch64, NASM, xorriso, just. /usr/share/OVMF, /usr/share/AAVMF e /usr/share/qemu ausentes; nao comprova ausencia global de firmware. Targets Rust ainda nao inventariados. /dev/kvm existe; acesso/execucao nao testados. TCG continua baseline.
Nenhuma instalacao, build, boot, ISO ou Ventoy executado. Etapa A parcial; kernel, compilador e instalador aguardam gate. Nenhum merge: documentacao em branch para revisao independente. Lista de ferramentas faltantes mostrada ao usuario.
Trios locais nao migrados: somente Orquestrador acessa terminal remoto pelo portal. Quota/limites da conta e recuperacao apos rebuild nao verificados.
Proximo: ferramentas, modelos/revisao independente, demais gates da Etapa A. WSL e administrador Windows nao sao requisitos. Historico abaixo preserva estados/caminhos locais anteriores, que nao se tornam acessiveis no remoto por copiar documentos.

# Retomada acompanhada — 2026-11-05

Estado: Etapa A parcial; M0 não iniciado. Pacote nesta pasta do papel, sem integração à raiz.

## Verificado nesta retomada
- AGENTS.md da raiz lido por completo; PROGRESS, TOOLING, SPEC, INTERFACES, ROADMAP, autorização anterior, relatório e cinco ADRs locais consultados.
- `wsl --list --quiet` informa que o Subsistema do Windows para Linux não está instalado. Não foi executado inventário dentro de Ubuntu.
- `git status --short` na raiz retorna `fatal: not a git repository`.
- `maestri list` mostra os onze Líderes e respectivos pares. Nenhum trio recebeu nova tarefa nem foi criado nó.
- Raiz contém AGENTS.md, agents/ e .maestri/; docs globais continuam preparados apenas nesta pasta do papel.
- Permissões efetivas permitem escrita nesta pasta do Orquestrador, não na raiz nem em um futuro ~/mokos. Autorização por mensagem não modifica o sandbox.

## Ordem para resolver pendências com o usuário
1. Ambiente: usuário autorizou Linux remoto e escolheu GitHub Codespaces em 2026-11-05, pois não tem administrador local. Conectar navegador logado ao Orquestrador geral, preparar workspace padrão e confirmar acesso, escrita e persistência. Depois executar inventário, mostrar faltantes e instalar somente ferramentas autorizadas. WSL local deixou de ser pré-requisito.
2. Modelos: confirmar MEDIO Terra nos verificadores de Pesquisa e Integração e RAPIDO Luna quando aplicável. Não abrir novo ciclo nos papéis não conformes antes da correção ou alternativa autorizada. Preservar R1 e pareceres anteriores.
3. Revisão: retomar pelos Líderes a verificação independente dos adendos/ADRs e o aceite incompleto de Pesquisa. Não transferir parecer da versão base para a versão posterior.
4. Decisões: apresentar para aprovação kernel monolítico modular (0001), candidato Cranelift sem implementação no M0 (0002), adiamento do modelo de memória Moklang (0003) e candidato Limine (0004). ADR 0005 tem adendo que substitui execução WSL por Linux remoto autorizado, TCG baseline e KVM condicional. Outras escolhas e a Etapa A não receberam aprovação por essa migração.
5. Aquisições: mostrar versões, origem e escopo de Limine/Ventoy antes de pedir autorização específica ou usar artefatos autorizados já existentes. Escolha arquitetural não autoriza aquisição. Cranelift fica fora da implementação M0.
6. Integração: com acesso liberado, revisar diferenças antes de levar o pacote à raiz; normalizar LF e resolver ambiguidades documentais de ownership, revisão e protocolo. Criar Git/worktrees no ambiente autorizado. Nada foi integrado nesta retomada.
7. Gate: concluir critérios reais da Etapa A e pedir aprovação conforme atribuição atual antes de kernel, compilador ou instalador. A autorização noturna histórica está registrada em NIGHT-AUTHORIZATION.md; não é evidência de conclusão técnica.
8. M0: só após gates, planejar contratos e tarefas separadas Rust/Assembly/Build; x86_64, aarch64, ISO direta e Ventoy, com revisão independente e até três trios ativos.

## Não testado
Toolchain Linux, QEMU, firmware, aceleração, build, boot, ISO, assinatura e Ventoy. Não há resultado de execução M0. Preços, seletor atual dos terminais e quota não foram confirmados nesta retomada.

## Interação pendente
Usuário informou que não tem administrador local, autorizou Linux remoto e atualizações de AGENTS.md/documentação, escolheu Codespaces e ofereceu conectar navegador logado. Solicitada conexão diretamente ao Orquestrador geral, usando maestri-portal. Próximo passo: confirmar portal e preparar workspace padrão. Nenhum ambiente remoto criado ou acessado até este registro. Sem aquisição de plano pago, cobrança adicional ou aprovação da Etapa A.
