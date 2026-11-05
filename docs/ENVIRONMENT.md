# Ambiente atual - Codespaces
Data: 2026-11-05. Verificado pelo Orquestrador por comandos Linux; revisores documentais nao reexecutaram os comandos.
Workspace persistente do provedor: /workspaces/MokOS; Ubuntu 24.04.5 LTS x86_64. Transporte pelo portal Codespaces local MokOS.
Ativar Rust em cada terminal: source /workspaces/.mokos-tools/activate
Rust 1.99.1 fixado em rust-toolchain.toml, perfil minimal; targets x86_64-unknown-none e aarch64-unknown-none instalados. Cache fora do Git em /workspaces/.mokos-tools; recuperacao apos rebuild nao testada.
Ferramentas presentes: QEMU x86_64/aarch64 8.2.2 (Debian 1:8.2.2+ds-0ubuntu1.18), NASM 2.16.01, just 1.21.0, xorriso 1.5.6, GNU as 2.42, clang 18.1.3, GCC 13.3.0 e Git 2.56.0. Pacotes OVMF/AAVMF 2024.02-2ubuntu0.10.
Evidencia: [inventario completo, comandos/saidas e hashes](evidence/2026-11-05-toolchain-inventory.json). Logs de apt/rustup/pin preservados em evidence/. Listagem de faltantes foi mostrada ao usuario antes de instalar. Instalacao somente no remoto.
QEMU inicializa com TCG e CPU pausada em pc-i440fx-8.2 e virt-8.2/cortex-a72, 256M, CODE pflash somente leitura e VARS copiado para /tmp. Timeout 124 esperado. Primeira tentativa com -bios/OVMF_CODE_4M.fd falhou e esta preservada; a configuracao corrigida passou em ambas as arquiteturas.
Isso NAO e boot de firmware nem MokOS. Nao testados: build de produto, kernel, ISO, assinatura, Ventoy, desempenho, Secure Boot, KVM, persistencia apos rebuild. /dev/kvm existe, mas nao foi usado.
Repositorio fornecido pelo usuario: https://github.com/fel1x-Hub/MokOS, publico antes da importacao, conforme [contexto real](evidence/2026-11-05-repository-context.json). Visibilidade nao alterada; usuario instruiu subir o trabalho nesse repositorio.
Historico do inventario antes de instalar: [arquivo preservado](history/ENVIRONMENT-before-closeout.md). Ausencias daquele levantamento nao descrevem o estado atual.
