# A-SOURCES — evidência do executor

Consulta documental em 2026-11-04; não substitui TEST_REPORT independente.

## Entradas lidas integralmente

- C:/Users/20260210-ieg/Desktop/MokOS/AGENTS.md
- C:/Users/20260210-ieg/Desktop/MokOS/agents/02-pesquisa/executor.md
- C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/83df6a95-1b9f-49b8-9fd6-6f5fd8041c88/work/02-pesquisa/A-SOURCES/TASK.md
- C:/Users/20260210-ieg/.agents/skills/maestri/SKILL.md
- AGENTS.md e role.json do próprio sandbox.

Método: Get-Content -Raw; leituras posteriores UTF8 para acentos. maestri list retornou este agente como Pesquisa · Pesquisador, conectado a Líder pesquisa e Pesquisa · Verificador. Sem criação de agentes.

## Índice de fontes efetivamente acessadas

URLs completas estão junto das afirmações em REPORT.md. Consulta via ferramenta web, sem salvar páginas ou baixar binários.

| IDs | Documento/seção consultada | Resultado da leitura |
|---|---|---|
| K1 | Linux Building External Modules / Introduction | Acessível; base de modularidade |
| K2 | seL4 About / What is seL4 | Acessível; descrição de microkernel |
| B1 | LLVM Target-Independent Code Generator | Acessível; arquitetura de codegen |
| B2 | Cranelift / apresentação e Attributes | Acessível; implementação, alvos e objetivos |
| M1 | Rust Book / What Is Ownership | Acessível; categorias e regras |
| M2 | Rustonomicon / FFI | Acessível; fronteira com código externo |
| M3 | std::rc / descrição do módulo | Acessível; Rc, Arc, Weak e ciclos |
| U1 | Limine PROTOCOL.md / ABIs, revisões, requests | Acessível; protocolo em branch móvel trunk |
| U2 | UEFI 2.11 / Boot Services | Acessível; contrato pré/pós ExitBootServices |
| V1 | Ventoy Get Started / instalação e uso | Acessível; instalação prévia |
| V2 | Ventoy Memdisk / Scope | Acessível; limites de imagem e remontagem |
| E1 | QEMU Introduction / Virtualisation Accelerators | Acessível; tabela por host |
| E2 | QEMU WHPX / Prerequisites, Minimum OS, Quick Start | Acessível; requisitos separados por ISA |
| E3 | Microsoft WSL Configuration / nestedVirtualization | Acessível; opção não comprova KVM local |
| E4 | QEMU Arm virt / Supported devices | Acessível; plataforma virtual, UART, versões |
| E5 | QEMU i440fx PC / Peripherals | Acessível; serial e BIOS padrão |
| E6 | TianoCore edk2 OvmfPkg README | Acessível; firmware UEFI virtual |

Limitações: docs master/trunk/latest e páginas sem versão fixada podem mudar; não equivalem às ferramentas locais. QEMU master consultado se apresenta como documentação 11.1.50, sem inferência sobre instalação local. UEFI 2.10 retornou 403, substituída por 2.11 acessível; primeira URL docs.sel4 de overview falhou, substituída pelo site oficial About. URL antiga de wiki OVMF redirecionou à raiz; usada a README oficial OvmfPkg. Página memorymanagement indisponível foi descartada. Não apoiar conclusões nessas tentativas falhas.

## Limites da evidência

VD significa suporte documental observado pelo autor, sujeito à conferência do Verificador. Não foram rodados comandos de build, testes, QEMU, WSL, KVM ou Ventoy. Estado WSL/raiz Git é informação herdada explicitamente da TASK. Observação de modelo: role.json sem campos correspondentes e consulta Get-ChildItem Env: filtrada por MODEL|REASON|EFFORT sem entradas; seletor não exposto. Não foi aberta configuração privada nem procurado segredo.
