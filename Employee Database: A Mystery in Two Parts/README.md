# **A Mystery in Two Parts**

## **Background**
It is a beautiful spring day, and it is two weeks since you have been hired as a new data engineer at Pewlett Hackard. Your first major task is a research project on employees of the corporation from the 1980s and 1990s. All that remain of the database of employees from that period are six CSV files.
In this assignment, you will design the tables to hold data in the CSVs, import the CSVs into a SQL database, and answer questions about the data. In other words, you will perform:
  1. Data Modeling
  2. Data Engineering
  3. Data Analysis


**Data Modeling**
  -Inspect the CSVs and sketch out an ERD of the tables. Feel free to use a tool like http://www.quickdatabasediagrams.com.

![](sql-challenge/QuickDBD-Schemata.png)

**Data Engineering**
  -Use the information you have to create a table schema for each of the six CSV files. Remember to specify data types, primary keys, foreign keys, and other constraints.
  -Import each CSV file into the corresponding SQL table. (Schemas->Create Table->Name Table->Assign Columns with Names, Data Types, Length, Not Null, Primary Key->Upload CSV File.)
   
**Data Analysis**
Once you have a complete database, do the following:

  **1. List the following details of each employee: employee number, last name, first name, gender, and salary.**

SELECT employees.emp_no, employees.last_name, employees.first_name, employees.gender, salaries.salary\
FROM employees\
JOIN salaries\
ON employees.emp_no = salaries.emp_no;

  **2. List employees who were hired in 1986.**

SELECT * FROM employees\
WHERE hire_date LIKE '1986%';

  **3. List the manager of each department with the following information: department number, department name, the manager's employee number, last name, first name, and start and end employment dates.**

SELECT departments.dept_no, departments.dept_name, dept_manager.emp_no, employees.last_name, employees.first_name, dept_manager.from_date, dept_manager.to_date\
FROM departments\
JOIN dept_manager\
ON departments.dept_no = dept_manager.dept_no\
JOIN employees\
ON dept_manager.emp_no = employees.emp_no;

  **4. List the department of each employee with the following information: employee number, last name, first name, and department name.**

SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name\
FROM dept_emp\
JOIN employees\
ON dept_emp.emp_no = employees.emp_no\
JOIN departments\
ON dept_emp.dept_no = departments.dept_no;

  **5. List all employees whose first name is "Hercules" and last names begin with "B."**

SELECT * FROM employees\
WHERE first_name LIKE 'Hercules'\
AND last_name LIKE 'B%';

  **6. List all employees in the Sales department, including their employee number, last name, first name, and department name.**

SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name\
FROM dept_emp\
JOIN employees\
ON dept_emp.emp_no = employees.emp_no\
JOIN departments\
ON dept_emp.dept_no = departments.dept_no\
WHERE departments.dept_name = 'Sales';

  **7. List all employees in the Sales and Development departments, including their employee number, last name, first name, and department name.**

SELECT dept_emp.emp_no, employees.last_name, employees.first_name, departments.dept_name\
FROM dept_emp\
JOIN employees\
ON dept_emp.emp_no = employees.emp_no\
JOIN departments\
ON dept_emp.dept_no = departments.dept_no\
WHERE departments.dept_name = 'Sales'\
OR departments.dept_name = 'Development';

  **8. In descending order, list the frequency count of employee last names, i.e., how many employees share each last name.**

SELECT last_name, COUNT(*) AS frequency\
FROM employees\
GROUP BY last_name\
ORDER BY frequency DESC;

## **Bonus**
Generate a visualization of the data by: 
  1. Importing the SQL database into Pandas. 
  2. Create a histogram to visualize the most common salary ranges for employees and average salary by title. 
  3. Summarize data engineering steps in markdown format. 
  
  
