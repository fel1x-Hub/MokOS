# ADR 0001 — direção do kernel
Status: provisório, aguarda aprovação do usuário
Classificação: suposição arquitetural; não testado operacionalmente. Documento preparado, não integrado.

## Decisão
Adotar monolítico modular como direção provisória, conforme convergência de Ideação e Pesquisa. Nenhum loader dinâmico de módulos, contrato de syscall ou divisão definitiva de drivers nesta noite. A mudança de organização após serviços implementados é cara: não construir esses serviços enquanto a decisão estiver provisória. Um hello de boot futuro deve ser independente dessa organização.

## Alternativas
- Monolítico modular: menos mecanismos iniciais de serviços; isolamento de módulos não garantido.
- Microkernel: isolamento explícito entre serviços; exige IPC e bootstrap próprios cedo.
- Híbrido: permite extração seletiva; risco de duplicar mecanismos antes de medir necessidade.
Custos são estimativas, sem benchmark.

## Reversão
Agora: substituir esta ADR antes de implementar subsistemas. Depois: extrair serviços exige revisar ownership, segurança e comunicação; custo alto, portanto adiado. Não publicar ABI nem estruturar drivers em torno da escolha nesta sessão.

## Fonte e condição de revisão
Pesquisa usa Linux apenas como referência do conceito de módulos e seL4 como exemplo de microkernel, sem reutilizar código: https://docs.kernel.org/kbuild/modules.html e https://sel4.systems/About/ . Esses exemplos não comprovam desempenho ou segurança de MokOS.
Reavaliar se isolamento de drivers for necessário desde M1.
## Proveniência e limite
Relatórios preparados, não integrados:
- Ideação: C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/76273b66-47c3-4f75-8927-350f2233deef/work/01-ideacao/A-DECISIONS/RELATORIO.md
- Pesquisa: C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/b48a6ac2-d737-469c-bd3d-d6d73f133b39/work/02-pesquisa/A-SOURCES/REPORT.md
Crítica/verificação independente ainda em curso quando este rascunho foi preparado. Aceite posterior deve ser consultado em docs/PROGRESS.md. Não há aprovação do usuário nem evidência experimental. Esta ADR não autoriza aquisição de terceiros, instalação fora da lista ou alteração de ABI estável.

Adendo de encerramento: Ideação aceita documentalmente; Pesquisa com critérios técnicos aprovados, mas sem aceite integral por R1. Ver caminhos e vereditos em ../PROGRESS.md e ../MORNING.md. Esta ADR não foi revalidada independentemente.
