+++
date = '2026-04-23T12:30:54-03:00'
draft = true
title = 'Introdução ao Ansible'
+++
# Artigo - Introdução ao Ansible

Gerenciar configurações de servidores e serviços em TI pode ser bastante desafiador, principalmente em ambientes de missão critica e de grande escala. Processos manuais são lentos e sujeitos a erros. O Ansible automatiza operações de TI, simplificando tarefas repetitivas. Ele permite mudanças eficientes, padronizando servidores, minimizando falhas e economizando tempo.

## **Mas afinal, o que é o Ansible?**

O Ansible é uma ferramenta de automação open source adquirida pela RedHat em 2015, mas que manteve seu código aberto para toda a comunidade. Sua finalidade é automatizar o provisionamento, a gestão de configuração, a implantação de apps, a orquestração e outros processos. O legal do Ansible é sua simplicidade: não é necessário instalar agentes nos hosts que precisam ser gerenciados; ele trabalha de forma declarativa (utilizando Yaml). Basicamente, você define o estado que deseja e o Ansible faz as mudanças necessárias.

Utilizando uma abordagem “push” de automação, em que o control node envia as instruções diretamente para os managed nodes. Isso é feito via SSH (em sistemas Unix/Linux) ou via WinRM (em sistemas Windows). Segue etapas executadas:

**Conexão via SSH/WinRM:** O Ansible estabelece uma conexão com os managed nodes usando SSH.

**Execução das Tarefas:** O Ansible executa as tarefas diretamente no host gerenciado. Essas tarefas são baseadas nos módulos do Ansible, que são pequenos scripts que realizam uma ação específica, como instalar um pacote, modificar um arquivo ou reiniciar um serviço.

**Idempotência:** O Ansible garante que cada tarefa seja idempotente. Isso significa que uma tarefa será executada apenas se for necessária para atingir o estado desejado. Por exemplo, se um pacote já estiver instalado na versão correta, o Ansible não tentará reinstalá-lo.

**Relatório de Execução:** Após a execução das tarefas, o Ansible gera um relatório mostrando o que foi alterado, o que já estava conforme o esperado e se houve algum erro.

## **Como Funciona o Ansible?**

Seguindo uma abordagem simples para realizar tarefas de automação. Sua arquitetura é baseada em três componentes principais: **control node**, **managed nodes** e **playbooks**.

**Control Node:** Este é o ponto central a partir do qual o Ansible é executado. O control node executa os playbooks, estabelecendo conexões com os managed nodes via SSH. É aqui que você define o que será automatizado.

**Managed Nodes:** Esses são os hosts que o Ansible gerencia. Podem ser servidores físicos, máquinas virtuais, containers ou até mesmo dispositivos de rede. Os managed nodes não necessitam de um agente específico do Ansible, apenas de conectividade SSH.

**Playbooks:** Os playbooks são conjuntos de tarefas escritas em YAML que descrevem o que deve ser feito em cada managed node. Um playbook pode conter instruções detalhadas para instalação de pacotes, configuração de serviços, atualização de software, entre outras tarefas.

Demais recursos presentes e necessários para o funcionamento:

**Inventário**: É o arquivo onde você lista todos os hosts que o Ansible irá gerenciar, contém informações como endereços de IP, nome dos hosts e grupos. Um inventário pode ser estático (um simples arquivo de texto) ou dinâmico (gerado a partir de fontes como AWS ou Azure)

**Módulos:** São pequenos scritps executados pelos playbooks para realizar ações específicas, como modificar arquivos, reiniciar serviços, execução de comandos, instalar pacotes ou interagir com APIs.

**APIs**: As APIs (Application Programming Interfaces) permitem interagir e automatizar de forma programática. Elas são ferramentas úteis para integrar o Ansible em fluxos de trabalho, sistemas de automação ou em qualquer ambiente que precise de interações automáticas com o Ansible.

O **CMDB (Configuration Management Database)** no Ansible é um repositório usado para armazenar dados de configuração e inventário sobre os managed nodes. Ele pode ser usado como uma fonte centralizada de dados para automação, permitindo que o Ansible recupere informações sobre hosts, aplicações e serviços, como variáveis, estados e configurações específicas.

**No Ansible**, o CMDB pode ser implementado de várias formas:

- **Dynamic Inventory**: Integração com ferramentas como AWS, Azure ou Kubernetes para obter dados em tempo real.
- **Arquivos YAML ou JSON**: Um CMDB simples pode ser mantido em arquivos que detalham configurações específicas dos hosts.
- **Integração com ferramentas externas**: Ferramentas como ServiceNow ou Puppet podem atuar como CMDB para fornecer dados ao Ansible.

**Variáveis:** Permitem personalizar as execuções, passando parâmetros específicos para diferentes máquinas ou ambientes

![ansible-engine](/images/ansible-engine.png)

### **Estrutura de um Playbook**

Abaixo, um exemplo simples de um playbook em YAML para instalar o Python em um servidor Linux:

```yaml
---
- name: Instalacao Python
  hosts: prod
  become: yes
  tasks:
    - name: Certifique-se de que o Python esteja instalado
      apt:
        name: python3
        state: present

```

---

Neste exemplo:

- `hosts: prod`: O Ansible será executado nos hosts identificados como “prod”.
- `become: yes`: Garante que as tarefas sejam executadas com privilégios de superusuário (root)
- `tasks`: Lista de tarefas a serem executadas
- `apt`: Usa o módulo `apt` para garantir que o Python3 esteja instalado.

## **Conclusão**

O Ansible é uma ferramenta essencial para equipes de TI que precisam gerenciar grandes infraestruturas de forma eficiente e segura. Sua arquitetura sem agentes, simplicidade na criação de playbooks e suporte a uma vasta gama de módulos o tornam ideal para automação de tarefas complexas. Com o Ansible, as equipes podem focar mais na inovação e menos na gestão manual e repetitiva de sistemas.