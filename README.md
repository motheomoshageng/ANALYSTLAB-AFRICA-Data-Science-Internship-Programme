Employee Attrition Analysis
AnalystLab Africa - Week 1 Assignment
📋 Project Overview
This project analyzes employee attrition for ABC Manufacturing Ltd using the IBM HR Analytics Employee Attrition & Performance dataset. The analysis explores workforce composition, identifies departments and roles with the highest turnover, and uncovers key factors contributing to employee departures. This foundational analysis establishes the business case for predictive machine learning models to support proactive HR decision-making.

Project Type: Exploratory Data Analysis (EDA)
Domain: Human Resources Analytics
Organization: AnalystLab Africa Consulting
Internship Program: Data Science Internship Programme (Week 1)

🎯 Learning Objectives
Understand the business problem of employee attrition

Inspect and understand a real-world HR dataset

Perform initial exploratory data analysis

Create meaningful visualizations

Generate business-focused insights

Communicate findings professionally

📊 Business Questions Addressed
Workforce Composition: What does the company's workforce look like?

Department Analysis: Which departments have the highest employee attrition?

Age Impact: Does age influence attrition?

Income Impact: Does monthly income affect retention?

Overtime Impact: Does overtime influence attrition?

Role Analysis: Which job roles experience the highest turnover?

Predictive Variables: Which variables appear important for future predictive modelling?

📁 Dataset Information
Source: IBM HR Analytics - Employee Attrition & Performance (Kaggle)
Records: 1,470 employee records
Variables: 35 features
Target Variable: Attrition (Yes/No)
Attrition Rate: 16.1% (237 employees left, 1,233 stayed)

Variable Categories
Category	Variables
Personal Attributes	Age, Education, Education Field, Gender, Marital Status
Job-Related	Department, Job Role, Job Level, Business Travel, Overtime, Monthly Income
Satisfaction	Job Satisfaction, Environment Satisfaction, Work-Life Balance
Career	Years at Company, Years in Current Role, Years Since Last Promotion, Total Working Years
🔍 Key Findings
Workforce Observations
Young Workforce: Average employee age is 37 years, with majority in 30-43 age range

Department Distribution: R&D (65.4%), Sales (30.3%), HR (4.3%)

Compensation Variation: Monthly income ranges from $1,009 to $19,999

Work-Life Balance: 28.3% of employees work overtime

Moderate Tenure: Average tenure is 7 years at the company

Factors Contributing to Attrition
Factor	Key Finding
Department	Sales has highest attrition (20%)
Job Role	Sales Representatives have 35%+ attrition
Overtime	3x higher attrition rate for overtime employees
Compensation	Leavers earn $25,000+ less annually
Age	Younger employees (<35) more likely to leave
📈 Visualizations
Bar Charts
Attrition by Department

Attrition by Job Role

Attrition by Overtime

Histograms
Age Distribution

Monthly Income Distribution

Boxplots
Age by Attrition Status

Monthly Income by Job Role and Attrition

Pie Charts
Department Distribution

Overall Attrition Distribution

🛠️ Technologies Used
Tool/Library	Purpose
Python 3.8+	Programming language
Pandas	Data manipulation and analysis
NumPy	Numerical operations
Matplotlib	Data visualization
Seaborn	Statistical visualization
Jupyter Notebook	Interactive development environment
📁 Project Structure
text
analystlab-week1/
│
├── Week1_Employee_Attrition_Analysis.ipynb   # Main Jupyter Notebook
├── Business_Understanding_Report.pdf         # Business context and problem framing
├── Dataset_Inspection_Report.pdf             # Data quality assessment
├── Reflection_Report.pdf                     # Learning experience documentation
│
├── visualizations/                           # Output visualizations
│   ├── attrition_by_department.png
│   ├── attrition_by_jobrole.png
│   ├── attrition_by_overtime.png
│   ├── age_distribution.png
│   ├── income_distribution.png
│   ├── age_boxplot.png
│   ├── income_by_role_boxplot.png
│   └── department_pie.png
│
└── README.md                                 # Project documentation
🚀 Installation and Setup
Prerequisites
Python 3.8 or higher

Jupyter Notebook or JupyterLab

Git (for cloning repository)

Clone Repository
bash
git clone https://github.com/yourusername/analystlab-week1.git
cd analystlab-week1
Install Dependencies
bash
pip install pandas numpy matplotlib seaborn jupyter
Run Jupyter Notebook
bash
jupyter notebook Week1_Employee_Attrition_Analysis.ipynb
📊 Usage Instructions
Open the Notebook: Launch Jupyter and open Week1_Employee_Attrition_Analysis.ipynb

Run All Cells: Execute all cells sequentially using Run > Run All

Review Outputs: Examine visualizations and statistical summaries

Read Reports: Review PDF reports for business context and findings

📝 Reports Included
Report	Description
Business Understanding Report	Research on employee attrition, business impact, and data science applications
Dataset Inspection Report	Data quality assessment, variable summaries, and key statistics
Reflection Report	Personal learning experience and key takeaways
💡 Key Insights for ABC Manufacturing
Immediate Recommendations
Review Overtime Policies: Overtime employees are 3x more likely to leave

Conduct Pay Equity Audit: Leavers earn $25,000+ less than stayers

Focus on Sales Department: Highest attrition rate (20%)

Target Young Professionals: Early-career employees (25-35) at highest risk

Develop Career Pathways: Clear progression for high-turnover roles

Future Predictive Modeling
Variables identified as important for future models:

Overtime (strongest predictor)

Monthly Income

Age

Job Role

Department

Years at Company

📈 Sample Visualizations
Attrition by Overtime
Employees working overtime have approximately 30% attrition rate compared to 10% for those who don't work overtime.

Age by Attrition
Leavers have a median age of 31 years compared to 37 years for stayers.

🔮 Future Work
Predictive Modeling: Build machine learning models to predict employee attrition

Feature Engineering: Create new features from existing variables

Model Deployment: Deploy model as a dashboard for HR monitoring

Intervention Testing: A/B test retention strategies

ROI Analysis: Measure financial impact of retention initiatives

