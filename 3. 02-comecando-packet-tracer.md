# 🌐 Curso 2: Começando com o Cisco Packet Tracer (Cisco Academy)

Este documento registra a conclusão oficial dos estudos práticos de fundamentos de redes e a aplicação da topologia de arquitetura de conectividade.

---

## 🛠️ Laboratório Prático: Engenharia de Redes e Conectividade Segura

**Analista responsável:** Michael Hernandes Rodrigues  
**Ambiente Utilizado:** Cisco Packet Tracer  
**Escopo do Projeto:** Simulação de Infraestrutura de Rede Corporativa Segura com Segmentação de Setores e Conectividade Sem Fio (Wireless)  

> 📌 **Contexto Acadêmico:** Este projeto prático foi desenvolvido no âmbito de simulação de laboratório para correlacionar conceitos de sub-redes, roteamento de gateways e segurança periférica à minha graduação em Segurança da Informação na **Faculdade de Tecnologia Prof. José Arana Varela (Araraquara)**.

---

## 🗺️ 1.0 Arquitetura da Topologia Física

A topologia simulada reproduz o cenário de uma organização dividida logicamente em dois setores de negócios principais, interconectados por um nó central de roteamento de borda:

* **Ativo de Borda / Roteamento:** 1 Roteador Cisco 2911 de três interfaces Gigabit, atuando como o núcleo de encaminhamento de pacotes entre os segmentos.
* **Ativos de Distribuição Camada 2:** 2 Switches Cisco Catalyst 2960 de 24 portas FastEthernet, responsáveis pelo gerenciamento local de enlace de dados em cada setor.
* **Pontos de Acesso Wireless:** 2 Access Points corporativos vinculados diretamente aos switches locais para expansão da cobertura de rede móvel.
* **Dispositivos Finais (Endpoints):** Estações de trabalho fixas cabeadas (PCs) e estações móveis híbridas (Laptops e Smartphones operando via Wi-Fi).

---

## ⚙️ 2.0 Detalhes do Endereçamento Lógico e Configuração

O Roteador Cisco 2911 foi configurado para atuar como o gateway padrão de ambos os domínios de colisão, dividindo o tráfego nas seguintes sub-redes:

### 💼 2.1 Setor A: Administration (Lado Esquerdo)
* **Escopo de Endereçamento:** `192.168.1.0/24` (Máscara: `255.255.255.0`)
* **Interface de Gateway (Roteador - GigabitEthernet 0/0):** `192.168.1.1`
* **Identificador de Rede Sem Fio (SSID):** `WIFI-ADMIN`
* **Inventário de Endpoints:** PC0 (`192.168.1.10`) e Laptop0 (`192.168.1.11`)

### 💰 2.2 Setor B: Financeiro (Lado Direito)
* **Escopo de Endereçamento:** `192.168.2.0/24` (Máscara: `255.255.255.0`)
* **Interface de Gateway (Roteador - GigabitEthernet 0/1):** `192.168.2.1`
* **Identificador de Rede Sem Fio (SSID):** `WIFI-FIN`
* **Inventário de Endpoints:** PC1 (`192.168.2.10`) e Laptop1 (`192.168.2.11`)

---

## 🚀 3.0 Validação de Conectividade e Métodos de Teste

Para validar a integridade lógica da tabela de roteamento e o correto funcionamento do encapsulamento de pacotes do laboratório:

1. Acesse o Prompt de Comando (CLI) de qualquer endpoint do Setor Administração (ex: **PC0**).
2. Execute o comando de teste de eco ICMP em direção ao IP de uma estação de trabalho do Setor Financeiro:
   ```bash
   ping 192.168.2.10
   ```
3. **Validação do SOC:** O sucesso no recebimento das respostas confirma a operação correta do protocolo ARP, a tradução de endereços nas interfaces do roteador e o perfeito funcionamento do Default Gateway.

---

## 🧠 4.0 Conexão com GRC e Segurança da Informação (ISO 27001)

Embora o cenário simule a conectividade básica de infraestrutura, sob a ótica de Governança, Riscos e Conformidade (GRC), os aprendizados aplicados são de natureza puramente defensiva:

* **Segmentação de Redes (ISO/IEC 27001:2022 - Controle A.8.22):** A divisão explícita em sub-redes distintas (`192.168.1.0/24` e `192.168.2.0/24`) isola os domínios de broadcast corporativos. Isso reduz drasticamente a superfície de ataque da organização, impedindo o farejamento de pacotes (*packet sniffing*) acidental e contendo a **Movimentação Lateral** de vetores maliciosos caso uma máquina periférica da Administração seja comprometida.
* **Segurança de Serviços de Rede (Controle A.8.20):** A centralização dos gateways no roteador de borda cria um ponto único de auditoria lógica, permitindo que futuras Listas de Controle de Acesso (ACLs) sejam implantadas na CLI para restringir de forma rigorosa quais ativos do setor administrativo podem estabelecer conexões com os servidores ou dados confidenciais do setor financeiro.
* **Gerenciamento de Redes Sem Fio:** A segregação de SSIDs (`WIFI-ADMIN` e `WIFI-FIN`) demonstra como a governança de ativos sem fio deve ser implementada para granularizar o controle de acessos com base na função (*Role-Based Access Control*).

---
[⬅️ Voltar para o Painel de Controle](./README.md)
