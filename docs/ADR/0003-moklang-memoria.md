# ADR 0003 — adiar compromisso semântico de memória
Status: provisório, aguarda aprovação do usuário
Classificação: decisão de adiamento; segurança, ergonomia e custos não testados. Documento preparado, não integrado.

## Decisão
Não congelar modelo de memória, sintaxe, ABI ou runtime esta noite. A reversão posterior é cara e as frentes não convergiram no mecanismo: Ideação recomenda estudar ownership estático como direção; Pesquisa propõe explorar memória explícita e arenas/destruição por escopo. Registrar a divergência e manter a memória explícita exigida pelo produto como requisito, sem escolher implementação. Não construir compilador, stdlib ou UI em cima de qualquer hipótese no M0.

## Alternativas
- Manual explícita/arenas com destruição por escopo: implementação inicial menor como hipótese, mas erros de vida útil e valores que escapam exigem solução.
- Ownership e empréstimos estáticos: potencial de checagem sem coletor obrigatório; custo do analisador e ergonomia da UI desconhecidos.
- Contagem opt-in: candidata ao compartilhamento em UI; ciclos e concorrência precisam de política.
Fontes: https://doc.rust-lang.org/book/ch04-01-what-is-ownership.html , https://doc.rust-lang.org/std/rc/ e https://doc.rust-lang.org/nomicon/ffi.html . As garantias de Rust não se transferem automaticamente à Moklang.

## Reversão e condição de decisão
Agora o adiamento pode ser substituído por ADR com exemplos revisados. Depois de programas publicados, trocar ownership muda programas aceitos, destruição e bibliotecas: custo alto. Solicitar exemplos futuros de posse, empréstimo, callback cancelável, ciclo, async, FFI e containers; revisão Moklang antes de implementação. Fora do M0 e pendente do usuário.
## Proveniência e limite
Relatórios preparados, não integrados:
- Ideação: C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/76273b66-47c3-4f75-8927-350f2233deef/work/01-ideacao/A-DECISIONS/RELATORIO.md
- Pesquisa: C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/b48a6ac2-d737-469c-bd3d-d6d73f133b39/work/02-pesquisa/A-SOURCES/REPORT.md
Crítica/verificação independente ainda em curso quando este rascunho foi preparado. Aceite posterior deve ser consultado em docs/PROGRESS.md. Não há aprovação do usuário nem evidência experimental. Esta ADR não autoriza aquisição de terceiros, instalação fora da lista ou alteração de ABI estável.

Adendo de encerramento: Ideação aceita documentalmente; Pesquisa com critérios técnicos aprovados, mas sem aceite integral por R1. Ver caminhos e vereditos em ../PROGRESS.md e ../MORNING.md. Esta ADR não foi revalidada independentemente.
