# Revisão da base de código (`projeto-quiz/index.js`)

## Problemas encontrados

1. **Bug de validação de resposta**
   - A função `validarRespostaUsuario` compara a resposta do usuário com `pergunta.pergunta` (texto da pergunta), em vez de comparar com `pergunta.resposta` (gabarito).
   - Efeito: o jogador praticamente nunca pontua, mesmo respondendo o ano correto.

2. **Dado histórico inconsistente (potencial bug de conteúdo)**
   - A pergunta sobre o primeiro lançamento de foguete da SpaceX usa resposta `2017`, mas o primeiro lançamento da SpaceX (Falcon 1) ocorreu em **2006**.
   - Efeito: resposta correta do usuário tende a ser marcada como errada.

3. **Mutação do array global de perguntas**
   - `embaralharArray` usa `sort` diretamente no array recebido, mutando `questoes` globalmente.
   - Efeito: comportamento mais difícil de prever em futuras execuções/reuso e maior acoplamento.

4. **Cobertura de testes inexistente**
   - O projeto não possui testes automatizados para funções críticas (`embaralharArray`, `validarRespostaUsuario`, `exibirResultado`).
   - Efeito: regressões simples (como a comparação incorreta) passam despercebidas.

## Tarefas sugeridas

### 1) Corrigir erro de digitação
**Tarefa:** Ajustar a string de resultado final de `"Voce é um verdadeiro nerd!"` para `"Você é um verdadeiro nerd!"` (e revisar outras mensagens para acentuação/padronização, ex.: "aleatórias").

### 2) Corrigir bug
**Tarefa:** Corrigir `validarRespostaUsuario` para comparar com `pergunta.resposta` e normalizar entrada do usuário (ex.: `trim`) antes da comparação.

### 3) Ajustar comentário/discrepância de documentação
**Tarefa:** Atualizar comentários que fixam valores no texto (ex.: "retorna 10 perguntas") para refletirem o parâmetro `quantidade_questoes`, evitando documentação divergente do comportamento real.

### 4) Melhorar teste
**Tarefa:** Criar suíte de testes unitários (Jest ou Node test runner) cobrindo:
- validação correta de resposta (`resposta` vs `pergunta`);
- quantidade de itens retornados por `embaralharArray` sem mutar a coleção original;
- faixas de pontuação/mensagens de `exibirResultado`.
