# Projeto 3

Nesse projeto foi criado um Banco de Dados MySql no Azure, inserindo os dados e também integrando esse banco de dados com o Workbanch e o Power BI,
Fiz o ETL para poder tranformar os dados para trazer tabelas fatos e dimensões para assim ter melhor desempenho dos dados na hora de criar os relacionamento e também quando fazer a criação das metricas necessarias para fazer uma análise mas coerente dos dados.
Lista de tabelas criadas:
- dCalendario: foi criada na linguagem dax com a função "CALENDARAUTO()";
- dDept: tabela dimensão criada com o intuito de trazer os dados referente aos departamentos, para trazer essa tabela foi criada uma query SQL:
"select d.Dnumber as DeptId, d.Dname as Departamento, Dept_create_date as DataCriacaoDept
from departament d;"
- dProjeto: tabela dimensão criada para conter os dados sobre os projetos.
- dGerentes: tabela dimensão criada com intuito de trazer os gerentes refernte aos departamentos e projetos, para trazer essa tabela foi criada uma query SQL:
- "select d.Mgr_ssn as GerenteId, concat(e.Fname, " ", e.Minit, " ", e.Lname) as Gerente, d.Mgr_start_date as DataInicioGerente, 
		d.Dname as Departamento
from departament d
left join dept_locations dl on dl.Dnumber = d.Dnumber
inner join employee e on e.ssn = d.Mgr_ssn;"
- dColaboradores: Tabela criada para trazer as informações referente dos colaboradores, foi criada uma query SQL: 
"select Ssn, concat(Fname, " ", Minit, " ", Lname) as Name, Salary, Dno, Super_ssn, Bdate, Sex, Address from employee;"
- fWorkson: tabela fato para trazer melhor dados referente aos colaboradores, horas e salario, para ela houve os seguinte passos:
criação de uma query SQL para trazer os dados que realmente necessitava "select Ssn, concat(Fname, " ", Minit, " ", Lname) as Name, Salary, Dno, Super_ssn, Bdate, Sex, Address from employee;", após isso houve uma "replace value" para os valores nulos existentes na coluna Super_ssn, depois foi feito um merge queries com a tabela WorsOn para trazer os dados referentes as horas trabalhadas pelos colaboradores.

esses foram os passos do ETL feito nesse projeto, desde a criação do banco de dados na Azure até o carregamento dos dados para criação do relatório.
