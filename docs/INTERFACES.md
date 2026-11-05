# Interfaces
Estado: rascunho documental preparado, não integrado. Não há ABI/syscall estável definida nesta entrega.

## Nomes exigidos
Crates mokos-*, kernel mokos.elf, shell mok, scripts .mks, fontes .mkl, compilador mklc, pacotes mklpkg. ESP: caminho EFI/mokos; entrada UEFI MokOS; rótulos MOKOS_ROOT e MOKOS_LIVE. ISO mokos-<versão>-<arch>.iso + .sha256 + assinatura.

## Limite do M0
Contrato de boot ainda não aprovado: arquitetura, formato de imagem, ponto de entrada, mapa de memória, framebuffer, console e estado dos serviços UEFI devem constar de ADR antes de qualquer código. Não fixar ABI de kernel/userspace nesta fase.

## Entregas entre frentes
- Ideação: alternativas, recomendação, crítica, custo de reversão.
- Pesquisa: links primários, fatos separados de inferências, relatório independente.
- Orquestrador: decisão provisória em ADR e objetivo para cada líder.
- Rust/Assembly: contrato acordado por arquivo antes de desenvolver em paralelo.
- Build: manifesto de entradas, versões, comandos e hashes.
- Testador: comando executado, saída/log, versão do artefato e veredito por critério.
- Integração: somente entrega aceita pelo líder e Testador, com reexecução independente.

## Classificação
Verificado: evidência executada ou documento de origem identificado.
Suposição: inferência arquitetural sem prova experimental.
Não testado: comportamento ou comando ainda não executado.

## Adendo documental v0.1 — posterior à revisão base
Estado: preparado, não integrado; sem ABI estável; revisão independente deste adendo não realizada. Prefixos normativos: mokos_ e MOKOS_. ISO híbrida, UEFI obrigatória. A autoridade sobre alterações de interfaces é do Orquestrador; frentes propõem e Integração mantém coerência, sem redefinir protocolos unilateralmente. Uma tarefa futura de boot deve preencher versão de contrato, autoria/ADR, arquitetura, entrada, memória/validade, console, serviços disponíveis e evidência antes de código.
