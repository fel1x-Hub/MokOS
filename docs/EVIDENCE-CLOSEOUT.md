# Evidências documentais da Etapa A

As cópias abaixo preservam autoria e conteúdo dos pareceres. Normalizações CRLF para LF são explicitadas no manifesto, com SHA256 de origem e publicado; bytes originais recuperáveis em evidence/2026-11-05-raw-encodings.json. [Manifesto de proveniência](evidence/2026-11-05-report-provenance.json) associa cada origem local ao destino e SHA256. Caminhos absolutos dentro dos relatórios são históricos; use os links deste índice no remoto.

## Ideação — A-DECISIONS, ciclo 1
- [Alternativas do Ideador](../work/01-ideacao/A-DECISIONS/executor/RELATORIO.md).
- [Crítica independente](../work/01-ideacao/A-DECISIONS/testador/TEST_REPORT.md).
- [Resultado aceito pelo Líder](../work/01-ideacao/A-DECISIONS/lider/RESULTADO_FINAL.md).

## Pesquisa — A-SOURCES e fechamento ciclo 2
- [Relatório técnico](../work/02-pesquisa/A-SOURCES/executor/REPORT.md) e [checagem de 17 fontes](../work/02-pesquisa/A-SOURCES/verificador/SOURCE_CHECKS.md).
- [TEST_REPORT original, com R1](../work/02-pesquisa/A-SOURCES/verificador/TEST_REPORT.md).
- [STATUS corrigido pelo Executor](../work/02-pesquisa/A-SOURCES/executor/STATUS.md), [adendo independente em Terra/high](../work/02-pesquisa/A-CLOSEOUT/verificador/TEST_REPORT.md) e [aceite do Líder](../work/02-pesquisa/A-CLOSEOUT/lider/RESULTADO_FINAL.md).
- [Seletor nativo e A5](../work/02-pesquisa/A-CLOSEOUT/lider/A5-SELETOR.md).

Os pareceres são documentais. Não comprovam boot, compilador, ABI, segurança de memória, Ventoy ou desempenho do MokOS; as recomendações permanecem suposições. A revisão original Sol/medium não é apagada pelo fechamento posterior.

## Ferramentas no Codespaces
Inventário atual e hashes de firmware em `evidence/2026-11-05-toolchain-inventory.json`. Logs oficiais de apt/rustup e falha inicial -bios preservados ao lado. QEMU foi inicializado com TCG, firmware pflash e CPU pausada nas duas arquiteturas; timeout 124 era esperado. Isso não é boot de firmware nem do MokOS. Não houve código de kernel, compilador ou instalador nesta fase.

Revisão de Integração do commit e das correções posteriores terá relatórios separados. Não transferir aceite de uma revisão para versões alteradas.
