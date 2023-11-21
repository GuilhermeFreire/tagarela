# Tagarela

Objetivo do projeto é desenvolver a melhor LLM especializada na língua portuguesa.

## Planejamento

### Dataset
- [ ] Criar uma lista de fontes para a construção do dataset
- [ ] Criar estratégias de filtro para garantir a qualidade dos exemplos do dataset
- [ ] Criar estratégias de geração de exemplos artificiais
- [ ] Criar estratégias de tradução de datasets
- [ ] Certificar que o dataset não tem duplicatas

### Treino
- [ ] Escolher um modelo base (idealmente com licenças permissivas)
- [ ] Definir híper-parametros pro treino (podemos pegar inspiração de vários lugares e partir daí)
- [ ] Decidir que framework usar pra treinar o modelo (tendo em vista eficiência e facilidade de uso)

### Avaliação
- [ ] Definir quais benchmarks temos interesse
  - [x] Será que vale a pena traduzir algum benchmark? e.g. O MLBench tem apenas 80 perguntas, daria pra fazer manualmente.
- [ ] Calcular uma _baseline_ com modelos existentes pra termos uma noção do que quermos atingir e passar
- [ ] Traduzir o [BIG-Bench-Hard](https://github.com/suzgunmirac/BIG-Bench-Hard) pra pt-br

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
  - Temos algum benchmark que queremos focar? e.g. MTBench, HumanEval
    - A gente traduziria para pt-br? Ou faríamos a tradução ser parte da tarefa?
- Que tipo de conteúdo queremos que o modelo saiba?
  - Constituição brasileira?
  - Pares de descrições e código em pt-br?
  - Livros de domínio público?
  - Notícias?
- Estamos procurando um dataset na ordem de pelo menos 65B de tokens (tamanho do dataset do LAION pra fazer o Llama 2
aprender alemão). O pessoal to Phi-1 usa um dataset de 7B de tokens, com um dataset pra SFT de 200M 
- LAION tb usa datasets de poemas e músicas em alemão (eles geram o dataset com GPT4, mas acho que podemos ver se existem poemas e músicas em domínio público que possamos usar) O dataset tem 400+500 exemplos juntos apenas
- Uma coisa interessante que observei é que você consegue manter muito das habilidades de fazer tarefas mesmo se o
modelo for treinado em outra língua. Por exemplo, no meu caso, estava fine-tuning um modelo pra melhorar a escrita de
textos, todo o dataset de treino era em inglês. Só de curiosidade, eu coloquei um input em português e o modelo fez a tarefa perfeitamente (a saída estava em inglês, mas não precisei traduzir o input nem nada)

#### Lista de Datasets potencialmente relevantes
- [Open Platypus](https://huggingface.co/datasets/garage-bAInd/Open-Platypus) -> [OpenSchnabeltier](https://huggingface.co/datasets/LeoLM/OpenSchnabeltier) traduzido pra alemão
- [OpenAssistant](https://huggingface.co/datasets/OpenAssistant/oasst_top1_2023-08-25) (acho que tem uma versão mais autalizada atualmente) -> [OpenAssistant-DE](https://huggingface.co/datasets/OpenAssistant/OASST-DE) traduzido pra alemão
- [OSCAR-2301](https://huggingface.co/datasets/oscar-corpus/OSCAR-2301)

## Recursos (recomendo ler)
- [LAION treinou um modelo SOTA em Alemão](https://laion.ai/blog/leo-lm/). Podemos pegar bastante inspiração do processo deles
- [Eval em um benchmark de código](https://github.com/AbanteAI/mentat/blob/main/tests/benchmarks/exercism_practice.py)
- [Zephyr](https://arxiv.org/abs/2310.16944) - Eles usam DPO pra alinhar o modelo, em vez de PPO tradicional (isso parece ser bem mais estável e eficiente pra alinhar modelos depois da fase de SFT)
- [Textbooks are all you need](https://arxiv.org/abs/2306.11644) - Aqui eles mostram como você consegue treinar um modelo bem menor com menos dados e atingir performance competitiva se esses dados forem de alta qualidade 
- [Orca](https://arxiv.org/abs/2306.02707) - Aqui eles seguem uma ideia parecida, mas usando explicações geradas pelo GPT4 pra gerar o dataset
- [OpenAssistant](https://github.com/LAION-AI/Open-Assistant) - eles criaram uma ferramenta bem legal pra coletar dados de conversas (estilo ChatGPT) e usar isso pra treinar modelos. Dataset é aberto tb, podemos usar as conversas em pt-br, apesar de que não são muitas. Podemos tb tentar traduzir algumas conversas pra pt-br
- [Continual Pre-Training of Large Language Models: How to (re)warm your model?](https://arxiv.org/abs/2308.04014) - Usar isso pra tentar mitigar o esquecimento dos dados prévios do modelo, quando fizermos nosso Stage-2 pre-training 
