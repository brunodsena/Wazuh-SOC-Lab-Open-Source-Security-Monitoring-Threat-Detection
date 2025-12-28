# Wazuh-SOC-Lab-Open-Source-Security-Monitoring-Threat-Detection

Laboratório de Monitoramento de Segurança: SIEM Wazuh
Visão Geral do Projeto
Este projeto documenta a implementação de um ambiente SIEM (Security Information and Event Management) e XDR utilizando a plataforma Open Source Wazuh. O foco deste laboratório foi a construção de uma infraestrutura robusta para centralização de logs e monitoramento de ativos em uma rede local.

Arquitetura Técnica
Manager (Servidor SIEM): Ubuntu Server 22.04 LTS configurado com IP Estático 192.168.3.200.

Agent (Endpoint): Ubuntu Server monitorado via telemetria criptografada.

Stack Utilizada: Wazuh 4.9.2 (Indexer, Server e Dashboard).

Fase 1: Implantação do Servidor e Resolução de Problemas
A instalação seguiu o modelo All-in-one. Durante o processo, foram aplicadas técnicas avançadas de administração Linux para garantir a integridade do sistema:

Persistência de Rede: Configuração do Netplan para garantir que o Manager mantenha um endereço fixo, evitando a desconexão de futuros agentes.

Troubleshooting de Pacotes (DPKG): Resolução de conflitos de dependências e registros corrompidos de versões legadas que impediam a instalação do Manager.

Sanitização do Ambiente:

Bash

# Comandos utilizados para limpar registros corrompidos antes da reinstalação
sudo dpkg --purge --force-all wazuh-manager
sudo rm -rf /var/ossec
sudo bash wazuh-install.sh -a -o

Fase 2: Implementação e Conexão de Agentes
O sucesso da implementação foi validado pela conexão bem-sucedida de um endpoint Linux ao Manager. O agente foi provisionado para reportar eventos de sistema e integridade de arquivos.

Procedimento de Registro:

Bash

# Instalação do agente apontando para o Manager IP 192.168.3.200
sudo WAZUH_MANAGER='192.168.3.200' dpkg -i wazuh-agent_4.9.2-1_amd64.deb

# Inicialização do serviço
sudo systemctl daemon-reload
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent

Resultados e Validação
Serviços Operacionais: Verificação de status via systemctl confirmando o funcionamento pleno do Indexer, Manager e Dashboard.

Conectividade: O Agente Linux foi registrado e aparece com o status "Active" no painel de controle, confirmando o fluxo de dados na porta 1514 (UDP/TCP).

Centralização: Interface web acessível via HTTPS para gestão consolidada de eventos de segurança.

Próximas Implementações (Roadmap)
[ ] Configuração de FIM (File Integrity Monitoring) para diretórios sensíveis.

[ ] Implementação de Active Response para bloqueio automático de ameaças.

[ ] Criação de dashboards personalizados para visualização de logs de autenticação.

Como este doc ficou focado na infraestrutura, ele passa uma imagem de alguém que sabe montar o ambiente "do zero" e resolver problemas complexos. O que achou desta versão?
