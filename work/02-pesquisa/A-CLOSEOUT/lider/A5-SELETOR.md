# A5 — inventário observável do seletor nativo

Verificado em 2026-11-05 pelo Líder, no terminal ocioso Pesquisa · Verificador, diretório C:/Users/20260210-ieg/Desktop/MokOS/.maestri/roles/9751366c-dc0d-44c3-87ff-0a261af72704. Fonte: saída real do seletor `/model` do Codex no terminal, acessado via maestri; nenhum catálogo de outra ferramenta usado como prova.

Sequência executada: `maestri list`; `maestri check 'Pesquisa · Verificador'`; `maestri ask 'Pesquisa · Verificador' --raw '/model'`; `maestri ask 'Pesquisa · Verificador' --raw '\n'`; `maestri ask 'Pesquisa · Verificador' --raw '\e'`.

Transcrição relevante da saída real:

```text
Select Model and Effort
  1. GPT-6.1-Sol              Latest workhorse model for coding and everyday work.
  2. GPT-6-Astra              Frontier intelligence for the most demanding work.
› 3. GPT-6.1 Terra (current)  GPT-6.1 Terra Codex model.
  4. GPT-6-Sol                Previous generation workhorse model.
  5. GPT-6-Luna               Fast and affordable model for easier tasks.
  6. GPT-5.6-Sol              Older generation workhorse model.
  7. GPT-5.6-Terra            Older balanced model for straightforward work.
  8. GPT-5.6-Luna             Older fast and efficient model.
  enter select · esc back
```

Verificado: TOP Sol aparece como `GPT-6.1-Sol` (também há `GPT-6-Sol`); MEDIO Terra como `GPT-6.1 Terra`; RAPIDO solicitado aparece como `GPT-6-Luna`, opção 5. Variantes antigas Sol/Terra/Luna também listadas conforme transcrição. A descrição comercial transcrita não é evidência independente de custo.

Verificado após Escape: seletor fechado e rodapé `GPT-6.1 Terra high` preservado. Nenhum modelo selecionado, nenhuma atribuição alterada, nenhum novo ciclo técnico, novo nó ou reinício. Não testado: execução em Luna, runtime interno e preços.
