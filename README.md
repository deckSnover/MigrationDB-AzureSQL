# SQL Server para Azure SQL Database

## Visão Geral

Este documento descreve o processo detalhado de migração de um sistema legado baseado em SQL Server para a plataforma de nuvem Azure SQL Database. A migração visa alcançar maior escalabilidade e redução de custos operacionais.

## Etapas da Migração

### 1. Avaliação e Planejamento

#### Ferramenta Utilizada: Data Migration Assistant (DMA)

1. **Instalação do DMA**
   - Baixe e instale o [Data Migration Assistant](https://aka.ms/dma).

2. **Criação de Projeto de Avaliação**
   - Abra o DMA.
   - Clique em "New" para criar um novo projeto.
   - Selecione "Assessment" como tipo de projeto.
   - Conecte-se ao seu servidor SQL Server.
   - Selecione os bancos de dados a serem avaliados.
   - Execute a avaliação para identificar possíveis problemas de compatibilidade.

3. **Correção de Incompatibilidades**
   - Revise o relatório gerado pelo DMA.
   - Corrija quaisquer problemas de compatibilidade encontrados.

### 2. Preparação do Ambiente

#### Backup do Banco de Dados

1. **Realização de Backup Completo**
   - Execute o script `backup.sql` para fazer um backup completo do banco de dados SQL Server.

### 3. Configuração do Azure SQL Database

#### Criação do Banco de Dados no Azure

1. **Criação de Nova Instância do Azure SQL Database**
   - No Azure Portal, navegue até o serviço "Azure SQL".
   - Clique em "Criar".
   - Preencha as informações necessárias, como nome do banco de dados, servidor, etc.
   - Selecione o nível de desempenho adequado.

2. **Configuração do Azure Database Migration Service (DMS)**
   - No Azure Portal, configure o Azure Database Migration Service.
   - Navegue até "Azure Database Migration Services".
   - Clique em "Criar".
   - Preencha as informações e crie o serviço.

### 4. Migração dos Dados

#### Utilizando o Azure Database Migration Service (DMS)

1. **Configuração do Projeto de Migração**
   - No DMS, crie um novo projeto de migração.
   - Selecione "Online data migration" ou "Offline data migration".
   - Conecte-se ao servidor SQL Server de origem.
   - Conecte-se ao Azure SQL Database de destino.
   - Selecione os bancos de dados a serem migrados.

2. **Início da Migração**
   - Execute o script `migration.ps1` para iniciar a migração.

### 5. Pós-Migração

#### Validação e Otimização

1. **Validação de Dados**
   - Verifique se todos os dados foram migrados corretamente.

## Considerações Finais

Este documento fornece uma estrutura detalhada para a migração de um banco de dados SQL Server para Azure SQL Database, visando garantir uma transição suave e eficiente. É crucial seguir cada etapa cuidadosamente para minimizar interrupções e garantir a integridade dos dados durante todo o processo de migração.
