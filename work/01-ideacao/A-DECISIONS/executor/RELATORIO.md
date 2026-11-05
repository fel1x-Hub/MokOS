# A-DECISIONS — recomendações provisórias, ciclo 1

Estado: entrega documental não integrada, aguardando crítica independente e aceite do Líder. Nenhuma alternativa está aprovada para implementação, nem serve de base arquitetural esta noite.

## Evidências e convenções

**Verificado documentalmente:** foram lidos os documentos locais E1–E5 abaixo. E1 exige kernel próprio, Rust por padrão, Moklang com controle explícito de memória, UEFI, teste Ventoy, Windows 11/WSL2 Ubuntu e ausência de escrita em dispositivo físico. E2 limita esta entrega ao papel de Ideador. E4 e E5 autorizam análise provisória, proíbem implementação e registram WSL ausente. A divergência 00/01 foi resolvida pela TASK e pela instrução do solicitante em favor de `01-ideacao`.

| ID | Fonte local efetivamente consultada |
| --- | --- |
| E1 | `C:/Users/20260210-ieg/Desktop/MokOS/AGENTS.md` |
| E2 | `C:/Users/20260210-ieg/Desktop/MokOS/agents/01-ideacao/executor.md` |
| E3 | `C:/Users/20260210-ieg/Desktop/MokOS/agents/01-ideacao/testador.md` |
| E4 | `C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/0bd13b93-8062-4bd3-a81e-cff3444f9334/work/01-ideacao/A-DECISIONS/TASK.md` |
| E5 | `C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/68c04052-f73c-49e5-a860-7b19c869ea12/work/01-ideacao/A-DECISIONS/TASK.md` |

**Suposição:** todas as comparações técnicas, benefícios esperados, custos, compatibilidades potenciais e recomendações nas seções D1–D5. São hipóteses para a frente Pesquisa confirmar; não foram consultadas fontes externas. E1 é fonte de requisitos, não prova de desempenho ou compatibilidade de produtos.

**Não testado:** toolchains, compilação, boot, Ventoy, WHPX, QEMU, disponibilidade de firmware, execução no WSL, consumo de memória, latência, licenças e versões de ferramentas. A ausência de WSL é informação documental de E4/E5, não nova sondagem executada por este Executor.

Custos relativos **baixo / médio / alto** comparam alternativas dentro da mesma decisão: baixo implica pouca elaboração local; médio implica projeto e validação próprios; alto implica trabalho estrutural e manutenção contínua. Não são prazos, horas ou medições. Custo de reversão aparece em dois momentos: **agora**, quando só existe proposta documental; **depois**, caso uma futura autorização leve à implementação e adoção. Nenhum limite de ABI, formato ou API é estabelecido aqui.

## D1 — Organização do kernel

**Problema (requisito documental E1):** conciliar kernel próprio, isolamento e desempenho sem comprometer cedo a organização de drivers e serviços.

| Alternativa | Prós esperados (suposição) | Contras e risco (suposição) | Custo relativo (suposição) | Reversão explícita (suposição) |
| --- | --- | --- | --- | --- |
| K1. Monolítico modular | Menos fronteiras de execução no caminho inicial; facilita investigar o primeiro boot e módulos básicos. | Falhas de drivers podem afetar todo o kernel; modularidade não comprova isolamento. Pode tornar cara a extração futura de serviços. | Médio: núcleo e drivers ainda próprios; menor elaboração inicial de transporte entre serviços que K2. | Agora baixo: revisar proposta. Depois alto: separar módulos em processos exige redesenhar dependências, ownership de memória e comunicação. |
| K2. Microkernel | Fronteiras de isolamento explícitas; possibilidade de reiniciar serviços separadamente. | Projeto de comunicação e recuperação mais amplo desde cedo; latência e cópias dependem da implementação, sem garantia de vantagem. | Alto: serviços, transporte, inicialização e tratamento de falhas distribuídos. | Agora baixo. Depois alto: reunir serviços muda modelo de segurança e comunicação; requer revalidação de isolamento. |
| K3. Híbrido com conjunto mínimo privilegiado e serviços selecionados fora dele | Permite estudar extração seletiva de componentes. | A seleção pode ser arbitrária, duplicar mecanismos e ampliar a superfície privilegiada; não assegura equilíbrio de desempenho. | Alto: exige justificar duas formas de execução e suas fronteiras. | Agora baixo. Depois alto: migração de cada componente pode atravessar ambos os modelos e contratos. |

**Proposta recomendada (suposição):** K1 como candidato inicial para comparação futura, pela menor quantidade presumida de mecanismos necessários ao diagnóstico do M0/M1. A recomendação não determina que drivers ou serviços ficarão permanentemente privilegiados. Isolamento exigido pelo produto continua sendo obrigação a demonstrar.

**Riscos da recomendação:** dependências internas podem cristalizar; baixo custo inicial pode ocultar custo posterior de isolamento. Não há dados que autorizem alegar desempenho superior.

**Condição de adiamento:** manter a escolha aberta até Pesquisa comparar isolamento/IPC e o Orquestrador/usuário aceitar uma ADR. Se isolamento de drivers já for requisito obrigatório do primeiro marco, reavaliar K2 antes de implementar. Esta noite: apenas registrar candidatos, sem definir contratos.

## D2 — Backend do compilador mklc

**Problema (E1):** equilibrar compilação rápida, qualidade do código e manutenção para bootstrap em Rust, x86_64/aarch64 e futuro self-hosting. Suporte de um backend ao host de desenvolvimento não prova suporte ao futuro MokOS.

| Alternativa | Prós esperados (suposição) | Contras e risco (suposição) | Custo relativo (suposição) | Reversão explícita (suposição) |
| --- | --- | --- | --- | --- |
| B1. LLVM | Potencial para otimização ampla e suporte a múltiplos alvos. | Integração e builds possivelmente pesados; portabilidade ao MokOS, licenças/versões e tempo de compilação precisam de pesquisa. | Alto: dependência ampla e manutenção da integração. | Agora baixo. Depois alto: substituir lowering, depuração e integração de alvos; manter semântica da linguagem não elimina essa migração. |
| B2. Cranelift | Hipótese de integração mais enxuta e compilação rápida para bootstrap. | Qualidade do código e recursos por alvo podem não bastar; compatibilidade bare-metal e futura execução nativa não demonstradas. | Médio: integração ainda exige lowering, objetos, ligação e runtime mínimo. | Agora baixo. Depois médio/alto: reescrever emissão e convenções internas; maior se detalhes do backend vazarem à linguagem. |
| B3. Gerador de código próprio | Controle direto da implementação e dependências. | Exige seleção de instruções, registradores, alvos e depuração; risco elevado de correção e otimização insuficiente. | Alto: manutenção contínua para duas arquiteturas e otimizações. | Agora baixo. Depois alto: substituir gerador e reconstruir validação de correção. |

**Proposta recomendada (suposição):** B2 como primeiro candidato de pesquisa para bootstrap, condicionado à demonstração posterior dos alvos, formatos de objeto e ligação necessários. A escolha definitiva não deve ser tomada com base apenas na reputação de velocidade. B1 permanece candidato se requisitos indispensáveis falharem em B2; B3 fica adiado pelo custo presumido.

**Riscos da recomendação:** dependência não portar ao MokOS; funcionalidades da linguagem exigirem recursos ausentes; introdução prematura de dependência grande. Não se autoriza adicionar bibliotecas.

**Condição de adiamento:** aguardar matriz documentada de alvos, licenças e necessidades do compilador e, em tarefa futura autorizada, comparação com o mesmo programa e condições de medição. Nesta noite não fixar IR, backend, ABI ou dependências. Uma futura separação entre semântica e emissão é apenas hipótese de redução do custo de reversão, não novo contrato.

## D3 — Modelo de memória da Moklang

**Problema (E1):** oferecer controle explícito e abstrações de custo previsível, contemplando componentes reativos e signals/slots sem assumir um runtime pesado. Segurança opcional e ergonomia precisam de semântica clara.

| Alternativa | Prós esperados (suposição) | Contras e risco (suposição) | Custo relativo (suposição) | Reversão explícita (suposição) |
| --- | --- | --- | --- | --- |
| M1. Gerência manual explícita, com camada segura futura | Controle visível de alocação/liberação e bootstrap conceitualmente menor. | Vazamentos e uso após liberação; camada futura não torna código atual seguro; callbacks e cancelamento exigem cuidado. | Médio inicialmente, alto em auditoria e diagnóstico. | Agora baixo. Depois alto: inserir ownership ou contagem muda código, bibliotecas e expectativas de vida útil. |
| M2. Ownership com empréstimos estáticos; escape inseguro explícito | Possibilidade de detectar parte dos erros de vida útil antes da execução, sem coleta global. | Analisador complexo; grafos reativos e referências compartilhadas podem exigir mecanismos adicionais. Segurança e custo zero não estão provados. | Alto: semântica, análise e diagnósticos fazem parte central do compilador. | Agora baixo. Depois alto: relaxar ou trocar regras altera programas aceitos e bibliotecas. |
| M3. Contagem de referências explícita ou opt-in para objetos compartilhados | Pode facilitar compartilhamento em UI; destruição associada à última referência, conforme semântica futura. | Atualizações de contadores custam; ciclos precisam de política; compartilhamento entre threads pode exigir sincronização. | Médio/alto: suporte de compilador/biblioteca e estratégia para ciclos. | Agora baixo. Depois alto: substituir contagem altera ownership, comportamento de destrutores e estruturas da UI. |

**Proposta recomendada (suposição):** estudar M2 como direção de longo prazo, mantendo decisão adiada. Antes de selecionar, solicitar exemplos documentais de posse exclusiva, empréstimo, callback cancelável e ciclo entre componentes para confrontar as três alternativas. Não propor M1 como linguagem já estabelecida nesta noite: isso criaria migração semântica cara. M3 pode ser avaliada como mecanismo opt-in futuro, sem presumir combinação aprovada.

**Riscos da recomendação:** esforço do analisador atrasar o compilador; restrições tornarem UI impraticável; promessa indevida de segurança. A capacidade de implementar M2 não foi demonstrada.

**Condição de adiamento:** enquanto faltarem invariantes de vida útil, política de destruição/ciclos e aceitação de exemplos pelo revisor Moklang, nenhuma sintaxe ou regra pública deve ser congelada. Encaminhar decisão semântica ao Orquestrador/usuário por ADR; não iniciar runtime ou stdlib com hipótese irreversível.

## D4 — Bootloader e Ventoy

**Problema (E1/E4):** alcançar UEFI nas duas arquiteturas e ISO live via Ventoy, sem confundir boot direto em QEMU com validação da ISO exposta como disco virtual. Secure Boot, persistência de variáveis e firmware são questões separadas, não capacidades comprovadas.

| Alternativa | Prós esperados (suposição) | Contras e risco (suposição) | Custo relativo (suposição) | Reversão explícita (suposição) |
| --- | --- | --- | --- | --- |
| L1. Limine como candidato de bootloader externo | Possibilidade de reaproveitar carregamento e handoff já definidos pelo projeto externo. | Versão, licença, suporte a ambas as arquiteturas e forma de distribuição via Ventoy precisam ser confirmados; dependência externa. | Médio: integração/empacotamento e validação; menor trabalho próprio presumido que L2. | Agora baixo. Depois médio/alto: adaptar entrada, mapa de memória e framebuffer; alto se protocolo contaminar o kernel. |
| L2. Carregador UEFI próprio | Controle sobre carregamento e diagnóstico dos caminhos de firmware. | Responsabilidade própria sobre firmware, saída dos serviços de boot e localização dos arquivos; risco e manutenção maiores. | Alto: código de boot nas duas arquiteturas e matriz de firmware/ISO. | Agora baixo. Depois alto: trocar handoff e refazer testes de firmware e distribuição. |
| L3. GRUB como candidato externo | Outra via para estudar carregamento de ISO e integração com ferramentas existentes. | Adequação do protocolo, arquitetura, configuração e licenciamento não pesquisada; não presumir que disponibilidade em Linux resolve o caso MokOS. | Médio/alto: investigar caminho de boot adequado e empacotamento. | Agora baixo. Depois médio/alto: trocar configuração e handoff e repetir matriz de boot. |

**Proposta recomendada (suposição):** L1 como candidato de pesquisa, condicionado ao suporte efetivo exigido. Se não cobrir ambos os alvos, reavaliar L2/L3 com Pesquisa; não escolher silenciosamente um bootloader diferente por arquitetura.

**Riscos da recomendação:** ISO depender de localização indisponível sob Ventoy; validação x86_64 ser tomada como prova aarch64; confusão entre bootloader do MokOS e manutenção do menu dual boot do instalador. A recomendação não define instalador nem sua interação com ESP.

**Condição de adiamento:** WSL/ferramentas indisponíveis e suporte não pesquisado impedem aceitação técnica. Plano futuro, não executado: comparar boot direto UEFI e boot da mesma ISO via Ventoy em imagens virtuais, por arquitetura quando suportado e com firmware/versões registrados; verificar acesso aos arquivos de boot/live e saídas reais. Falta de suporte aarch64 deve constar como bloqueio, sem inferir compatibilidade. Pendrive físico permanece teste manual do usuário. Nenhuma ISO ou dispositivo foi produzido ou alterado.

## D5 — Hardware de referência e ambiente

**Problema (E1/E4/E5):** separar plataforma virtual reproduzível, aceleração disponível e hardware real; respeitar Windows 11/WSL2 Ubuntu com WSL documentado como ausente.

| Alternativa | Prós esperados (suposição) | Contras e risco (suposição) | Custo relativo (suposição) | Reversão explícita (suposição) |
| --- | --- | --- | --- | --- |
| H1. QEMU x86_64 como referência virtual primária; WHPX condicional; aarch64 por emulação pura | Alinha o desenvolvimento ao ambiente solicitado; mantém duas arquiteturas no plano. | WHPX depende do host/processo QEMU; a execução no WSL não comprova sua disponibilidade. Emulação aarch64 pode elevar tempo dos testes. | Médio: preparar ambiente e registrar máquinas/firmwares; nenhum preparo autorizado agora. | Agora baixo. Depois médio: trocar máquina virtual exige rever dispositivos, baseline e evidências; evita-se compromisso inicial com hardware comprado. |
| H2. Mesma matriz QEMU, com emulação pura também em x86_64 como baseline | Alternativa explícita quando WHPX não estiver disponível; potencialmente menos dependente de aceleração do host. | Execução possivelmente mais lenta; medições não se comparam diretamente ao perfil WHPX. Continua dependendo da preparação do WSL para build. | Médio: configuração e tempo de execução; custo de execução esperado maior que H1 acelerado. | Agora baixo. Depois baixo/médio: habilitar aceleração requer nova baseline e validação, sem provar equivalência de tempos. |
| H3. Hardware físico dedicado como referência primária futura | Pode revelar comportamento de firmware e dispositivos não representado na VM. | Compra/seleção, riscos operacionais e menor reprodutibilidade; conflita com a fase atual se usado para experimentar instalação. | Alto: seleção, disponibilidade e manutenção; nenhum preço pesquisado. | Agora baixo. Depois alto: drivers, compras e baselines podem prender o projeto à plataforma. |

**Proposta recomendada (suposição):** H1 como descrição provisória da referência virtual exigida, com H2 como fallback documentado se WHPX estiver indisponível. Ambos conservam aarch64 por emulação pura. Adiar H3; nenhum equipamento físico específico é selecionado ou recomendado para compra.

**Fato documental:** E1 determina builds/scripts/testes em WSL2 Ubuntu. Isso não demonstra que um QEMU Linux possa usar WHPX. **Suposição a pesquisar:** um processo QEMU no host Windows pode ser necessário para a aceleração solicitada; o fluxo entre build WSL e executor de VM precisa de resolução explícita pelo Líder/Orquestrador antes de ser adotado. Não se autoriza execução de teste fora da regra de E1. Se essa combinação conflitar com a regra global, registrar bloqueio e escalar, usando H2 apenas após confirmar que cabe à tarefa futura.

**Riscos da recomendação:** presumir aceleração sem verificar, chamar VM de hardware real ou publicar números de perfis distintos como comparáveis. Capacidade do host, memória, CPU, firmwares e versões não foram inspecionadas nesta entrega.

**Condição de adiamento:** sem WSL e ferramentas provisionadas, manter apenas o plano documental. Uma futura tarefa deve registrar versões, modelo de máquina virtual, dispositivos, firmware, memória/CPU configuradas e acelerador efetivamente usado; nenhum valor é fixado nesta proposta. H3 só será reavaliada com autorização e escopo próprios, sem escrita em disco físico pelo agente.

## Encaminhamento e pendências

As cinco recomendações são provisórias: K1, B2, estudo M2 sem escolha semântica, pesquisa L1 e referência virtual H1 com fallback H2. Todos os compromissos de implementação permanecem adiados até pesquisa, crítica e decisão pelas autoridades do projeto. Não há ADR, contrato, instalação ou dependência adicionada.

Pendências para Pesquisa/Líder: validar hipóteses e licenças de backends/bootloaders; resolver fluxo WSL/WHPX; esclarecer matriz Ventoy por arquitetura; confrontar custo do ownership com UI; obter critérios de isolamento do primeiro marco. Nenhuma dessas pendências será resolvida por expansão unilateral desta TASK.

**Não testado / pendente:** A4 depende do TEST_REPORT independente, a produzir no sandbox do Testador. O Executor não emite veredito de aceite A1–A6. O Líder confere esses critérios depois da crítica. Este ciclo termina com encaminhamento dos artefatos, sem integração.
