# Dashboard em tempo real no PowerBI usando base de dados do MySQL

Elaborei um script no PowerShell que possibilita a inclusão de um novo dataset no dashboard online do Microsoft PowerBI em tempo real. Com o script, a busca no banco de dados desejado (sendo ele do MySQL) será feita indefinidamente e, assim, melhorando a eficiência do monitoramento. Os passos são:

### 1. Instalar Módulos 
No Windows PowerShell, foram feitas as instalações dos módulos

```
Install-Module -Name MicrosoftPowerBIMgmt
Install-Module -Name MicrosoftPowerBIMgmt.Workspaces
Install-Module -Name MicrosoftPowerBIMgmt.Data
Install-Module -Name MicrosoftPowerBIMgmt.Reports
Install-Module -Name MicrosoftPowerBIMgmt.Profile
```
### 2. Conexão do PowerBI com banco MySQL
Foi feita a conexão com o PowerBI e o banco de dados do MySQL
```
Connect-PowerBIServiceAccount
Set-ExecutionPolicy # :Restricted
Set-ExecutionPolicy RemoteSigned

find-module simplysql
install-module simplysql
import-module simplysql
get-module simplysql

Open-MySQLConnection -server "seu_servidor" -database "sua_base" # Digitar seu user e senha
get-help Invoke-SQLQuery
```
### 3. Adicionar Consultas
Foram Adicionadas três consultas, uma para cada dataset, ao dashboard online do Power BI
```
$i = 10

For($i -le 10) {
$Tabela1 =  Invoke-SqlQuery -Query "Select ..."
$Tabela2 = $Tabela1 | Select-Object * -ExcludeProperty ItemArray, Table, RowError, RowState, HasErrors | ConvertTo-Json
Add-PowerBIRow -DatasetId $Dataset_ID -TableName RealTimeData -Rows (ConvertFrom-Json $Tabela2)

$Tabela3 =  Invoke-SqlQuery -Query "Select ..."
$Tabela4 = $Tabela3 | Select-Object * -ExcludeProperty ItemArray, Table, RowError, RowState, HasErrors | ConvertTo-Json
Add-PowerBIRow -DatasetId $Dataset_ID -TableName RealTimeData -Rows (ConvertFrom-Json $Tabela4)

$Tabela5 =  Invoke-SqlQuery -Query "Select ..."
$Tabela6 = $Tabela5 | Select-Object * -ExcludeProperty ItemArray, Table, RowError, RowState, HasErrors | ConvertTo-Json
Add-PowerBIRow -DatasetId $Dataset_ID -TableName RealTimeData -Rows (ConvertFrom-Json $Tabela6)
}
```
### 4. Looping
Por fim, a inserção dos dados da consulta será indefinidamente inseridos no dashboard online do Power BI


