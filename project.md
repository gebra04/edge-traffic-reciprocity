# Plano de desenvolvimento do estudo

## 1. Tema e contexto

**Título provisório:** Coordenação distribuída de rotas urbanas com reciprocidade entre nós de borda.

Trabalho prático da disciplina de edge computing, desenvolvido em dupla em aproximadamente oito semanas, com disponibilidade informada de 5–10 horas semanais. A distribuição de responsabilidades será definida após o detalhamento das tarefas, distinguindo atividades individuais e decisões conjuntas.

O estudo investiga a tomada de decisão coletiva em uma cidade conectada. Cada região urbana possui um nó de borda que acompanha o trânsito local e negocia com regiões vizinhas a recepção de veículos desviados. Cada nó protege o desempenho de sua região, mas pode aceitar um custo local para ajudar outra região e acumular prioridade em negociações futuras.

O mapa será de um recorte pequeno de Campinas, sujeito à verificação de viabilidade de preparação. A demanda será sintética e controlada: o objetivo não é reproduzir ou prever o trânsito real da cidade.

## 2. Pergunta de pesquisa e objetivos

**Pergunta principal:** em quais condições a cooperação entre nós de borda reduz congestionamentos em comparação com decisões apenas locais, e a reciprocidade melhora a distribuição dos custos entre regiões com perda limitada de eficiência em relação à cooperação sem reciprocidade?

### Objetivo geral

Construir um protótipo distribuído e um experimento reproduzível para comparar estratégias de coordenação de rotas entre regiões urbanas.

### Objetivos específicos

- Implementar nós de borda como processos ou serviços independentes.
- Restringir cada nó ao conhecimento de sua região e a resumos recebidos das vizinhas.
- Implementar negociação para receber tráfego desviado de regiões congestionadas.
- Introduzir um saldo explícito de ajuda entre regiões.
- Avaliar eficiência global e distribuição dos custos locais.
- Apresentar uma visualização simples do trânsito, das negociações e dos saldos.

### Hipóteses a testar

- H1: a cooperação entre bordas melhora o desempenho em situações nas quais decisões exclusivamente locais transferem ou agravam congestionamentos.
- H2: o histórico de reciprocidade distribui melhor o custo de receber desvios, com uma perda de eficiência limitada por uma tolerância previamente definida.

São hipóteses, não resultados esperados obrigatórios. A ausência de benefício ou a superioridade da cooperação sem reciprocidade também constituem resultados válidos.

## 3. Escopo e premissas

- Usar um recorte real de Campinas, inicialmente com três ou quatro regiões, ajustável após a inspeção do mapa.
- Simular veículos que seguem integralmente as rotas recomendadas.
- Concentrar a autonomia e a negociação nos nós de borda, não nos veículos individuais.
- Trabalhar com demanda controlada e rotas alternativas viáveis entre regiões.
- Acumular o saldo de ajuda durante cada execução e zerá-lo no início de uma nova execução, sem expiração na primeira versão.
- Permitir que o saldo altere decisões dentro de uma tolerância de custo; não usar apenas desempate nem obrigação irrestrita de retribuir.
- Priorizar a execução distribuída e um algoritmo explícito de complexidade limitada.

Não fazem parte do núcleo: decisões de direção e mudança de faixa, percepção cooperativa, sensores, treinamento de modelos de aprendizado, motoristas estratégicos, implantação em veículos reais ou reprodução de toda Campinas. Incidentes temporários, adesão parcial, atrasos de rede e envelhecimento dos créditos são extensões possíveis.

## 4. Arquitetura proposta

### Simulação de mobilidade

Um simulador mantém vias, veículos, demanda e deslocamentos. Sua integração com os serviços deve fornecer a cada borda somente observações locais. O simulador pode manter o estado global internamente para executar o trânsito; esse estado não deve ficar disponível ao algoritmo de decisão das bordas.

### Nós de borda

Cada serviço deve:

1. Observar o trânsito da própria região.
2. Produzir resumos de condições locais para as vizinhas.
3. Solicitar ou oferecer recepção de tráfego desviado.
4. Avaliar propostas segundo custo local, informações compartilhadas e, quando habilitado, reciprocidade.
5. Confirmar acordos e aplicar recomendações de rota por meio da integração com o simulador.
6. Registrar decisões, estimativas, saldos e resultados observados.

Não haverá controlador central com conhecimento global para escolher rotas. Um componente de execução poderá iniciar serviços e sincronizar passos, sem tomar decisões de tráfego. A avaliação poderá usar dados globais, separados do acesso concedido aos agentes.

### Comunicação

Definir mensagens mínimas para estado regional, pedido de desvio, proposta, aceitação ou recusa, confirmação e registro de ajuda. Cada negociação deve possuir identificador, validade e quantidade de tráfego acordada, evitando compromissos duplicados e alterações de saldo contadas duas vezes.

A tecnologia de comunicação e o simulador serão escolhidos após um teste pequeno de integração. A execução em uma única máquina com serviços separados demonstra a arquitetura lógica, mas não comprova desempenho de uma implantação física de edge computing.

## 5. Negociação e reciprocidade

A ajuda consiste em receber veículos desviados de outra região. Seu valor deve refletir o custo de absorver esse tráfego, e não apenas a quantidade de veículos: o mesmo volume pode causar impactos diferentes conforme as condições locais.

Fluxo inicial proposto:

1. Uma borda identifica uma necessidade de desvio e consulta regiões vizinhas.
2. As receptoras estimam o custo local e informam propostas admissíveis.
3. As bordas negociam a alternativa usando a política experimental selecionada.
4. A reciprocidade pode favorecer uma região que ajudou anteriormente, respeitando uma tolerância de custo em relação à alternativa de referência da negociação.
5. Após a confirmação e a execução da ajuda, o saldo é atualizado uma única vez.

Antes da implementação, definir em conjunto:

- Indicador usado para estimar custo local e sua unidade.
- Se o saldo será bilateral entre pares ou agregado por região; saldo bilateral é uma opção inicial a avaliar.
- Como custo e volume recebido serão convertidos em créditos.
- Qual alternativa serve de referência à tolerância e como lidar com ausência de alternativa viável.
- Momento da atualização do saldo e tratamento de execução parcial ou cancelada.
- Frequência de negociação e duração dos compromissos.
- Mecanismo para evitar redirecionamentos repetidos dos mesmos veículos.

A tolerância é aplicada à estimativa disponível durante a negociação. O custo efetivamente observado deverá ser medido separadamente: um limite na estimativa não garante o mesmo limite no resultado global.

## 6. Desenho experimental

### Estratégias comparadas

| Estratégia | Informação e comportamento |
|---|---|
| Local | Cada borda decide com informações locais, sem negociação entre regiões. |
| Cooperação sem reciprocidade | As bordas trocam resumos e negociam considerando o estado atual, sem histórico de ajuda. |
| Cooperação com reciprocidade | Mesma base cooperativa, acrescentando saldo de ajuda e tolerância de custo. |

Manter iguais, sempre que aplicável, mapa, demanda, limites de atuação, frequência de decisão e estimador de custo. A comparação entre as duas estratégias cooperativas deve isolar o efeito da reciprocidade.

### Cenários

1. **Principal — picos alternados:** regiões diferentes concentram demanda em momentos diferentes, permitindo ajudar e depois solicitar ajuda.
2. **Contraponto — demanda persistentemente desigual:** uma região precisa de ajuda com maior frequência, testando se o mecanismo depende de reciprocidade conveniente.
3. **Referência — demanda moderada:** verificar se o mecanismo gera desvios ou negociações desnecessárias quando há pouca pressão.
4. **Extensão — incidente temporário:** reduzir a capacidade de uma via e observar a recuperação, se houver tempo.

Repetir os experimentos com diferentes sementes, usando as mesmas sementes entre estratégias. Definir a quantidade de repetições após medir o tempo de execução e a variabilidade no piloto. Explorar poucos valores de tolerância, incluindo zero como referência, sem ampliar excessivamente a matriz experimental.

### Métricas

- Tempo médio de viagem e distribuição dos tempos de viagem.
- Viagens concluídas, veículos ainda na rede e demanda não inserida, evitando favorecer políticas que deixem viagens difíceis sem conclusão.
- Atraso ou tempo acumulado de congestionamento por região.
- Distribuição do custo adicional associado à cooperação entre regiões.
- Volume de tráfego recebido e encaminhado por região.
- Evolução dos saldos e número de acordos aceitos ou recusados.

Definir como atribuir o custo regional: por exemplo, atraso acumulado nos trechos de cada região, com normalização pela demanda ou capacidade quando apropriado. Separar desigualdade estrutural do mapa de desigualdade causada pela política. Usar diferenças entre execuções comparáveis como aproximação do impacto da política; não tratar automaticamente todo atraso observado como efeito de um desvio específico.

Relatar resultados absolutos e diferenças entre métodos, acompanhados de dispersão entre execuções. Julgar o compromisso entre equilíbrio e eficiência com critérios definidos antes da análise final. O saldo de créditos não é, por si só, uma medida de justiça ou benefício.

## 7. Pacotes de trabalho

Atribuir responsáveis depois de estimar o esforço de cada pacote. As decisões conceituais e a interpretação dos resultados devem ser conjuntas.

| Pacote | Tarefas | Entrega verificável | Organização sugerida |
|---|---|---|---|
| P1 — Viabilidade | Inspecionar um recorte de Campinas; testar simulador e integração; verificar rotas alternativas | Mapa pequeno com veículos circulando e observações locais acessíveis | Decisão conjunta, testes divisíveis |
| P2 — Protocolo experimental | Definir regiões, demanda, métricas, custo, saldo e tolerância | Especificação curta com exemplos de negociação | Conjunta |
| P3 — Base de mobilidade | Preparar cenários, sementes e estratégia local | Experimento local reproduzível | Responsável a definir |
| P4 — Serviços de borda | Implementar processos, mensagens, estados e logs | Dois nós trocando e confirmando uma proposta | Responsável a definir |
| P5 — Cooperação | Integrar decisão de rota e negociação sem saldo | Segundo método funcionando de ponta a ponta | Integração conjunta |
| P6 — Reciprocidade | Implementar atualização de saldo e tolerância | Terceiro método e verificações do mecanismo | Responsável a definir; revisão conjunta |
| P7 — Avaliação | Automatizar execuções e produzir métricas e gráficos | Comparação reproduzível dos três métodos | Execuções divisíveis; interpretação conjunta |
| P8 — Comunicação | Criar visualização, documentação e apresentação | Demonstração e relatório final | Responsáveis a definir; revisão conjunta |

A revisão bibliográfica será enxuta e orientada às escolhas do projeto: coordenação de tráfego em edge computing, roteamento distribuído e reciprocidade. Ela deverá contextualizar o estudo e evitar alegações de novidade sem verificação, sem substituir a entrega prática.

## 8. Cronograma de referência

| Semana | Foco | Marco |
|---|---|---|
| 1 | Viabilidade, leitura dirigida e seleção do mapa | Recorte de Campinas e integração mínima validados |
| 2 | Cenários, métricas, interfaces e estratégia local | Base reproduzível e especificação acordada |
| 3 | Serviços independentes e mensagens | Negociação mínima entre bordas |
| 4 | Cooperação sem reciprocidade | Segundo método integrado ao trânsito |
| 5 | Saldo e tolerância de custo | Terceiro método integrado |
| 6 | Pilotos, correções e visualização simples | Matriz experimental estabilizada |
| 7 | Experimentos e análise | Gráficos e comparação dos resultados |
| 8 | Consolidação, relatório e apresentação | Entrega reproduzível e demonstração |

Ajustar o cronograma ao prazo oficial da disciplina. Priorizar os três métodos e a avaliação antes de extensões. A visualização deve reutilizar os registros do sistema e evitar a construção de uma aplicação complexa.

## 9. Verificação e critérios de conclusão

- Os serviços de borda executam separadamente e não consultam estado global para decidir.
- As três políticas podem ser executadas por configuração no mesmo ambiente experimental.
- As rotas propostas são válidas e os acordos não comprometem a mesma oferta de recepção mais de uma vez.
- Saldos são atualizados conforme a convenção especificada, inclusive em cancelamentos ou execução parcial.
- A regra de tolerância é verificável em exemplos pequenos antes dos experimentos completos.
- Configurações, sementes, versões e resultados brutos são preservados.
- O relatório distingue estimativas usadas pelo algoritmo dos custos observados.
- Resultados negativos e limitações são apresentados sem depender de uma hipótese confirmada para concluir o trabalho.

## 10. Riscos e contenção de escopo

| Risco | Resposta planejada |
|---|---|
| Preparação do mapa de Campinas consumir muito tempo | Reduzir a área e simplificar a demanda; discutir alternativa somente se o recorte continuar inviável |
| Regiões sem rotas alternativas úteis | Verificar conectividade e possibilidades de desvio na primeira semana |
| Reciprocidade não melhorar os resultados | Analisar condições e custos; manter o resultado como conclusão válida |
| Oscilação de rotas ou negociação excessiva | Estabelecer validade dos acordos e intervalo mínimo entre novas decisões |
| Métricas confundirem congestionamento prévio com custo da cooperação | Usar referências comparáveis e explicitar a atribuição regional dos custos |
| Integração distribuída atrasar o projeto | Limitar mensagens e manter um cenário mínimo integrado desde cedo |
| Visualização competir com os experimentos | Mostrar mapa, estados e saldos com recursos simples, priorizando a avaliação |

## 11. Próximos passos

1. Conferir requisitos e prazo oficial da disciplina.
2. Selecionar e testar um recorte de Campinas e um simulador adequado.
3. Fechar as definições de custo regional, saldo, tolerância e mensagens.
4. Estimar os pacotes de trabalho e distribuir responsabilidades individuais e conjuntas.
5. Implementar a menor execução completa: simulação, duas bordas, uma negociação e seu registro.

O nome curto do repositório permanece em aberto; não interfere no escopo do estudo.
