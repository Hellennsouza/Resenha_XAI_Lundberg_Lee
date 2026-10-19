#Resenha Crítica: **A Unificação da XAI via Teoria dos Jogos Cooperativos**

Hellen Nunes dos Santos Souza  
17 de outubro de 2026, Sorocaba/SP

Resenha Crítica do artigo: *A Unified Approach to Interpreting Model Predictions*
Lundberg, Scott M.; Lee, Su-In. A Unified Approach to Interpreting Model Predictions. In: ADVANCES IN NEURAL INFORMATION PROCESSING SYSTEMS (NIPS 30), 2017, Long Beach. Proceedings... Long Beach: NIPS, 2017. p. 4765–4774.

Esta resenha tem como princípio analisar o artigo 'A Unified Approach to Interpreting Model Predictions', de autoria de Scott M. Lundberg e Su-In Lee (2017). Com o aumento do volume de dados,  Ludenberg e Lee  notaram a necessidade de estabelecer um framework, capaz de explicar as previsões de  forma simplificada. Assim, através de experimentos usando a Teoria dos Jogos Cooperativos, demonstram que os valores de SHAP são os únicos que seguem a lógica de pensamento humano, superando as limitações dos métodos de explicação até então existentes.

Os autores explicam os Métodos de Atribuição de Importância Aditiva informando que não dá para explicar um modelo complexo utilizando seu projeto original, mas que é necessário encontrar um modo de explicar de forma simplificada. Para isso, eles trazem métodos diferentes para serem comparados. O LIME, por exemplo, tenta simplificar o modelo original buscando minimizar a soma dos erros que não foram fiéis à “caixa-preta”. Porém, apesar do LIME ser utilizado, Lundberg e Lee (2017, p. 4) mostram que ele possui limitação:

                     “The LIME choices for these parameters are made heuristically; using these choices,       Equation 2 does not recover the Shapley values. One consequence is that local accuracy and/or consistency are violated, which in turn leads to unintuitive behavior in certain circumstances.” (LUNDBERG; LEE, 2017, p. 4)

Essa escolha heurística dos parâmetros no LIME permite que viole a propriedade da Consistência. Desse modo o peso de uma variável poderia ser manipulado para bem próprio ou de terceiros.

A grande inovação deste artigo é o método e  a aplicação do Framework SHAP (SHapley Additive exPlanations). Onde Ludenberg e Lee ligam a XAI (Inteligência Artificial Explicável) à Teoria dos Jogos Cooperativos , utilizando os Valores de Shapley para distribuir o peso de uma previsão entre as variáveis do modelo.  Como o próprio Shapley (1953, p. 1) explica em seu trabalho original:

                     “...at the foundation of the theory of games is the assumption that the players in a game can evaluate, in their utility scales, every 'prospect' that might arise as a result of a play...” (SHAPLEY, 1953, p. 1)

Trazendo isso para o aprendizado de máquina, cada variável de um modelo funciona como se fosse um “jogador” em uma equipe, e a previsão final é o resultado dessa cooperação, provando matematicamente que apenas essa abordagem na classe dos métodos aditivos satisfaz simultaneamente as 3 propriedades fundamentais (consistência, precisão local e ausência), garantindo explicações confiáveis e livres das contradições de heurísticas anteriores.

Os autores analisam também métodos como o DeepLIFT e o LRP. O DeepLIFT foi criado por Shrikumar, Greenside e Kundaje (2017, p. 1) para fazer a **“decomposing the output prediction of a neural network on a specific input by backpropagating the contributions of all neurons in the network to every feature of the input”**. Ele faz isso comparando a ativação de cada neurônio com uma entrada de referência neutra, calculando as contribuições de trás para frente. 

Porém, as regras originais do DeepLIFT para lidar com componentes não lineares também depende de escolhas heurísticas. Nesse sentido, Lundberg e Lee desenvolveram o Deep SHAP, que combina o DeepLIFT com os Valores de Shapley. Dessa forma, conseguiram manter a velocidade da retropropagação em redes profundas, mas com a garantia matemática do SHAP.

Já, nos modelos baseados em árvores de decisão e comitês (como XGBoost e Random Forests), o método heurístico de Saabas era muito usado para dar explicações locais. Só que, como demonstrado mais tarde por Lundberg et al. (2019, p. 4):

                     “The Saabas method has not been well studied, and we demonstrate here that it is strongly biased to alter the impact of features based on their distance from the root of a tree (...) This causes Saabas values to be inconsistent, which means we can modify a model to make a feature clearly more important, and yet the Saabas value attributed to that feature will decrease.” (LUNDBERG et al., 2019, p. 4)

Todavia, o método de Saabas dá um peso maior para variáveis que estão nas folhas da árvore e prejudica as variáveis que ficam perto da raiz. Pensando em uma solução para isso os autores criaram o algoritmo TreeSHAP (Lundberg et al., 2019), que consegue calcular os Valores de Shapley exatos em modelos de árvores de forma muito mais rápida. Ele reduz a complexidade de um cálculo exponencial para um cálculo polinomial, permitindo explicabilidade exata e sem variações para empresas que usam modelos de árvores.

Para tornar viável os cálculos dos subconjuntos computacionalmente, propõe-se o Kernel SHAP, uma abordagem agnóstica baseada em regressão linear ponderada pelo Kernel de Shapley que funciona para qualquer modelo. Os autores propõem que ao aproveitar a estrutura interna do modelo é possível criar determinados estimadores de forma mais agil. Dentre eles estão o Max SHAP, o Corollary 1 (Linear SHAP), e o O Low-Order SHAP que traz a comparação do shapley kernel, e dos métodos usando lime Kernel, provando que o método com SHAP retorna resultados diferentes dos métodos heurísticos. 

Entretanto, a principal limitação do SHAP é o seu alto custo computacional. Em bases de dados com muitas variáveis ou em sistemas que precisam responder em tempo real, calcular o SHAP exige bastante poder de processamento. Além disso, a suposição de independência das variáveis usadas em algumas aproximações pode acabar avaliando combinações de dados irreais, gerando um dilema entre a fidelidade matemática ao modelo e a realidade dos dados.

Destarte, o artigo “A Unified Approach to Interpreting Model Predictions” de Lundberg e Lee (2017) é um trabalho de grande valor para a Ciência de Dados e para a Inteligência Artificial Explicável. Ao unir diferentes métodos sob a ótica da Teoria dos Jogos e provar a unicidade dos Valores de Shapley, os autores conseguem resolver o grande dilema entre ter modelos precisos e ter modelos explicáveis.


**REFERÊNCIAS BIBLIOGRÁFICAS:**

Ludenberg, Scott M.; Lee, Su-In. A Unified Approach to Interpreting Model Predictions. In: ADVANCES IN NEURAL INFORMATION PROCESSING SYSTEMS (NIPS 30), 2017, Long Beach. Proceedings... Long Beach: NIPS, 2017. p. 4765–4774.

Ludenberg, Scott M. et al. Explainable AI for Trees: From Local Explanations to Global Understanding. arXiv preprint arXiv:1905.04610, 2019. p. 1–72.

Shapley, Lloyd S. A Value for n-Person Games. In: Kuhn, H. W.; Tucker, A. W. (Eds.). Contributions to the Theory of Games. Princeton: Princeton University Press, v. 2, 1953. p. 307–317.

Shrikumar, Avanti; Greenside, Peyton; Kundaje, Anshul. Learning Important Features Through Propagating Activation Differences. In: INTERNATIONAL CONFERENCE ON MACHINE LEARNING (ICML 34), 2017, Sydney. Proceedings... Sydney: PMLR, v. 70, 2017. p. 3145–3153.


