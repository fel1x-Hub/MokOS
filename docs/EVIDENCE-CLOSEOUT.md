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

## Registro final de Integração — complemento ciclo 3

**Alvo:** `090abae171090d8a5e90912ae541365fae54ca21` (base `9869e27bfe877ddd4e7299cae387e2a51607e8a1`).

- Integrador: `work/10-integracao/A-CLOSEOUT/IMPL_NOTES.md`, SHA-256 34171D7E04D907C039E1AF52FB14648BC33A47E549870DB8913734CD8A8F6464; `STATUS.md`, 1D758F8A5A6F334DC3B1E461C4491B7B373D1F9B6D1B7087EF808BEEA59C0C90.
- Testador: `work/10-integracao/A-CLOSEOUT/TEST_REPORT.md`, SHA-256 DFB2AAF3C80348671919FC43843B01146AE297AC4EA6D78DD46DDEE643358077; `STATUS.md`, BDE96ABDBCB561D913813228C98E15B2E9547336DF60380AD1FE3DE5BF70B2AF.
- Líder Integração: `work/10-integracao/A-CLOSEOUT/STATUS.md`, SHA-256 2AC4DC9ECDB10B6752EF25D42CB715F58FE2C09CBAED47CD44214B5A41BB0227.
- Orquestrador: diff focal `CICLO3-RETEST-C01.md`, SHA-256 2A650709F3D1F51B5F4FA97986C57DEFAFC57111771B7E5BAD709DC42372B621.

O Testador revalidou só a frase do critério 1; critérios 2–9 permanecem os resultados aceitos na base 9869e27. A proveniência do diff/hash foi mediada pelo Codespace/editor; não houve reautenticação independente do Git remoto. Nenhuma alegação de boot, ABI, ISO ou Ventoy foi feita.
