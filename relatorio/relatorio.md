# Relatório Executivo de Auditoria: Telemetria e Privacidade em Smart TVs

## 1. Principais Padrões Observados

A análise cruzada das variáveis de sistema e comportamento do usuário revelou padrões operacionais consolidados no ecossistema das Smart TVs:

* **Consumo Enraizado:** A audiência é altamente concentrada, com mais de 60,6% das janelas de coleta dominadas por Filmes, Séries e Esportes. Esse engajamento prolongado facilita a atuação contínua da telemetria de reconhecimento automático de conteúdo (ACR).
* **Frequência do Hardware:** O microfone permaneceu ativo em 38,7% do tempo amostrado. Isso demonstra que os sensores de captação ambiental são rotineiramente acionados no uso cotidiano dos aparelhos.
* **Ineficácia Relativa do Modo de Privacidade:** A ativação do Modo de Privacidade na interface do sistema tem impacto nulo no fluxo de dados ordinário. A mediana de tráfego foi estatisticamente equivalente para o modo Ativado (22,54 KB) e Desativado (24,52 KB).
* **Dinâmica Publicitária:** Há um alto volume de inserções, mas a resposta é escassa. O funil de CTR global estacionou em 14,12%, confirmando que exibições passivas raramente se convertem em interações ativas.

## 2. Resultados Estatísticos que Chamaram Atenção

Os cálculos das medidas de dispersão e tendência central evidenciaram anomalias estruturais nos dados capturados:

* **Coeficiente de Variação (CV) Extremo no Tráfego:** A variável `trafego_saida_kb` apresentou um CV de impressionantes **750,73%**. Com uma mediana baixa (~23,5 KB) e picos isolados que ultrapassam 9.200 KB, o comportamento de transmissão das TVs é matematicamente errático e sujeito a explosões de dados repentinas não explicadas pelo uso normal.
* **Interações como *Outliers* Matemáticos:** Na variável `interacoes_anuncios`, tanto a mediana quanto o 3º quartil (Q3) cravam em **0,00**. Isso significa que a ausência de clique é a regra absoluta do sistema, a ponto de qualquer interação real com um anúncio ser classificada algoritmicamente como um evento atípico (187 *outliers* flagrados).
* **Estabilidade da Confiança de Classificação:** Em oposição ao tráfego errático, a inteligência artificial de reconhecimento de som mostrou constância impecável. Com um desvio padrão de apenas 0,13 e um CV de 16,5%, o algoritmo mantém uma confiança média travada em **78%** sempre que há som válido, atestando forte estabilidade no *firmware*.

## 3. Três Principais Achados

A investigação aprofundada das inconsistências gerou três alertas centrais para a conformidade do produto:

1. **Falha Crítica no *Opt-out* (Vazamento de Privacidade):** Dos usuários que informaram explicitamente "Não" à coleta de dados, 42,8% continuaram transmitindo ativamente metadados classificados como "Publicidade" ou "ACR/conteúdo". A recusa de interface não está desarmando o gatilho técnico da telemetria de marketing.
2. **Efeito "Placebo" da Chave de Privacidade:** Habilitar a configuração "Modo de Privacidade" não impôs restrições arquiteturais ao tráfego de telemetria mediano. O aparelho continua operando o envio de pacotes sob a mesma intensidade de um aparelho desprotegido.
3. **Alto Risco de Captação Passiva:** O acionamento do microfone em quase 4 em cada 10 janelas, somado aos picos atípicos de tráfego, levanta o alerta sobre escuta passiva e a potencial transmissão desses fragmentos para servidores externos sem conhecimento do usuário.

## 4. Decisões e Ações Recomendadas

Para mitigar os riscos técnicos e jurídicos evidenciados pelos achados, recomendam-se as seguintes frentes de atuação corretiva:

* **Intervenção Técnica no *Opt-out*:** Implementar um bloqueio arquitetural (*hardcode*) no nível de rede do sistema operacional. Se a flag de consentimento for nula ou falsa, o sistema deve impedir fisicamente qualquer requisição (POST) direcionada a domínios de publicidade ou de ACR, independentemente do serviço rodando em segundo plano.
* **Revisão da Interface e Documentação Legal:** Realinhar o que a chave "Modo de Privacidade" comunica ao usuário versus o que ela corta no *backend*. Caso ela impeça apenas logs do sistema, seu nome e seus Termos de Uso precisam ser alterados imediatamente para evitar passivos por propaganda enganosa ou infração à LGPD.
* **Auditoria de Gatilhos de *Firmware*:** Engajar a equipe de segurança cibernética para inspecionar os processos (da TV ou do *Soundbar*) que estão ativando o microfone. É imperativo descobrir se o sensor está sendo acordado por falha na identificação de *wake words* (falsos positivos) ou se há serviços clandestinos abrindo a porta de escuta do sistema de forma indiscriminada.

## 5. Limitações do Dataset

A validade e a inferência das conclusões deste relatório devem observar as premissas e limitações inerentes aos dados manipulados:

* **Simulação e Amostragem:** O dataset é constituído de dados simulados que espelham comportamentos esperados, limitados a um período temporal curto (01/09/2026 a 10/10/2026).
* **Recorte Temporal Capado:** As coletas são restritas a janelas fechadas de no máximo 10 minutos (`minutos_visualizados`). Isso oblitera a compreensão do comportamento sequencial e de longa duração das sessões do usuário.
* **Ambiguidade Semântica:** A flag `estado_microfone` = "Ativo" indica apenas que o *hardware* foi energizado ou acionado em algum momento da janela, não atestando que houve gravação contínua ou processamento do áudio durante os 10 minutos completos.
* **Opacidade de Conteúdo (Payload):** Um alto `trafego_saida_kb` sinaliza volume transferido, mas o dataset não especifica o *payload* (conteúdo dos pacotes). Um pico de 9 MB pode ser um vazamento grave de dados pessoais estruturados, mas também pode ser um *crash dump* inofensivo de vídeo ou download de *patches*, dificultando a prova definitiva sem a inspeção técnica de pacotes de rede.

A análise dos dados permitiu concluir que há falhas sistêmicas na arquitetura de privacidade do sistema avaliado, evidenciadas pela ineficácia prática do "Modo de Privacidade" em conter o volume de tráfego e pelo envio contínuo de telemetria publicitária mesmo após a recusa explícita de consentimento. Por outro lado, é imperativo ressaltar o que os dados não permitem afirmar: não há qualquer comprovação de que conversas estão sendo gravadas ou interceptadas, pois o status de microfone ativo não atesta gravação contínua e a volumetria de tráfego não revela o conteúdo (payload) dos pacotes enviados. Além disso, por estarmos lidando exclusivamente com um dataset simulado em recortes fechados de dez minutos, nenhuma dessas vulnerabilidades reflete ou pode ser atribuída a modelos, marcas ou aparelhos de Smart TVs reais operando no mercado.