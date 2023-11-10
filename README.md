# Tagarela

Objetivo do projeto é desenvolver a melhor LLM especializada na língua portuguesa.

## Planejamento

### Dataset
- [ ] Criar uma lista de fontes para a construção do dataset
- [ ] Criar estratégias de filtro para garantir a qualidade dos exemplos do dataset
- [ ] Criar estratégias de geração de exemplos artificiais
- [ ] Criar estratégias de tradução de datasets

### Treino
- [ ] Escolher um modelo base (idealmente com licenças permissivas)

### Avaliação
- [ ] Definir quais benchmarks temos interesse
  - [ ] Será que vale a pena traduzir algum benchmark? e.g. O MLBench tem apenas 80 perguntas, daria pra fazer manualmente.
- [ ] Calcular uma _baseline_ com modelos existentes pra termos uma noção do que quermos atingir e passar

## Execução (em breve)

## Notas & ideias
- Procurar o que já há de LLMs em português (lembro de ver alguns modelos baseado no LLaMA, acho que usando Alpaca como estratégia de treino)
- A qualidade do dataset é de suma importância. Se tivermos dados de qualidade, podemos treinar um modelo com um dataset menor
- Como construir o dataset?
  - Scrape textos de alta qualidade em domínio público
  - Gerar datasets artificiais (isso parece funcionar bem pros modelos da família Phi-1)
    - Agora temos acesso ao GPT4-turbo que parece ser uma alternativa melhor que GPT3.5 e mais barata que GPT4 pra gerar o dataset
- Em que queremos focar?
  - Assistente genérico?
  - Assistente focado em código?
  - Temos algum benchmark que queremos focar? e.g. MTBench HumanEval
    - A gente traduziria para pt-br? Ou faríamos a tradução ser parte da tarefa?
- 

## Recursos (recomendo ler)
- [LAION treinou um modelo SOTA em Alemão](https://laion.ai/blog/leo-lm/). Podemos pegar bastante inspiração do processo deles
- [Eval em um benchmark de código](https://github.com/AbanteAI/mentat/blob/main/tests/benchmarks/exercism_practice.py)
- [Zephyr](https://arxiv.org/abs/2310.16944) - Eles usam DPO pra alinhar o modelo, em vez de PPO tradicional (isso parece ser bem mais estável e eficiente pra alinhar modelos depois da fase de SFT)
- [Textbooks are all you need](https://arxiv.org/abs/2306.11644) - Aqui eles mostram como você consegue treinar um modelo bem menor com menos dados e atingir performance competitiva se esses dados forem de alta qualidade 
- [Orca](https://arxiv.org/abs/2306.02707) - Aqui eles seguem uma ideia parecida, mas usando explicações geradas pelo GPT4 pra gerar o dataset
- [OpenAssistant](https://github.com/LAION-AI/Open-Assistant) - eles criaram uma ferramenta bem legal pra coletar dados de conversas (estilo ChatGPT) e usar isso pra treinar modelos. Dataset é aberto tb, podemos usar as conversas em pt-br, apesar de que não são muitas. Podemos tb tentar traduzir algumas conversas pra pt-br
