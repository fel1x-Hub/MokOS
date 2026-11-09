# Autorizações da retomada — 2026-11-05

Fonte: mensagens do usuário nesta conversa, preservadas aqui como escopo de trabalho; não são prova de conclusão técnica.

1. Usuário informou não ter administrador local e autorizou “usa remoto e atualiza o que for necessario do agents.md e outras coisas”. Escolheu GitHub Codespaces e conectou navegador logado ao repositório MokOS. Autoriza a mudança de ambiente e documentação; não implica gasto adicional, CI/prebuild ou hardware.
2. Usuário indicou MokOS como repositório “onde tudo deve subir”. Branch documental e PR #1 foram publicados, preservando README e autoria. Merge no tronco depende dos aceites previstos.
3. Usuário solicitou “continua a etapa a, finaliza e continua”. Prosseguir após critérios e aceites reais, respeitando o limite M0 anterior. A transição A→B está solicitada antecipadamente; não exige repetir a mesma pergunta depois do aceite técnico. Não declarar A pronta antes disso.
4. Instalação das ferramentas faltantes foi mostrada ao usuário antes de executar: Rust/rustup e targets, QEMU x86/ARM/utilitários, OVMF/AAVMF, NASM, xorriso e just. Realizada somente no Codespaces com pacotes oficiais e rustup; nenhum componente Windows instalado.
5. Limine/Ventoy oficiais para testes virtuais: pergunta específica enviada e ainda sem resposta explícita até este registro. Não baixar nem tratar como instalados enquanto pendente. Cranelift permanece candidato documental para M3; nenhuma aquisição agora.

Nenhuma aprovação inferida de mensagens de status dos Líderes. Modelos TOP Sol, MEDIO Terra e RAPIDO Luna, máximo high, sem Astra/xhigh; três trios ativos no máximo, nenhum novo nó. Escrita em dispositivos físicos, CI/infra, custos adicionais e ações irreversíveis continuam fora deste escopo.

## Aceite final da Etapa A — 2026-11-09

O Líder de Integração registrou o aceite do complemento focal do ciclo 3/5. A continuidade até M0 se apoia na autorização anterior do usuário, registrada no item 3, para concluir A e continuar conforme o escopo vigente. Isso não aprova aquisição Limine/Ventoy, gastos adicionais, CI/infra, disco físico ou M1.

- Commit-base 9869e27: critérios documentais 2–9 aceitos; a única lacuna focal foi a proibição literal de autoaceite no perfil Ideação 01.
- Commit 090abae171090d8a5e90912ae541365fae54ca21: o diff mediado apresentado para o reteste descreve uma alteração em `agents/01-ideacao/executor.md`; essa descrição não equivale a auditoria independente da árvore remota. Testador passou a frase focal e Líder aceitou o fechamento documental.
- A1–A5 documentais cobertos. Boot do MokOS, ISO, Ventoy, assinatura, custo e execução de Luna não demonstrados.
- Limine/Ventoy: autorização de aquisição continua pendente. Não baixar nem tratar como disponíveis.
- M0 é a fronteira atual; não iniciar M1 nem criar nós. Máximo três trios ativos.
