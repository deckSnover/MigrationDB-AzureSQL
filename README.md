# MigrationDB-AzureSQL

Para documentar seu projeto de migração de um banco de dados SQL Server para Azure SQL Database e postar no GitHub, você pode criar uma estrutura organizada com arquivos README e scripts necessários. Aqui está um exemplo de como você pode estruturar seu repositório e documentar o processo:

### Estrutura do Repositório

```
migração-sql-server-para-azure-sql-db/
├── README.md
├── scripts/
│   ├── backup.sql
│   ├── migration.ps1
├── img/
│   ├── step1.png
│   ├── step2.png
│   ├── ...
└── docs/
    ├── avaliação.md
    ├── preparação.md
    ├── migração.md
    ├── pós-migração.md
```

### Conteúdo dos Arquivos

#### 1. README.md

```markdown
# Migração de Banco de Dados SQL Server para Azure SQL Database

## Descrição
Este projeto documenta a migração de um sistema legado baseado em SQL Server para a plataforma de nuvem Azure SQL Database, visando escalabilidade e redução de custos operacionais.

## Tecnologias Utilizadas
- SQL Server
- Azure SQL Database
- Azure Database Migration Service (DMS)
- Data Migration Assistant (DMA)

## Habilidades Adquiridas
- Migração de banco de dados
- Administração em nuvem
- Otimização de performance

## Estrutura do Repositório
- `scripts/`: Contém scripts SQL e PowerShell utilizados no processo de migração.
- `img/`: Imagens e capturas de tela do processo.
- `docs/`: Documentação detalhada de cada etapa do processo.

## Como Utilizar
Siga a documentação detalhada nas pastas `docs/` para reproduzir o processo de migração.

## Etapas da Migração
1. [Avaliação e Planejamento](docs/avaliação.md)
2. [Preparação do Ambiente](docs/preparação.md)
3. [Configuração do Azure SQL Database](docs/configuração.md)
4. [Migração dos Dados](docs/migração.md)
5. [Pós-Migração](docs/pós-migração.md)

```

#### 2. scripts/backup.sql

```sql
-- Script para realizar backup do banco de dados SQL Server
BACKUP DATABASE [SeuBancoDeDados]
TO DISK = N'C:\backups\SeuBancoDeDados.bak'
WITH NOFORMAT, NOINIT,
NAME = N'SeuBancoDeDados-Full Database Backup',
SKIP, NOREWIND, NOUNLOAD, STATS = 10;
GO
```

#### 3. scripts/migration.ps1

```powershell
# Script PowerShell para configurar e iniciar a migração utilizando o Azure Database Migration Service (DMS)

# Parâmetros
$sourceSqlConnectionString = "Server=seu_servidor_sql_server;Database=SeuBancoDeDados;User Id=seu_usuario;Password=sua_senha;"
$targetSqlConnectionString = "Server=seu_servidor_azure_sql.database.windows.net;Database=SeuBancoDeDados;User Id=seu_usuario;Password=sua_senha;"

# Instalar módulo do Azure
Install-Module -Name Az -AllowClobber -Force

# Login no Azure
Connect-AzAccount

# Criar serviço de migração
New-AzDmsService -ResourceGroupName "seu_grupo_de_recursos" -ServiceName "seu_servico_de_migracao" -Location "East US" -Sku "Basic_1vCore"

# Configurar projeto de migração
New-AzDmsProject -ResourceGroupName "seu_grupo_de_recursos" -ServiceName "seu_servico_de_migracao" -ProjectName "seu_projeto_de_migracao" -SourcePlatform "SQL" -TargetPlatform "AzureDb"

# Iniciar migração
Start-AzDmsMigration -ResourceGroupName "seu_grupo_de_recursos" -ServiceName "seu_servico_de_migracao" -ProjectName "seu_projeto_de_migracao" -SourceSqlConnectionString $sourceSqlConnectionString -TargetSqlConnectionString $targetSqlConnectionString -DatabaseName "SeuBancoDeDados"
```

#### 4. docs/avaliação.md

```markdown
# Avaliação e Planejamento

## Ferramenta: Data Migration Assistant (DMA)

### Passos:
1. **Instalação do DMA**: Baixe e instale o [Data Migration Assistant](https://aka.ms/dma).
2. **Criação de Projeto de Avaliação**:
   - Abra o DMA.
   - Clique em "New" para criar um novo projeto.
   - Selecione "Assessment" como tipo de projeto.
   - Conecte-se ao seu servidor SQL Server.
   - Selecione os bancos de dados a serem avaliados.
   - Execute a avaliação para identificar possíveis problemas de compatibilidade.
3. **Correção de Incompatibilidades**:
   - Revise o relatório gerado pelo DMA.
   - Corrija quaisquer problemas de compatibilidade encontrados.

### Capturas de Tela:
![DMA Assessment](../img/step1.png)
```

#### 5. docs/preparação.md

```markdown
# Preparação do Ambiente

## Backup do Banco de Dados

### Passos:
1. **Realize um Backup Completo**:
   - Execute o script `backup.sql` localizado na pasta `scripts/` para fazer um backup completo do banco de dados SQL Server.

### Script:
```sql
-- Script para realizar backup do banco de dados SQL Server
BACKUP DATABASE [SeuBancoDeDados]
TO DISK = N'C:\backups\SeuBancoDeDados.bak'
WITH NOFORMAT, NOINIT,
NAME = N'SeuBancoDeDados-Full Database Backup',
SKIP, NOREWIND, NOUNLOAD, STATS = 10;
GO
```

### Capturas de Tela:
![Backup](../img/step2.png)
```

#### 6. docs/configuração.md

```markdown
# Configuração do Azure SQL Database

## Criação do Banco de Dados no Azure

### Passos:
1. **Criar uma Nova Instância do Azure SQL Database**:
   - No Azure Portal, navegue até o serviço "Azure SQL".
   - Clique em "Criar".
   - Preencha as informações necessárias, como nome do banco de dados, servidor, etc.
   - Selecione o nível de desempenho adequado.
2. **Configuração do Azure Database Migration Service (DMS)**:
   - No Azure Portal, configure o Azure Database Migration Service.
   - Navegue até "Azure Database Migration Services".
   - Clique em "Criar".
   - Preencha as informações e crie o serviço.

### Capturas de Tela:
![Create Azure SQL Database](../img/step3.png)
```

#### 7. docs/migração.md

```markdown
# Migração dos Dados

## Utilizando o Azure Database Migration Service (DMS)

### Passos:
1. **Configurar o Projeto de Migração**:
   - No DMS, crie um novo projeto de migração.
   - Selecione "Online data migration" ou "Offline data migration".
   - Conecte-se ao servidor SQL Server de origem.
   - Conecte-se ao Azure SQL Database de destino.
   - Selecione os bancos de dados a serem migrados.
2. **Iniciar a Migração**:
   - Execute o script `migration.ps1` localizado na pasta `scripts/` para iniciar a migração.

### Script:
```powershell
# Script PowerShell para configurar e iniciar a migração utilizando o Azure Database Migration Service (DMS)

# Parâmetros
$sourceSqlConnectionString = "Server=seu_servidor_sql_server;Database=SeuBancoDeDados;User Id=seu_usuario;Password=sua_senha;"
$targetSqlConnectionString = "Server=seu_servidor_azure_sql.database.windows.net;Database=SeuBancoDeDados;User Id=seu_usuario;Password=sua_senha;"

# Instalar módulo do Azure
Install-Module -Name Az -AllowClobber -Force

# Login no Azure
Connect-AzAccount

# Criar serviço de migração
New-AzDmsService -ResourceGroupName "seu_grupo_de_recursos" -ServiceName "seu_servico_de_migracao" -Location "East US" -Sku "Basic_1vCore"

# Configurar projeto de migração
New-AzDmsProject -ResourceGroupName "seu_grupo_de_recursos" -ServiceName "seu_servico_de_migracao" -ProjectName "seu_projeto_de_migracao" -SourcePlatform "SQL" -TargetPlatform "AzureDb"

# Iniciar migração
Start-AzDmsMigration -ResourceGroupName "seu_grupo_de_recursos" -ServiceName "seu_servico_de_migracao" -ProjectName "seu_projeto_de_migracao" -SourceSqlConnectionString $sourceSqlConnectionString -TargetSqlConnectionString $targetSqlConnectionString -DatabaseName "SeuBancoDeDados"
```

### Capturas de Tela:
![DMS Migration](../img/step4.png)
```

#### 8. docs/pós-migração.md

```
