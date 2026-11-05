# A-CLOSEOUT — revisão independente do bootstrap remoto

Objetivo: revisar a entrega documental do PR https://github.com/fel1x-Hub/MokOS/pull/1, commit congelado b6df12d84475b3270089436732f819fa50d474f7, contra critérios Etapa A e achados C01–C12. Não fazer merge ainda. Usuário pediu finalizar Etapa A e continuar; gate técnico permanece obrigatório.

Configuração autorizada: Líder Sol/medium, Integrador Sol/medium, Testador Terra/medium. Aplicar MEDIO Terra pelo seletor nativo existente e confirmar rodapé; não reiniciar/criar terminal nem mudar atribuição. Máximo high; sem Astra/xhigh. Registrar limitações de evidência/custo.

Fontes: arquivos do commit remoto (repositório público, pode usar raw.githubusercontent.com/fel1x-Hub/MokOS/<commit>/<arquivo>); raiz AGENTS, 33 perfis, docs/SPEC, INTERFACES, ROADMAP, PROGRESS, TOOLING, ENVIRONMENT, cinco ADRs, quatro templates e evidências importadas. Cópia local pré-importação em C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/68c04052-f73c-49e5-a860-7b19c869ea12/migration/remote-root/ é histórica: não substitui textos remotos que mudaram. Se acesso à revisão congelada falhar, escalar sem inventar leitura nem solicitar bypass.

Líder: organizar uma tarefa por vez, separar ownership em TASK própria; consultar leitura de cada revisor; manter três trios ativos no máximo (Pesquisa + Integração nesta janela). Executor produz revisão de coerência/achados com correções propostas; não modifica fontes congeladas. Testador prepara plano e reavalia independentemente, sem usar parecer do Integrador como substituto.

Aceite: cobertura A1–A5; modelos declarados versus observados; loop de revisão e autorização rastreados; cinco decisões com alternativas/fontes/recomendações/adiamentos explícitos; nomes, ISO/assinatura e interfaces coerentes; LF/33 perfis/templates; inventário real distinguido de boot não testado; referências históricas locais tratadas como tais. Não exige implementar ou bootar para aprovar documentação. Ferramentas serão preparadas pelo Orquestrador e terão evidência separada; qualquer atualização posterior requer revisão focal, não herda aceite.

Relatório deve distinguir bloqueios reais de Etapa A de débitos que só bloqueiam M0/futuros marcos. Limine/Ventoy/Cranelift não adquiridos; não tratar candidato como dependência instalada. Memória Moklang adiada, sem congelar semântica.

Ownership: cada papel somente seus TASK/IMPL_NOTES/TEST_REPORT/STATUS no próprio sandbox work/10-integracao/A-CLOSEOUT/. Sem alteração de fontes/testes alheios, raiz Windows, CI/infra ou produto; sem merge/push nesta TASK. Relatórios com caminhos absolutos/hashes e comandos reais. Máximo 5 ciclos; terceiro eleva esforço dentro de high máximo ou escala.

Retorno por maestri ask ao Orquestrador geral: resultado final, arquivos/hashes, bloqueios e correções mínimas. O Orquestrador aplica mudanças documentais autorizadas, solicita revisão focal e publica evidências.
