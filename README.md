# Desafio - Processando e Transformando Dados com Power BI

Neste projeto, criei um banco de dados MySql no Azure, inseri dados e integrei o banco de dados com Workbanch e Power BI,
Faço ETL para poder transformar os dados para trazer tabelas de fatos e tabelas de dimensões para obter melhor desempenho dos dados na hora de criar relacionamentos e criar as métricas necessárias para uma análise mais consistente dos dados.

## Lista de tabelas criadas:

- dCalendario: criado através da função "CALENDARAUTO()" utilizando a linguagem dax;
- dDept: Tabela de dimensões criada para introduzir dados relacionados ao departamento. Para introduzir esta tabela foi criada uma consulta SQL:
"Selecione d.Dnumber como DeptId, d.Dname como Departamento, Dept_create_date como DataCriacaoDept
do departamento d;”
- dProjeto: Crie tabelas de dimensões para conter dados sobre projetos.
- dGerentes: Criei uma tabela de dimensões com o objetivo de permitir que os gestores façam referência a departamentos e projetos, criei uma consulta SQL para esta tabela:

- "select d.Mgr_ssn as GerenteId, concat(e.Fname, " ", e.Minit, " ", e.Lname) as Gerente, d.Mgr_start_date as DataInicioGerente, 
		d.Dname as Departamento
from departament d
left join dept_locations dl on dl.Dnumber = d.Dnumber
inner join employee e on e.ssn = d.Mgr_ssn;"
- dColaboradores: Tabela criada para trazer as informações referente dos colaboradores, foi criada uma query SQL: 
"select Ssn, concat(Fname, " ", Minit, " ", Lname) as Name, Salary, Dno, Super_ssn, Bdate, Sex, Address from employee;"
- fWorkson: tabela fato para trazer melhor dados referente aos colaboradores, horas e salario, para ela houve os seguinte passos:
criação de uma query SQL para trazer os dados que realmente necessitava "select Ssn, concat(Fname, " ", Minit, " ", Lname) as Name, Salary, Dno, Super_ssn, Bdate, Sex, Address from employee;", depois disso, faça uma “substituição de valor” nos valores nulos existentes na coluna Super_ssn e depois faça uma consulta de mesclagem com a tabela WorsOn para obter dados relacionados às horas de trabalho dos funcionários.
