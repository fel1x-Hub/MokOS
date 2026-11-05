# A-DECISIONS — TASK do Líder

Estado: autorizado para análise; não integrado. Uma tarefa, somente trio existente.
Origem: C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/68c04052-f73c-49e5-a860-7b19c869ea12/work/01-ideacao/A-DECISIONS/TASK.md

## Escopo
Ideador produz relatório de recomendações provisórias reversíveis para cinco decisões: kernel, backend mklc, memória Moklang, bootloader/Ventoy e hardware de referência. Para cada decisão: problema, 2–3 alternativas, proposta recomendada, prós/contras, custo, custo de reversão, riscos e condições de adiamento. Recomendações não aprovam arquitetura nem autorizam implementação.
Hardware solicitado: QEMU x86_64 com WHPX quando disponível; aarch64 emulação pura; Windows 11/WSL2 Ubuntu. WSL ausente conforme TASK de origem; nenhuma capacidade de execução deve ser presumida.

## Fora de escopo
Código, testes de boot/build, instalação, novos nós, dependências, commits, decisões arquiteturais caras, ABI/syscalls, integração e alteração de arquivos globais. Não acessar disco/dispositivo físico para escrita. Não copiar terceiros.

## Interfaces e arquivos
Fonte de verdade: AGENTS.md da raiz e agents/01-ideacao/{executor,testador}.md. Divergência 00/01 resolvida em favor de 01, diretório real e frente atribuída. docs/INTERFACES.md e docs/PROGRESS.md ausentes na raiz verificada; não criar nem inferir contratos.
Cada agente escreve apenas no próprio sandbox: work/01-ideacao/A-DECISIONS/; informa caminhos absolutos. Executor: relatório e IMPL_NOTES.md; Testador: TEST_REPORT.md independente com evidências e veredito por decisão e critério. Líder: TASK.md, STATUS.md e RESULTADO_FINAL.md.
Entrega não integrada. Trocas curtas pelo maestri ask, apontando arquivos. Executor encaminha entrega ao Testador e avisa Líder; Testador responde a ambos com caminho do relatório. Usar ask back para Líder ideação.

## Critérios de aceite
A1. Cinco decisões cobertas, cada uma com 2–3 alternativas distintas.
A2. Cada alternativa tem trade-offs, custo relativo/estimado e custo explícito de reversão; cada recomendação tem riscos e justificativa, sem decisão cara servir de base esta noite.
A3. Hardware e limitações do ambiente respeitados; Ventoy e WHPX não declarados validados sem execução real.
A4. Crítica independente do Testador com veredito por decisão, evidências documentais identificáveis, falhas e pendências; nenhuma execução inventada.
A5. Fatos documentais, suposições e itens não testados rotulados; fontes externas só se realmente consultadas; hipóteses técnicas sem pesquisa classificadas como suposição.
A6. Somente artefatos nos sandboxes respectivos, sem código ou alteração de contrato, e caminhos absolutos reportados. Líder confere A1–A6 após evidência do Testador.

## Modelo/esforço e loop
TOP Sol; MEDIO Terra; RAPIDO Luna; sem Astra; máximo high, preferir medium, sem trocar atribuições. Preparação do Executor verificou ausência de identificação exata do modelo/esforço em runtime: ambiente declara GPT-6; TOP/médio é atribuição prescrita, não configuração comprovada. Manter agente existente, não trocar modelo; registrar limitação em IMPL_NOTES. Líder também não dispõe de identificador runtime verificável.
Máximo 5 ciclos; no terceiro solicitar esforço maior até high, somente se ferramenta permitir, senão registrar e escalar. Mesma falha 3 vezes exige reavaliar. Ao aprovar ou bloquear, reportar Orquestrador geral e ficar parado.