# Financial Statement Report (DRE) in Power BI


![11](https://github.com/user-attachments/assets/b3a66cb8-cd4f-4a69-b8a2-83099f776a86)


## 1. Explanation of DRE
**The Statement of Income for the Year (DRE)** is an accounting report detailing the financial performance of an organization over a specific period. It organizes revenues, costs, expenses, and profits, offering a clear view of the company's operating and net results.  
In this project, the DRE was implemented in Power BI to:  
- Facilitate visualization and analysis of financial data.  
- Increase agility in generating periodic reports.  
- Enable continuous monitoring of the company's financial health.  

## 2. Technical Details  

### 2.1. ETL Process (Extract, Transform, and Load)  
#### **Data Sources**  
All data for creating the DRE in Power BI was consolidated in an Excel file that centralized the necessary information, including:  
- **Financial data exported from ERP:**  
  - Information on revenues, expenses, costs, and other financial details categorized by cost center, accounts, and dates.  
  - Organized in a dedicated Excel sheet.  
- **Historical data and reference tables:**  
  - Information on accounting categories used for detailed analyses.  
  - Available in complementary sheets within the same file.  
- Power BI handles multiple data formats seamlessly.

![1](https://github.com/user-attachments/assets/544350b8-3c38-4e6e-b7bd-a94d40d23a3d)


---

### 2.2. Integration with Power BI  
#### **Transformation in Power Query**  

![2](https://github.com/user-attachments/assets/5054b254-262e-4f36-9055-676f4da48896)


In Power Query, data was processed to ensure quality and consistency before modeling. Key steps include:  
- **Data Cleaning:**  
  - **Duplicate record removal:** Verified by combining keys such as dates or specific identifiers.
    
 ![3](https://github.com/user-attachments/assets/d06808e8-48f1-4878-a853-861a222c6198)

    
  - **Null value handling:** Missing data replaced with zeros or default values.  
- **Data Normalization:**  
  - Uniform formatting for numbers and dates to prevent modeling errors.

 ![4](https://github.com/user-attachments/assets/0f0e77d4-d106-4aa7-b730-340e4401d200)

  
  - Conversion of monetary values to decimal format using locale-specific separators.  
- **Loading:**  
  After treatment, tables were loaded into the Power BI tabular model with relationships optimized for performance.  

#### **Data Modeling**  
The model followed a star schema, with fact and dimension tables connected via foreign key relationships.  

![5](https://github.com/user-attachments/assets/2f263f4b-1162-4023-8e3f-d11e2b982e4d)


---

### Tabelas e Conexões  
#### **Fact Table (DRE)**  
The fact table contains transactional data related to financial values, periods, and account and cost center IDs.  
- **Key Fields:**  
  - `Cod.DRE`  
  - `Description`  
  - `Operation`  
  - `Type`  
- **Connections:**  
  - Related to `MapaDRE` via the `Cod.DRE` key.  

#### **Dimension Table (Calendar)**  
The calendar table maps fiscal dates and contains information like year, month, and quarter for temporal analysis.  

![6](https://github.com/user-attachments/assets/58b8b9d9-0c4e-42ef-8ef8-5180d5fa49a4)


- **Connection:**  
  - Linked to the `Fact Table (DRE)` via the `Date` key.  

#### **Chart of Accounts Table (PlanoContas)**  
This table provides detailed information on accounts, such as account name and type, used to classify transactions.  
- **Key Fields:**  
  - `Cod.ContaContábil`  
  - `AccountName`  
  - `Category`  
- **Connection:**  
  - Linked to `MapaDRE` via `Cod.ContaContábil`.  

#### **Mapping Table (MapaDRE)**  
The mapping table includes the DRE structure, account descriptions, and operation categories.  
- **Key Fields:**  
  - `Cod.DRE`  
  - `Cod.ContaContábil`  
- **Connections:**  
  - Linked to `Fact Table (DRE)` via `Cod.DRE`.  
  - Linked to `PlanoContas` via `Cod.ContaContábil`.  
  - Linked to `Transactions` via `Cod.ContaContábil`.  

#### **Transaction Table (Lançamentos)**  
This table logs financial transactions, associating them with accounts and values.  
- **Key Fields:**  
  - `Cod.ContaContábil`  
  - `Date`  
  - `Value`  
- **Connection:**  
  - Linked to `MapaDRE` via `Cod.ContaContábil`.  

#### **VH Analysis Table**  
Used for dynamic segmentation, enabling vertical (e.g., cost centers, accounts) and horizontal (period-based) analyses.  

---

#### **Relationship Diagram**  
The Power BI diagram ensures efficient data flow with:  
- **Unidirectional relationships:** Avoids ambiguity and enhances performance.

![7](https://github.com/user-attachments/assets/ed2d322b-84d1-4e01-9ca6-7b1b695a0fc6)



- **Cascading filters:** Allows dimension selections (e.g., year) to dynamically update fact table values.  

---

### 2.3. Calculations and Metrics  
#### **Horizontal Analysis (Period Variations):**  
This metric calculates percentage variations between a metric's current year value and the previous year, highlighting trends.  

![9](https://github.com/user-attachments/assets/8ef37511-de14-4f66-9aad-8066dfac7f0a)

#### **Vertical Analysis (Proportion by Gross Revenue):**  
This metric calculates a metric's percentage share relative to the gross revenue total, revealing the contribution of specific items.  

![10](https://github.com/user-attachments/assets/2f7d8dd2-f27a-41fc-9bf2-21d2abffce25)

---

## 3. Dashboard Screens Description  

![11](https://github.com/user-attachments/assets/bb9115ab-4ead-4369-b022-92c4262bc77f)


### Main Elements  
#### **Header and Title**  
- The title **"DRE MANAGERIAL"** identifies the report's purpose.  
- Filters include:  
  - **Date Selection:** Fields to set the analysis period.

 ![12](https://github.com/user-attachments/assets/eae5b149-6a00-4aab-afcf-a6cc0ddd3b9e)

    
  - **Analysis Control:** Radio buttons to toggle between horizontal and vertical analysis.  

#### **Data Table**  
Displays financial data by year, with consolidated total columns.  
- **Components:**  
  - `Year`: Financial results by period.  
  - `Description`: Financial items categorized (e.g., revenues, expenses).  
  - `DRE`: Absolute values of each financial item.  
  - `%`: Relative percentages based on selected analysis.  
  - `Total DRE`: Consolidated values for all years.  

#### **Analysis Types**  
- **Horizontal:** Highlights year-over-year trends.  
- **Vertical:** Focuses on the composition of a single year's data.  

![13](https://github.com/user-attachments/assets/4d82ab2b-ed7d-498c-9626-1286296d9e89)


---

## 4. Data Security  

Financial data is handled securely with robust practices, such as:  
- **Permission Management:**  
  - Reports are available only to specific Power BI Pro accounts.  
- **Centralization:**  
  - Data is stored in a centralized database with controlled access.  
- **Monitoring:**  
  - Power BI access logs and audit trails are utilized to identify and track suspicious activities.  

---

## 5. Project Benefits  

The implementation of the DRE in Power BI offers several advantages:  
- **Automation:**  
  - Reduces manual tasks and accelerates the analysis process.  
- **Consistency:**  
  - Standardizes reports, making it easier to compare data across different periods.  
- **Flexibility:**  
  - Allows for dynamic analyses with customizable filters to adapt to various needs.  
- **Reliability:**  
  - Minimizes human errors through automated calculations, ensuring accurate results. 
