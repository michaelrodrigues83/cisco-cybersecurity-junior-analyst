# 📑 Relatório de Inteligência de Ameaças: Análise Prática de Incidente de Phishing

Este relatório técnico documenta a análise forense e a auditoria regulatória de uma **tentativa real de ataque cibernético** recebida em meu ecossistema pessoal. O objetivo deste documento é estritamente **acadêmico, informativo e laboratorial**, demonstrando a aplicação prática dos conceitos de segurança e privacidade na triagem de ameaças.

**Analista responsável:** Michael Hernandes Rodrigues  
**Classificação do Incidente:** Engenharia Social / Phishing Scape (Bypass de Filtros)  
**Vetor de Ataque:** E-mail Malicioso (Inbound Phishing)  

---

## 🔍 1.0 Evidências Coletadas e Sintomas de Alerta (Red Flags)

A triagem inicial do e-mail simulando a empresa de tecnologia *Capgemini* revelou múltiplos indicadores de comprometimento (IoCs) visuais e lógicos:

1. **Uso de Imagem Oculta para Bypass:** O conteúdo do golpe não foi enviado em formato de texto digitado, mas sim **mascarado dentro de um elemento de imagem embutido** no corpo do e-mail. Esta técnica visa burlar filtros heurísticos de gateways de e-mail (SEG), que possuem maior dificuldade em inspecionar strings dentro de camadas de arquivos visuais.
2. **Inconsistência de Escopo e Urgência:** O assunto do e-mail indica um processo corporativo de boas-vindas (*"Welcome to Capgemini!"*), porém o corpo da mensagem induz o usuário a um gatilho financeiro fraudulento (*"1.3470 BTC BINANCE MINING"*), quebrando o princípio básico de coerência de contexto.
3. **Hiperlinks Desalinhados:** A URL explícita no texto aponta para um domínio de hospedagem de blogs gratuito (`mataroa.blog`) completamente alheio à infraestrutura de servidores da Capgemini ou da corretora Binance.

---

## 🛠️ 2.0 Diagnóstico de Engenharia Lógica (Análise Técnica)

A investigação do artefato malicioso seguiu os rigorosos pilares de triagem estabelecidos pelas formações da **Cisco Networking Academy** e do **Google Cybersecurity Certificate**:

* **Verificação em Reputadores de URL (Checker):** O link fraudulento contido na imagem foi isolado e submetido a motores de análise de reputação e ameaças (como o *VirusTotal* e *URLVoid*). O diagnóstico apontou o domínio como **Malicioso/Phishing**, associado a campanhas ativas de roubo de credenciais (*credential stuffing*) e fraudes financeiras com criptoativos.
* **Avaliação de Cabeçalhos (Headers):** A análise do endereço IP do servidor de origem indicou falhas crassificadas de autenticação de e-mail. Embora o remetente visual exibisse o nome da empresa afetada, as assinaturas **SPF (Sender Policy Framework)** e **DKIM (DomainKeys Identified Mail)** falharam, confirmando uma tática de *Email Spoofing* (falsificação de identidade de remetente).

---

## 🧠 3.0 Correlação com GRC, ISO 27001 e LGPD

Sob a ótica de Governança, Riscos e Conformidade (GRC), o incidente foi mapeado com base nas normas internacionais e legislações vigentes:

### 🛡️ 3.1 Framework de Segurança (ISO/IEC 27001:2022)
* **Conscientização em Segurança da Informação (Controle A.6.3):** O incidente comprova empiricamente que o elo mais vulnerável da segurança são as pessoas. Programas de GRC devem manter treinamentos contínuos de conscientização contra engenharia social para mitigar riscos operacionais antes que o tráfego atinja a rede interna.
* **Segurança de Serviços de Rede (Controle A.8.20):** Demonstra a necessidade urgente de calibrar os filtros de SPAM e gateways de e-mail da organização para realizar inspeção profunda de imagens e bloquear e-mails cujas diretivas SPF/DKIM não correspondam ao proprietário legítimo do domínio.

### ⚖️ 3.2 Implicações na Proteção de Dados (LGPD)
* **Mitigação de Incidentes de Vazamento (Art. 46):** O objetivo primário deste tipo de Phishing é capturar credenciais corporativas. Se um colaborador insere suas senhas nesse tipo de link, o atacante obtém acesso legítimo à infraestrutura interna da empresa (como sistemas de prontuários, no caso do setor de saúde), resultando em uma quebra severa de **Confidencialidade** e gerando um incidente de segurança de larga escala sujeito a sanções administrativas da ANPD.

---

## 👨‍🏫 4.0 Visão Consultiva de GRC: Conscientização e Mitigação de Riscos de Impacto em Massa

Este cenário prático serve como o **modelo perfeito de estudo de caso para orientar e treinar equipes internas** em qualquer empresa onde eu venha a atuar, servindo como base pedagógica para campanhas de Security Awareness.

### 🛑 4.1 O Risco do Efeito Dominó e Contágio do Ecossistema
É um erro crasso de gerenciamento achar que um ataque de Phishing compromete apenas o computador do funcionário que clicou no link. A grande ameaça à governança reside no potencial de **Movimentação Lateral** do agente malicioso. 
* Uma vez que a credencial do colaborador é roubada por meio de engenharia social, o invasor passa a navegar de forma legítima pelos sistemas.
* O atacante pode injetar scripts maliciosos (como Ransomwares), infectando não apenas uma máquina, mas desencadeando um contágio em massa que pode paralisar todo o ecossistema tecnológico e operacional da companhia.

### 📐 4.2 A Criação de Zonas de Risco e Defesa em Profundidade
Para conter essa ameaça em massa, a governança de GRC propõe a estruturação de **Zonas de Risco** e controles severos na infraestrutura:
* **Conscientização Contínua:** Capacitar colaboradores para que saibam ler os sinais visuais de golpes, transformando as pessoas na primeira linha de defesa ativa (human firewall).
* **Segmentação de Redes Rigorosa (Controle A.8.22 da ISO 27001):** Criação de barreiras lógicas para garantir que, caso uma zona da rede seja comprometida (como o setor administrativo), o agente malicioso fique isolado e não consiga migrar lateralmente para áreas críticas, salvaguardando o core business da empresa (como bancos de dados de exames médicos).

---

## 🚀 5.0 Plano de Resposta e Contenção Aplicado

Visando a preservação da integridade do ambiente e mitigação do risco de execução de malwares:
1. **Contenção:** O e-mail foi isolado, mantendo a diretiva de **não execução** de nenhum link interno ou download de elementos gráficos.
2. **Erradicação:** O artefato foi devidamente reportado aos servidores de e-mail como tentativa de fraude tecnológica e eliminado permanentemente.
3. **Lição Aprendida:** A inteligência artificial e os filtros automáticos falham. A última linha de defesa contra um ataque de engenharia social é o **olhar treinado e a maturidade técnica do analista**.

---
📌 *Estudo de caso simulado com dados de vetor real para fins estritamente informativos e educacionais.*

[⬅️ Voltar para o Painel Cisco](./README.md)
