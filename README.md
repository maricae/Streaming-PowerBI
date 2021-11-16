# Dashboard em tempo real no PowerBI usando base de dados do MySQL

Elaborei um script no PowerShell que posibilita a inclusão de um novo dataset no dashboard online do Microsoft PowerBI em tempo real. Com o script, a busca no banco de dados desejado (sendo ele do MySQL) será feita indefinidamente e, assim, melhorando a eficiência do monitoramento. Os passos são:

1. No Windows PowerShell, foram feitas as instalações dos módulos; 
2. Foi feita a conexão com o PowerBI e o banco de dados do MySQL;
3. Foram Adicionadas três consultas, uma para cada dataset, ao dashboard online do Power BI;
4. A busca será feita em loop (indefinidamente).
