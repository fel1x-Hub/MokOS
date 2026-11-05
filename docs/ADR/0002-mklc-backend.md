# ADR 0002 — candidato ao backend do mklc
Status: provisório, aguarda aprovação do usuário
Classificação: suposição arquitetural; não testado. Documento preparado, não integrado.

## Decisão
Selecionar Cranelift AOT como candidato documental, convergência das duas frentes; nenhuma dependência adicionada, nenhuma implementação de compilador no M0. A semântica e representação tipada da linguagem não devem depender de APIs específicas do backend.

## Alternativas
- Cranelift: Rust, AOT/JIT, x86-64 e aarch64 documentados; port ao MokOS e qualidade do código permanecem não testados.
- LLVM: infraestrutura extensa de otimização/codegen; custo de integração e port ainda desconhecido.
- Backend próprio: controle direto, custo elevado para duas ISAs e correção.
Fontes primárias: https://cranelift.dev/ e https://llvm.org/docs/CodeGenerator.html . Não transferir benchmarks de outros projetos ao MokOS.

## Reversão
Agora: trocar recomendação sem mudar código. Após implementação: reescrever lowering, objetos e depuração; custo médio/alto. Não construir em cima da escolha esta noite. Comparar exemplos e suporte ao host MokOS antes de congelar o backend. Aquisição de Cranelift/LLVM ou dependência grande requer escopo/autorização próprios.
## Proveniência e limite
Relatórios preparados, não integrados:
- Ideação: C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/76273b66-47c3-4f75-8927-350f2233deef/work/01-ideacao/A-DECISIONS/RELATORIO.md
- Pesquisa: C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/b48a6ac2-d737-469c-bd3d-d6d73f133b39/work/02-pesquisa/A-SOURCES/REPORT.md
Crítica/verificação independente ainda em curso quando este rascunho foi preparado. Aceite posterior deve ser consultado em docs/PROGRESS.md. Não há aprovação do usuário nem evidência experimental. Esta ADR não autoriza aquisição de terceiros, instalação fora da lista ou alteração de ABI estável.

Adendo de encerramento: Ideação aceita documentalmente; Pesquisa com critérios técnicos aprovados, mas sem aceite integral por R1. Ver caminhos e vereditos em ../PROGRESS.md e ../MORNING.md. Esta ADR não foi revalidada independentemente.
