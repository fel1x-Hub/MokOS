# Índice de agentes do MokOS

```
Orquestrador-Chefe
 ├── 01-ideacao  [Líder | Ideador | Crítico]
 ├── 02-pesquisa  [Líder | Pesquisador | Verificador]
 ├── 03-mok  [Líder | Dev | Testador]
 ├── 04-dev-rust  [Líder | Dev | Testador]
 ├── 05-dev-assembly  [Líder | Dev | Testador]
 ├── 06-dev-c  [Líder | Dev | Testador]
 ├── 07-dev-cpp  [Líder | Dev | Testador]
 ├── 08-moklang  [Líder | Projetista/Dev | Revisor/Testador]
 ├── 09-otimizacao  [Líder | Engenheiro de Performance | Benchmarker]
 ├── 10-integracao  [Líder | Integrador | Testador de Sistema]
 └── 11-build-iso-instalador  [Líder | Dev | Testador]
```

Cada frente fica em `agents/<slug>/{lider,executor,testador}.md`. Regras comuns: `AGENTS.md`.

| Frente | Líder | Executor | Testador |
|---|---|---|---|
| Ideação | Líder (TOP) | Ideador (TOP) | Crítico (TOP (modelo diferente do Ideador, se houver)) |
| Pesquisa | Líder (TOP) | Pesquisador (TOP com busca na web) | Verificador (MEDIO) |
| Mok (shell e .mks) | Líder (TOP) | Dev (MEDIO) | Testador (MEDIO) |
| Dev Rust | Líder (TOP) | Dev (TOP) | Testador (TOP (diferente do Dev, se possível)) |
| Dev Assembly | Líder (TOP) | Dev (TOP) | Testador (TOP (diferente do Dev, se possível)) |
| Dev C | Líder (TOP) | Dev (MEDIO) | Testador (MEDIO) |
| Dev C++ | Líder (TOP) | Dev (MEDIO) | Testador (MEDIO) |
| Moklang (.mkl) | Líder (TOP) | Projetista/Dev (TOP) | Revisor/Testador (MEDIO (diferente do Projetista/Dev)) |
| Otimização | Líder (TOP) | Engenheiro de Performance (TOP) | Benchmarker (MEDIO) |
| Integração | Líder (TOP) | Integrador (TOP) | Testador de Sistema (MEDIO) |
| Build, ISO e Instalador | Líder (TOP) | Dev (TOP) | Testador (TOP (diferente do Dev, se possível)) |
