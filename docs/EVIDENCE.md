# Índice de evidências da sessão
Estado: índice/transcrição dos resultados observados; não é log bruto de reexecução independente.
Origem: sessão do Orquestrador geral, terminal 6d9399cd-a74a-4900-aefd-81bb36b234a0, em 2026-11-04. Horário exato dos primeiros comandos não capturado; não inferir.

## Diagnóstico inicial
1. Comando: Get-Content AGENTS.md -Raw; depois leitura UTF8 integral. Cwd de leitura: pasta do papel; alvo absoluto na raiz. Fonte: saída da ferramenta nesta conversa.
2. Comando: wsl --list --verbose; cwd: pasta do Orquestrador. Chunk f07f54, exit_code=1. Saída UTF-16 renderizada com NULs; conteúdo legível: O Subsistema do Windows para Linux não está instalado; sugestão wsl.exe --install. Não executada a sugestão.
3. Comando: git status --short --branch; cwd: C:/Users/20260210-ieg/Desktop/MokOS. Chunk e658b1. Saída Git: fatal: not a git repository (or any of the parent directories): .git. O comando estava em lote PowerShell; o exit_code do lote foi 0 por comandos posteriores, portanto não usar esse código como sucesso do Git, nem atribuir 128 como código medido.
4. Comando: rg --files docs agents work; cwd: raiz. Chunk 40b5c5. docs/work não encontrados; perfis de agents listados. Depois Get-ChildItem recursivo filtrado por lider.md/executor.md/testador.md confirmou 33; chunk 889af9.
5. maestri list: chunk 31e59a, exit 0, Orquestrador geral e 11 líderes com seus pares.
6. maestri preset list: chunk 00f8e8, exit 0, cinco presets de provedores/shell; não catálogo de modelos.
7. maestri debug após falha local de JSON: chunk aa175c, exit 0; conexão e pipe OK. Não há falha de transporte demonstrada.

## Modelos
maestri check dos líderes exibe Sol medium. Líderes reportam observação dos pares em Sol medium, divergindo de Terra nos verificadores de Pesquisa e Integração. Registro de tela não certifica backend nem preço. Disponibilidade de seletor completo, troca segura e preço não verificados; nenhum novo ciclo nesses papéis após a orientação de encerrar o ciclo corrente.

## Fontes web abertas diretamente pelo Orquestrador
Consulta em 2026-11-04, sem download de binários/código:
- https://www.qemu.org/docs/master/system/introduction.html — tabela de aceleradores por host.
- https://cranelift.dev/ — Rust, AOT/JIT e alvos suportados.
- https://uefi.org/specs/UEFI/2.11/07_Services_Boot_Services.html — fronteira de Boot Services.
- https://github.com/limine-bootloader/limine-protocol/blob/trunk/PROTOCOL.md — candidato de protocolo, versão móvel.
- https://www.ventoy.net/en/doc_memdisk.html — leitura documental, sem ensaio operacional.
Ver as fontes completas e classificação nas entregas de Pesquisa e no seu TEST_REPORT.

## Limites
Não houve execução de WSL funcional, build, QEMU, ISO, Ventoy, teste em hardware ou instalação. Relatórios de outras frentes têm autoria e caminhos próprios; ler vereditos antes de considerar aceite. Arquivos preparados não estão commitados nem integrados.
