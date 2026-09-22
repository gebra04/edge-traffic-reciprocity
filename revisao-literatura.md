# Revisão exploratória da literatura — coordenação regional de rotas na borda com reciprocidade

**Data da busca:** 22 de setembro de 2026.  
**Projeto de referência:** nós de borda por região urbana, informação dinâmica local e resumos de vizinhos, negociação para receber tráfego desviado, histórico de ajuda e tolerância de custo. Veículos seguem as recomendações. Experimento em um recorte de Campinas, em dupla, durante aproximadamente oito semanas.

## 1. Conclusão principal

A proposta se encontra na interseção de linhas de pesquisa já consolidadas: roteamento cooperativo com edge/fog computing; controle e orientação de rotas entre regiões; equilíbrio entre justiça e eficiência; e reciprocidade ou créditos não monetários para alocar recursos de mobilidade.

**Não seria defensável apresentar como novidade geral o uso de edge computing para coordenar rotas, a cooperação entre regiões ou a introdução de justiça no trânsito.** Há antecedentes diretos para esses componentes, especialmente [R01](https://doi.org/10.1016/j.compeleceng.2023.108668), [R14](https://doi.org/10.1016/j.trc.2023.104359) e [R17](https://doi.org/10.1016/j.ejcon.2021.06.024).

**Não foi localizado, no conjunto consultado, um trabalho que reúna explicitamente todos os elementos do projeto:** saldos de ajuda pertencentes às regiões, coordenação entre bordas sem controlador global de rotas, informação dinâmica limitada aos vizinhos, compensação temporal por absorver desvios e preferência limitada por uma tolerância de custo. Isso identifica um recorte candidato, não comprova ineditismo. Parte dos trabalhos mais próximos só pôde ser examinada por resumo e trechos públicos.

A contribuição mais segura para a disciplina é uma **avaliação experimental reproduzível do valor — e dos limites — da memória de cooperação entre regiões**, em uma implementação distribuída. É possível que um método simples sem créditos seja tão bom quanto ou melhor. Esse resultado também responderia à pergunta de pesquisa.

## 2. Como a busca foi realizada

Foi feita uma revisão exploratória extensa, com busca por conceitos, títulos exatos e referências de trabalhos relevantes. Foram selecionados **24 trabalhos: 22 no núcleo da discussão e 2 complementares sobre reciprocidade entre veículos e comportamento humano**. O conjunto inclui artigos publicados e dois preprints identificados como tais.

Foram consultadas páginas de editoras e periódicos, repositórios institucionais, páginas dos autores e arXiv. Registros de DOI no Crossref ajudaram a conferir parte dos metadados; houve limitação de taxa em parte dessas consultas. Não foi feita exportação sistemática de Scopus ou Web of Science, nem protocolo PRISMA. A lista não pretende enumerar todos os artigos existentes.

### Famílias de consultas utilizadas

- `"traffic routing" "edge computing" distributed cooperative`
- `"vehicle routing" "edge computing" congestion cooperative`
- `"traffic management" "fog" "rerouting" distributed`
- `"Cross-domain cooperative route planning"`
- `"distributed" "perimeter" "route guidance" control`
- `"multi-region" traffic "incentive"`
- `"perimeter control" "game" "cooperative"`
- `"traffic" "regions" "Nash bargaining" control`
- `"traffic routing" "fairness" "bounded"`
- `"An MFD approach to route guidance with consideration of fairness"`
- `"traffic routing" "karma" credits`
- `"traffic" "regions" "reciprocity" routing credits`
- `"inter-region" "reciprocity" traffic routing`
- `"traffic" "regions" "tit-for-tat"`
- `"rerouting" "reciprocity"`
- `"credit" "regional controllers" traffic`
- Consultas adicionais com 2025 e 2026 para verificar trabalhos recentes.

**Critérios de seleção:** relação com rotas rodoviárias, decisão regional, arquitetura distribuída, justiça ou reciprocidade; fonte primária verificável; mecanismo ou resultado útil para posicionar o projeto.

**Exclusões importantes:** roteamento de pacotes, offloading de tarefas sem controle das rotas dos veículos, créditos de telecomunicações e reciprocidade administrativa de habilitação/pedágio. Muitas buscas por “traffic”, “routing” e “credit” retornam esses assuntos, que não constituem antecedentes diretos do problema rodoviário.

### Níveis de acesso nas fichas

- **T:** texto integral acessível; foram consultadas seções relevantes, sem reprodução experimental.
- **P:** resumo e trechos públicos do próprio artigo; métodos ou resultados completos não verificados.
- **R:** resumo oficial ou registro institucional/autoral.

“Ausente do material consultado” não equivale a “comprovadamente ausente do artigo”. As limitações abaixo distinguem restrições descritas pelos autores de diferenças observadas em relação ao projeto.

## 3. Trabalhos sobre roteamento cooperativo e edge/fog

### R01 — Xue et al. (2023)

**Cross-domain cooperative route planning for edge computing-enabled multi-connected vehicles.** *Computers and Electrical Engineering*, 108, 108668. **Acesso: P.** [Artigo e DOI](https://doi.org/10.1016/j.compeleceng.2023.108668).

- **Abordagem:** roteamento cooperativo apoiado em MEC, balanceando tráfego entre domínios e minimizando a probabilidade de congestionamento; algoritmo CRPA por pontos interiores.
- **Avaliação:** SUMO, MATLAB e TraCI. O resumo apresenta reduções do tempo médio de viagem de 4,85%, 15,62%, 35,54% e 63,11% contra diferentes comparadores. A correspondência detalhada entre percentuais e comparadores não foi confirmada no texto público; não tratar como ganho universal.
- **Relação:** antecedente muito direto da arquitetura/aplicação. Os trechos mostram veículos, bordas e nuvem; não classificá-lo como totalmente descentralizado sem ler o restante. Saldo de ajuda regional não foi identificado no material acessado.

### R02 — Brennand et al. (2019), FOXS

**Towards a Fog-Enabled Intelligent Transportation System to Reduce Traffic Jam.** *Sensors*, 19(18), 3916. **Acesso: T.** [Texto integral](https://www.mdpi.com/1424-8220/19/18/3916), [DOI](https://doi.org/10.3390/s19183916).

- **Abordagem:** cloudlets associados a RSUs coletam dados regionais e recomendam rotas dentro de sua área de conhecimento; escolha probabilística entre alternativas reduz concentração nos mesmos caminhos.
- **Resultados:** os autores reportam reduções máximas de 70% no tempo parado e 30% no atraso da aplicação, em seu conjunto de cenários/comparadores. Tempo parado não é tempo total de viagem.
- **Relação:** referência prática para coleta local, divisão territorial e integração mobilidade/comunicação. Também limita o aumento do comprimento da rota, antecipando a preocupação com desvios excessivos.
- **Diferença:** o mecanismo examinado não usa um saldo temporal de favores entre regiões.

### R03 — Du et al. (2024; online em 2023)

**Dynamic urban traffic rerouting with fog-cloud reinforcement learning.** *Computer-Aided Civil and Infrastructure Engineering*, 39, 793–813. **Acesso: T.** [Texto integral](https://onlinelibrary.wiley.com/doi/full/10.1111/mice.13115).

- **Abordagem:** GAQ-EBkSP combina aprendizado por reforço com atenção em grafos e seleção de caminhos balanceada por entropia, em arquitetura fog-cloud.
- **Resultados:** em testes de Manhattan, relata aumento de 2,4 m/s na velocidade média em comparação com GCQ-EBkSP e menor ocorrência de congestionamento severo nos cenários avaliados.
- **Diferença:** assume controle centralizado com execução distribuída; não equivale à troca apenas entre vizinhos.
- **Limitações declaradas:** explorar número/tamanho das áreas fog, intervalos de atualização, atributos das vias e resposta dos motoristas. É útil para estudar a transferência de congestionamento causada pelo próprio rerroteamento.

### R04 — Wang, Wen e Chao (2023)

**Hierarchical Cooperation and Load Balancing for Scalable Autonomous Vehicle Routing in Multi-Access Edge Computing Environment.** *IEEE Transactions on Vehicular Technology*. **Acesso: R.** [Registro institucional](https://scholar.nycu.edu.tw/en/publications/hierarchical-cooperation-and-load-balancing-for-scalable-autonomo/), [DOI](https://doi.org/10.1109/TVT.2023.3236783).

- **Abordagem:** cooperação hierárquica e balanceamento entre MECs para processar solicitações de rotas de CAVs em ambiente com gerenciamento autônomo de interseções.
- **Resultados:** capacidade de processamento de rotas 15,68 vezes maior que a centralizada e redução de 14,51% no tempo de computação por balanceamento.
- **Cuidado:** são resultados de capacidade computacional, não redução de congestionamento de 15,68 vezes.
- **Relação:** fundamenta o papel operacional da borda. Não foi identificado no resumo um mecanismo de compensação pelo custo rodoviário de receber desvios.

### R05 — Nguyen e Jung (2023; online em 2022)

**ACO-based traffic routing method with automated negotiation for connected vehicles.** *Complex & Intelligent Systems*, 9, 625–636. **Acesso: T.** [Texto integral](https://doi.org/10.1007/s40747-022-00833-3).

- **Abordagem:** feromônio invertido desestimula vias congestionadas; I-EPOS coordena escolhas entre rotas alternativas.
- **Avaliação:** Python/SUMO, dois mapas reais de Seul e dez sementes. A negociação melhora tempo de viagem e consumo nos testes.
- **Diferença:** agentes representam veículos; a coordenação usa uma árvore e informação agregada, não saldos de ajuda regional.
- **Limitação declarada:** o trabalho não avalia o desempenho da comunicação. Os autores sugerem integração com simulador de rede. A hipótese inicial de veículos altruístas é complementada por testes de adesão parcial.

### R06 — Pan, Popa e Borcea (2017), DIVERT

**DIVERT: A Distributed Vehicular Traffic Re-Routing System for Congestion Avoidance.** *IEEE Transactions on Mobile Computing*, 16(1), 58–72. **Acesso: R.** [Registro institucional](https://digitalcommons.njit.edu/fac_pubs/10049/), [Manuscrito dos autores](https://web.njit.edu/~borcea/papers/ieee-tmc16.pdf), [DOI](https://doi.org/10.1109/TMC.2016.2538226).

- **Abordagem:** transfere computação de rotas para os veículos e usa mensagens VANET para decisões cooperativas.
- **Resultados:** relata redução de 99,99% na carga de CPU e 95% na carga de rede do servidor; desempenho de viagem ligeiramente inferior ao centralizado, mas superior ao caso sem rerroteamento.
- **Diferença:** é híbrido, mantendo servidor para uma visão global de trânsito. Mostra que distribuir computação e eliminar conhecimento global são decisões diferentes. Não equivale à reciprocidade entre bordas.

## 4. Trabalhos sobre decisões e controle entre regiões

**Distinção de atuação:** controle de perímetro regula a entrada de veículos, frequentemente por semáforos; orientação de rotas altera o caminho escolhido. Ambos lidam com fluxos regionais, mas um controlador de semáforo não é um baseline de roteamento diretamente intercambiável.

### R07 — Haddad e Mirkin (2017)

**Coordinated distributed adaptive perimeter control for large-scale urban road networks.** *Transportation Research Part C*, 77, 495–515. **Acesso: P.** [Artigo](https://doi.org/10.1016/j.trc.2016.12.002).

- **Abordagem:** controladores adaptativos regionais com informação local e sinal de referência de um coordenador superior; modelagem por MFD, diagrama macroscópico que relaciona acumulação e produção/fluxo.
- **Resultados:** apresenta análise de estabilidade e seguimento assintótico sob as hipóteses do modelo.
- **Diferença:** existe coordenação superior e a atuação é sobre perímetros. A restrição informacional regional já aparece aqui; não é novidade isolada do projeto.

### R08 — Kim, Tak, Lee e Yeo (2019)

**Distributed Model Predictive Approach for Large-Scale Road Network Perimeter Control.** *Transportation Research Record*, 2673(5). **Acesso: R.** [Artigo](https://doi.org/10.1177/0361198119838521).

- **Abordagem:** agentes locais compartilham informação necessária e decidem simultaneamente nas fronteiras. Pesos condicionais alternam objetivos egoístas e cooperativos.
- **Resultado:** os estudos de caso superam controle fixo e estratégia puramente egoísta.
- **Relação:** muito próximo da tensão “proteger minha região versus cooperar”. O resumo não descreve saldo de ajuda acumulado; é necessário conferir o texto completo antes de excluir qualquer mecanismo equivalente.

### R09 — Leclercq, Ladino e Bécarie (2021)

**Enforcing optimal routing through dynamic avoidance maps.** *Transportation Research Part B*, 149, 118–137. **Acesso: R, página do autor.** [Resumo autoral](https://www.andresladino.com/publication/2021-tr-b/), [DOI](https://doi.org/10.1016/j.trb.2021.05.002).

- **Abordagem:** converte condições regionais em níveis de evitação enviados aos sistemas de navegação; também testa cooperação regional.
- **Resultados:** aproximadamente 15% de melhora no tempo total em congestionamento severo, mantendo abaixo de 10% o aumento médio da distância dos veículos desviados, nos testes descritos.
- **Relação:** antecedente direto de controle regional por desvios, sem depender de controlar semáforos.
- **Diferença:** não foi identificado no resumo um histórico de compensação entre regiões. Parâmetros de região e atualização são parte importante da avaliação.

### R10 — Zhou e Gayah (2023)

**Scalable multi-region perimeter metering control for urban networks: A multi-agent deep reinforcement learning approach.** *Transportation Research Part C*, 148, 104033. **Acesso: P.** [Artigo](https://doi.org/10.1016/j.trc.2023.104033).

- **Abordagem:** treinamento centralizado e execução descentralizada com decomposição da função de valor.
- **Resultados:** experimentos com sete regiões mostram desempenho comparável a MPC, resistência a dados inexatos e transferência para condições não vistas.
- **Diferença:** controla fluxos de perímetro e depende de treinamento; não oferece, no material consultado, a contabilidade de ajuda proposta. “Execução descentralizada” não implica ausência de informação global durante a construção da política.

### R11 — Kampitakis e Vlahogianni (2025)

**Decentralized multi-region perimeter control in complex urban environments using reinforcement and imitation learning.** *Transportation Research Part C*, 178, 105253. **Acesso: P.** [Artigo](https://doi.org/10.1016/j.trc.2025.105253).

- **Abordagem:** aprende um controlador global e usa imitação para obter agentes por região ou fronteira, incorporando balanceamento de filas.
- **Avaliação:** SUMO em cerca de 24 km² de Atenas, com 328 interseções semaforizadas. Relata superioridade aos baselines PI/MPC e testa perturbações de demanda e ruído.
- **Relação:** mostra que controle regional descentralizado em mapa real já é estudado em escala relevante.
- **Diferença:** política derivada de conhecimento global e atuação semafórica; não foi identificado saldo de reciprocidade no material consultado.

### R12 — Li et al. (2024)

**Beyond centralization: Non-cooperative perimeter control with extended mean-field reinforcement learning in urban road networks.** *Transportation Research Part B*, 186, 103016. **Acesso: P.** [Artigo](https://doi.org/10.1016/j.trb.2024.103016).

- **Abordagem:** agentes de perímetro e interiores com utilidades próprias; treinamento e execução descentralizados, com aprendizado por reforço de campo médio estendido.
- **Resultados:** análise de aproximação ao ponto fixo de Nash sob hipóteses do modelo e experimentos com simulação CTM.
- **Relação:** a existência de interesses conflitantes entre controladores também possui antecedente explícito.
- **Diferença:** grupos e atuação não coincidem com regiões recebendo desvios por créditos. Existe [corrigendum de autoria/financiamento](https://doi.org/10.1016/j.trb.2024.103097); no texto da correção consultado, não há alteração de resultados.

## 5. Justiça e eficiência: antecedentes decisivos

### R13 — Moshahedi e Kattan (2023)

**Alpha-fair large-scale urban network control: A perimeter control based on a macroscopic fundamental diagram.** *Transportation Research Part C*, 146, 103961. **Acesso: R.** [Artigo](https://doi.org/10.1016/j.trc.2022.103961).

- **Abordagem:** utilidade regional baseada em velocidade média e pesos relacionados às filas; parâmetro de alpha-fairness controla o compromisso distributivo.
- **Resultados:** nos cenários avaliados, melhora a justiça sem degradar eficiência em relação aos controles comparados.
- **Relação:** capacidade viária regional e distribuição dos impactos já são objetos de otimização conjunta.
- **Diferença:** atua sobre fluxos de perímetro. O mecanismo descrito não é uma dívida temporal por favores entre bordas.

### R14 — Hosseinzadeh, Moshahedi e Kattan (2023)

**An MFD approach to route guidance with consideration of fairness.** *Transportation Research Part C*, 157, 104359. **Acesso: R; artigo identificado como aberto, mas o corpo integral não foi recuperado nesta busca.** [Artigo](https://doi.org/10.1016/j.trc.2023.104359).

- **Abordagem:** dois esquemas de orientação de rotas, com justiça proporcional e controle antecipatório, em uma rede dividida em regiões e modelada por MFD.
- **Resultados:** relata maior homogeneidade mantendo eficiência; os esquemas funcionam nos níveis de adesão examinados, inclusive 30%.
- **Relação:** é um dos antecedentes mais importantes: não apenas controle regional, mas rotas e justiça juntas.
- **Diferença a investigar:** informação necessária ao controle e eventual memória temporal. O resumo não descreve créditos regionais. Deve ser lido integralmente antes de fechar uma alegação de originalidade.

### R15 — Jalota et al. (2023)

**Balancing fairness and efficiency in traffic routing via interpolated traffic assignment.** *Autonomous Agents and Multi-Agent Systems*, 37, artigo 32. **Acesso: R.** [Artigo](https://doi.org/10.1007/s10458-023-09616-7), [Repositório MIT](https://dspace.mit.edu/entities/publication/7b0ae8d0-e055-4463-ba7d-a5b2e554dc69).

- **Abordagem:** I-TAP interpola objetivos de eficiência e justiça, limitando a razão entre tempos de usuários com mesma origem/destino.
- **Resultados:** limites teóricos e avaliação numérica; relata execução ordens de grandeza mais rápida que o algoritmo de referência.
- **Diferença:** justiça entre viajantes de um mesmo par origem/destino não é justiça entre regiões. É uma referência para evitar misturar definições e para justificar a tolerância de custo, não um protocolo edge pronto.

### R16 — Riehl et al. (2026), preprint

**Distributive Perimetral Queue Balancing Mechanisms: Towards Equitable Urban Traffic Gating and Fair Perimeter Control.** arXiv:2604.07840v1. **Acesso: T; publicação revisada por pares não confirmada.** [Texto integral](https://arxiv.org/html/2604.07840v1).

- **Abordagem:** redistribui a capacidade de entrada conforme filas, usando princípios proporcional e max-min.
- **Avaliação:** SUMO/Python, três zonas de San Francisco e dez sementes. O controle básico aumenta fluxo médio em aproximadamente 13% no cenário descrito; o balanceamento acrescenta ganhos distributivos, com efeitos distintos por zona.
- **Relação:** evidencia a necessidade de comparar créditos com uma regra justa simples. Não atribuir os ganhos do controle básico ao componente de justiça.
- **Recurso:** os autores apontam código e cenários em [fair_perimeter_control](https://github.com/DerKevinRiehl/fair_perimeter_control); a executabilidade do repositório não foi verificada.

## 6. Créditos, memória e reciprocidade

### R17 — Salazar, Paccagnan, Agazzi e Heemels (2021)

**Urgency-aware optimal routing in repeated games through artificial currencies.** *European Journal of Control*, 62, 22–32. **Acesso: T, versão dos autores.** [DOI](https://doi.org/10.1016/j.ejcon.2021.06.024), [Manuscrito](https://arxiv.org/pdf/2011.11595).

- **Abordagem:** viajantes ganham créditos na rota mais lenta e gastam na mais rápida, considerando urgência variável ao longo de viagens repetidas.
- **Resultados:** no modelo estudado, alcança alocação ótima e reduz desconforto percebido em 14–20% ante política ótima que ignora urgência. Não é uma redução de 14–20% no tempo de viagem.
- **Limites:** análise aprofundada em duas rotas paralelas, com hipóteses específicas de comportamento e preços.
- **Relação:** antecedente direto de sacrificar desempenho agora por vantagem futura; os titulares dos créditos são viajantes, não regiões.

### R18 — Elokda et al. (2024; online em 2023)

**A Self-Contained Karma Economy for the Dynamic Allocation of Common Resources.** *Dynamic Games and Applications*, 14, 578–610. **Acesso: T.** [Texto integral](https://doi.org/10.1007/s13235-023-00503-0).

- **Abordagem:** alocação repetida com créditos não monetários que circulam entre agentes; modelagem por jogos populacionais dinâmicos.
- **Resultados:** existência de equilíbrio estacionário sob condições do modelo e análise de eficiência, justiça, heterogeneidade e redistribuição.
- **Limites relevantes:** agentes pareados em população grande e consideração de benefícios futuros. As garantias não se transferem automaticamente para três ou quatro regiões fixas de capacidades diferentes.
- **Uso no projeto:** fundamentar regras de ganho, gasto, conservação e validade prática dos créditos. Um simples peso de prioridade não herda as propriedades demonstradas para uma economia de karma.

### R19 — Elokda et al. (online em 2024; fascículo de 2025), CARMA

**CARMA: Fair and Efficient Bottleneck Congestion Management via Nontradable Karma Credits.** *Transportation Science*, 59(2), 340–359. **Acesso: T.** [Texto integral](https://doi.org/10.1287/trsc.2023.0323).

- **Abordagem:** viajantes usam karma para disputar uma faixa rápida de um gargalo; créditos são redistribuídos ao longo dos dias.
- **Resultados:** sob as hipóteses estudadas, apresenta melhoria de Pareto no custo médio de longo prazo e redução de congestionamento comparável à tarifação ótima; desenhos de redistribuição podem superá-la.
- **Diferença:** gargalo e usuários heterogêneos, não rede de bordas regionais. A distribuição inicial e a circulação dos créditos fazem parte do mecanismo; não são detalhes de implementação.

### R20 — Li e Ramezani (2022)

**Quasi revenue-neutral congestion pricing in cities: Crediting drivers to avoid city centers.** *Transportation Research Part C*, 145, 103932. **Acesso: T.** [Manuscrito institucional](https://transportlab.sydney.edu.au/wp-content/uploads/2022/11/YL-MR-TRC2022.pdf), [DOI](https://doi.org/10.1016/j.trc.2022.103932).

- **Abordagem:** pedágios positivos e negativos variam por região e tempo; MPC e LSTM apoiam redução do tempo total com receita aproximadamente neutra.
- **Resultados:** experimentos em rede multirregional mostram cumprimento conjunto desses objetivos frente a ausência de tarifa e controles reativos.
- **Diferença:** compensação aos motoristas por evitar áreas, por meio de preços/subsídios; não saldo de favores entre regiões. Mostra que “dar crédito por desviar” também possui antecedentes regionais.

### R21 — Elokda, Bolognani, Dörfler e Nax (2024–2026), preprint

**Dynamic Resource Allocation with Karma: An Experimental Study.** arXiv:2404.02687, **v4 de 16/06/2026**. **Acesso: R; publicação revisada por pares não confirmada.** [Versão consultada](https://arxiv.org/abs/2404.02687v4).

- **Abordagem:** experimento comportamental online com pessoas disputando repetidamente um recurso, com urgências variáveis e créditos não negociáveis.
- **Resultados:** melhora quase de Pareto sobre alocação aleatória mesmo com desvios das estratégias teóricas. A versão atual descreve diferenças entre tratamentos como majoritariamente não significativas; não superestimar superioridade de lances binários com base em versões antigas.
- **Limite:** não é experimento de trânsito urbano nem implantação edge. Ajuda a separar evidência comportamental de resultados obtidos com agentes programados para obedecer.

## 7. Adesão e dois antecedentes complementares

### R22 — Jiang, Tran e Keyvan-Ekbatani (2024)

**Regional route guidance with realistic compliance patterns: Application of deep reinforcement learning and MPC.** *Transportation Research Part C*, 158, 104440. **Acesso: R/P.** [Artigo](https://doi.org/10.1016/j.trc.2023.104440).

- **Abordagem:** orientação regional individualizada para veículos que aceitam recomendações, usando MPC e aprendizado por reforço.
- **Resultados:** estratégias multiagentes superam as de agente único nos testes; analisa compromisso entre tempo total e comprimento das viagens.
- **Relação:** a adesão integral escolhida para o projeto é uma hipótese simplificadora aceitável, mas já há métodos que tratam adesão heterogênea. Ela não deve ser apresentada como representação realista dos motoristas de Campinas.

### R23 — Reciprocidade indireta em mudança de faixa (2024)

**A digital decision approach for indirect-reciprocity based cooperative lane-changing.** *Physica A*, 633, 129365. **Acesso: P.** [Artigo](https://doi.org/10.1016/j.physa.2023.129365).

- **Abordagem:** quem cede passagem ganha uma pontuação de reputação e aumenta a chance de receber ajuda futura; combina jogos repetidos e Q-learning.
- **Resultados:** a simulação relata aumento de cooperação e redução de tempo de mudança de faixa nas condições estudadas.
- **Diferença:** interação veicular em entrada de interseção simplificada, não roteamento regional. É relacionado ao interesse original em CAV e mostra que memória de cooperação não precisa assumir a forma de moeda transferível.

### R24 — Shirado, Kasahara e Christakis (2023)

**Emergence and collapse of reciprocity in semiautomatic driving coordination experiments with humans.** *PNAS*, 120(51), e2307804120. **Acesso: resumo e trechos do estudo.** [DOI](https://doi.org/10.1073/pnas.2307804120), [Repositório do artigo](https://pmc.ncbi.nlm.nih.gov/articles/PMC10743379/).

- **Abordagem:** 300 participantes, em 150 duplas, controlam veículos robóticos em um jogo de coordenação.
- **Resultado:** a assistência automática pode alterar e suprimir reciprocidade que emerge entre participantes.
- **Relação:** evidencia que automatizar decisões não garante cooperação humana. O estudo do projeto, com bordas programadas e veículos obedientes, deve ser descrito como avaliação de política de coordenação, sem inferir aceitação social.

## 8. Mapa de proximidade com a proposta

As células resumem o mecanismo descrito, não uma auditoria de ausência de funcionalidades. “Não identificado” significa apenas que não apareceu no material consultado.

| Linha | Trabalhos | Proximidade | Diferença principal |
|---|---|---|---|
| Rotas apoiadas em edge/fog | R01–R04 | Muito alta na arquitetura e aplicação | Reciprocidade regional não identificada; alguns mantêm nuvem/hierarquia |
| Negociação distribuída de caminhos | R05–R06 | Alta no problema de evitar concentração de desvios | Agentes são veículos; há agregação/visão global em partes da arquitetura |
| Decisão por regiões | R07–R12 | Alta na distribuição e conflito local/coletivo | Vários controlam semáforos; coordenação/treinamento podem ser globais |
| Justiça regional e orientação de rotas | R13–R16 | Muito alta no objetivo científico | Justiça explícita sem o saldo de favores proposto |
| Créditos por sacrifício presente | R17–R21 | Muito alta no mecanismo temporal | Créditos pertencem principalmente a usuários; modelos e hipóteses distintos |
| Adesão às recomendações | R22 | Alta na modelagem comportamental | Vai além da adesão integral do projeto |
| Reciprocidade veicular/humana | R23–R24 | Complementar | Manobras e pessoas, não bordas territoriais |

### O que já foi abordado

- **Edge/fog para orientação cooperativa de rotas:** sim, diretamente.
- **Evitar que o desvio gere novo congestionamento:** sim, diretamente.
- **Dividir a rede em regiões com controladores próprios:** sim.
- **Combinar eficiência e justiça entre regiões:** sim; inclusive em orientação de rotas.
- **Ajudar agora e obter preferência depois:** sim; em karma e reputação veicular.
- **A combinação exata de saldos regionais, vizinhança informacional e tolerância de custo:** não localizada nesta revisão; requer confirmação aprofundada dos trabalhos mais próximos.

## 9. Lacunas candidatas e perguntas que o projeto pode responder

As propostas desta seção são **inferências a partir da comparação**, não alegações dos artigos de que o campo inteiro deixou esses problemas em aberto.

### 9.1. Qual é o valor adicional da memória de cooperação?

O contraponto decisivo não é apenas “comunicar versus não comunicar”. Há métodos de justiça regional sem histórico de favores, como [R13](https://doi.org/10.1016/j.trc.2022.103961) e [R14](https://doi.org/10.1016/j.trc.2023.104359).

**Pergunta:** mantendo informação, demanda e ações iguais, usar o saldo melhora o equilíbrio de custos em relação a uma política justa baseada apenas no estado atual?

**Teste proposto:** acrescentar uma regra sem memória que distribui os desvios considerando atraso/capacidade normalizados. Não precisa reproduzir integralmente MPC ou aprendizado profundo; deve ser apresentada como baseline simples inspirado nessa preocupação, não como reprodução dos artigos.

### 9.2. Reciprocidade funciona com parceiros fixos e capacidades desiguais?

A comparação com [R18](https://doi.org/10.1007/s13235-023-00503-0) evidencia a diferença entre uma grande população com encontros repetidos e poucos vizinhos fixos.

**Pergunta:** uma região estruturalmente congestionada consegue obter ajuda mesmo quando tem poucas oportunidades de retribuir? Uma região de alta capacidade acumula saldo que nunca consegue usar?

**Teste proposto:** contrastar picos alternados com desequilíbrio persistente e diferenças de capacidade. Registrar ajuda negada por incapacidade física separadamente de ajuda negada por prioridade/saldo.

### 9.3. O mecanismo depende de informação que a borda não tem?

Uma política pode parecer local enquanto consulta uma matriz global de tempos ou usa o simulador para escolher a melhor rota da cidade. [R06](https://doi.org/10.1109/TMC.2016.2538226) e [R10](https://doi.org/10.1016/j.trc.2023.104033) mostram arquiteturas distintas quanto à disponibilidade de conhecimento global.

**Pergunta:** quais resumos são suficientes para negociar desvios sem consulta a estado dinâmico global?

**Teste proposto:** definir uma interface explícita de observação. A topologia estática pode ser conhecida por todos; velocidades, ocupações e filas atualizadas devem respeitar as fronteiras informacionais escolhidas. Separar os dados do avaliador dos dados fornecidos aos controladores.

### 9.4. Tolerância estimada controla o custo efetivo?

Uma decisão admissível no instante da negociação pode ficar ruim quando várias regiões negociam ao mesmo tempo.

**Pergunta:** qual a diferença entre o custo previsto e o observado, e quantas vezes o resultado ultrapassa a tolerância pretendida?

**Teste proposto:** registrar ambas as medidas, impedir duplo comprometimento da mesma capacidade e limitar rerroteamentos sucessivos. A tolerância local não deve ser anunciada como garantia do custo global.

### 9.5. Que justiça está sendo medida?

[R15](https://doi.org/10.1007/s10458-023-09616-7) trabalha com usuários comparáveis por origem/destino; isso difere de igualar atrasos de territórios de tamanhos distintos.

**Pergunta:** o equilíbrio regional melhora porque os custos foram distribuídos ou porque todos pioraram?

**Teste proposto:** apresentar simultaneamente eficiência absoluta, pior custo regional, distribuição normalizada e viagens não concluídas. Não usar igualdade dos saldos como prova de justiça. Não aplicar diretamente índices que exigem valores não negativos a custos incrementais com sinais mistos.

## 10. Pontos do mecanismo que precisam ser fechados

### Créditos, reputação ou dívida bilateral?

Há três conceitos diferentes:

1. **Moeda de reciprocidade:** ganha-se e gasta-se saldo; regras definem quem paga, quem recebe e conservação/redistribuição.
2. **Reputação:** ajudar eleva uma pontuação usada na prioridade, sem transferência ou gasto necessariamente.
3. **Dívida bilateral:** a região A registra uma obrigação em relação à B; o saldo tem significado por par.

O plano atual ainda permite mais de uma interpretação. Para sustentar o vínculo com karma, é preciso explicitar ganho **e uso** dos créditos. Caso contrário, é melhor chamar o mecanismo de prioridade baseada em histórico de cooperação. Essa distinção decorre da comparação entre [R18](https://doi.org/10.1007/s13235-023-00503-0) e [R23](https://doi.org/10.1016/j.physa.2023.129365).

**Problema de inicialização:** se todos começam em zero, não podem ficar negativos e precisam pagar para receber ajuda, ninguém consegue iniciar. Será necessário permitir ajuda inicial sem saldo, dívida controlada ou uma dotação inicial. Isso é uma decisão de desenho ainda pendente, não uma falha inevitável da proposta.

### “Incentivo” ou política imposta?

Se todos os veículos obedecem e todas as bordas executam o algoritmo, o experimento avalia uma **política de alocação/coordenação com memória**. Ele não demonstra que agentes estratégicos escolheriam cooperar, nem equilíbrio de Nash ou resistência a manipulação. As provas de [R19](https://doi.org/10.1287/trsc.2023.0323) dependem de um modelo de decisão que o projeto não terá automaticamente.

Manter a hipótese atual é compatível com o prazo; basta formular a contribuição com precisão.

### Por que uma borda protege “sua” região?

Definir a utilidade local: atraso em todos os trechos da região, atraso de viagens originadas nela ou custo de seus residentes são objetivos diferentes. Para a primeira versão, atraso nos trechos locais é mensurável, mas pode induzir expulsão de tráfego. Avaliar o resultado global é necessário para identificar essa externalidade.

## 11. Ajustes recomendados ao plano experimental

### Pergunta reformulada

> Em uma rede urbana particionada, com informação dinâmica restrita à vizinhança, qual é o efeito de um histórico de ajuda entre nós de borda sobre a distribuição temporal dos custos de rerroteamento, em comparação com cooperação sem memória, sob uma tolerância explícita de custo?

### Quatro políticas principais

| Política | Função na comparação |
|---|---|
| L — Local | Referência sem negociação regional |
| C — Cooperativa imediata | Isolar o benefício de compartilhar informação e coordenar |
| F — Cooperativa justa sem memória | Verificar se justiça simples já explica os ganhos |
| R — Cooperativa com reciprocidade | Medir o valor adicional do histórico/saldo |

As duas comparações centrais são C versus L e R versus F. C versus R continua útil, mas sozinha não isola a contribuição da memória frente a outros critérios distributivos.

### Cenários e variações prioritários

1. Demanda moderada, para detectar intervenção desnecessária.
2. Picos alternados, favoráveis a oportunidades de retribuição.
3. Sobrecarga persistente em uma região, com capacidades assimétricas.
4. Poucos valores de tolerância de custo, calibrados em execuções distintas das finais.

Como ablação opcional, zerar o histórico a cada decisão ou embaralhar os saldos, mantendo a mesma regra de escolha. Isso ajuda a identificar se o conteúdo do histórico importa.

### Métricas mínimas

- Tempo total/médio e percentil alto de viagem; viagens concluídas e pendentes.
- Atraso regional absoluto e normalizado, incluindo o pior resultado regional.
- Ajuda concedida, recusada e efetivamente utilizada; distribuição dos custos ao longo do tempo.
- Custo estimado versus observado e frequência de violações da tolerância.
- Mensagens e duração das decisões como diagnóstico leve da implementação, sem transformar rede/latência em uma segunda pesquisa principal.

Usar as mesmas sementes e demandas entre políticas, repetições independentes e intervalos de incerteza. Conservar os resultados brutos. Ganhos percentuais publicados em outros mapas não são metas nem previsões para Campinas.

### Papel da borda e viabilidade

A escolha informacional do projeto permanece central: cada serviço possui dados locais e recebe resumos vizinhos. Serviços separados permitem demonstrar essa arquitetura, mas execução na mesma máquina não comprova vantagens de latência de uma implantação física.

SUMO com Python/TraCI é um candidato sustentado por implementações anteriores, como [R05](https://doi.org/10.1007/s40747-022-00833-3). A escolha definitiva exige um piloto. O mapa de Campinas agrega contexto ao estudo; usar uma cidade diferente não constitui, isoladamente, novidade científica.

## 12. Ordem de leitura sugerida

| Prioridade | Trabalho | Pergunta que ajuda a resolver |
|---|---|---|
| 1 | R01 — Cross-domain cooperative route planning | Quanto da arquitetura edge e do problema de desvios já está coberto? |
| 2 | R14 — An MFD approach… fairness | O que já existe de justiça na orientação regional de rotas? |
| 3 | R17 — Urgency-aware optimal routing | Como o sacrifício presente vira vantagem futura em rotas? |
| 4 | R02 — FOXS | Como implementar conhecimento local e recomendações na borda? |
| 5 | R18 — Self-contained karma economy | Quais regras dão significado aos créditos? |
| 6 | R08 — Distributed model predictive approach | Como controladores locais alternam interesses próprios e cooperação? |
| 7 | R16 — Queue balancing (preprint) | Qual baseline justo simples pode desafiar a reciprocidade? |
| 8 | R05 — ACO com negociação | Como avaliar coordenação em mapa real e quais lacunas de comunicação ficam? |

Para R01, R08 e R14, priorizar obtenção/leitura integral antes de afirmar que a combinação proposta é original. R11 e R12 ajudam a atualizar o posicionamento quanto à descentralização; R19 e R22 aprofundam mecanismos e comportamento.

## 13. Formulação segura para a proposta da disciplina

> Este estudo avalia uma política distribuída de coordenação de rotas urbanas em que nós de borda representam regiões e mantêm um histórico de ajuda na recepção de tráfego desviado. A investigação compara decisões locais, cooperação imediata, cooperação justa sem memória e cooperação com reciprocidade, sob restrições de informação e tolerância de custo. O objetivo é identificar em quais condições a memória de cooperação melhora a distribuição dos custos e quais perdas de eficiência ou limitações surgem em redes assimétricas.

Essa formulação não depende de prometer um algoritmo inédito ou um resultado positivo. A proposta permanece interessante e compatível com uma contribuição experimental de disciplina, desde que os antecedentes sejam reconhecidos e a comparação seja rigorosa.
