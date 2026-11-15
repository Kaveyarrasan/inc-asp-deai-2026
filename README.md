<!-- # Utitlizing Git from Databricks

**Leveraging Databricks Platform**

- Initially session begins with simple operations such as
    - Creating structured format markdown content in notebook by running magic command '%md'
    - Running magic commands to invoke & perform SQL, Python & Shell operation
- Later moves to core operation such as Spark SQL, Streaming
 -->

## Driven with Use Cases

### Use Case 1: Exploring Notebooks & Magic Commands

**Folder:** `Assignments/1_Usecase_Explore_Notebooks_magic_commands`

Hands-on walkthrough of Databricks notebook magic commands through 12 tasks:

| Task | Magic Command | What Was Done |
| --- | --- | --- |
| Task 1 | `%md` | Authored a structured article on the evolution of data management technologies (flat files → RDBMS → Data Warehouse → Big Data → Data Lake → Lakehouse → AI-native platforms) with timeline tables and LaTeX formatting |
| Task 2 | `%sql` | Created the Unity Catalog volume `workspace.default.usage_metrics` and verified it via `SHOW CATALOGS`, `SHOW SCHEMAS`, `SHOW VOLUMES` |
| Task 3 | `%py` | Created child notebook `4_child_nb_dataload`; pulled the mobile OS usage dataset from a public Tableau API endpoint using `requests` and wrote it into the volume via `dbutils.fs.put` |
| Task 4 | `%run` | Called the child notebook `4_child_nb_dataload` from the parent notebook |
| Task 5 | `%fs` | Listed the files in the `usage_metrics` volume (`%fs ls`) and previewed the CSV with `%fs head` |
| Tasks 6–8 | `%python` | Built a PySpark DataFrame (`df1`) from the CSV, renamed columns, wrote it to the table `default.mobile_os_usage` via `saveAsTable`, and read it back with `spark.sql` |
| Tasks 9–11 | `%pip` / `%python` | Defined a `convert_uppercase()` Python function, installed pandas via `%pip install pandas`, and read the volume CSV with `pd.read_csv` |
| Task 12 | `%sh` | Executed a Linux shell `echo` command confirming all magic command tasks completed |

**Key takeaways:** mixing SQL, Python, PySpark, shell, pip, run, and file-system magic commands within a single notebook workflow; loading external API data into a Unity Catalog Volume; and promoting volume files into a managed Delta table.

### Use Case 2: Healthcare Data Utilities (Markdown, dbutils & Widgets)

**Notebook:** `Assignments/2_Usecase_md_dbutils_widgets/2_Usecase_md_dbutils_widgets`

A healthcare-themed data pipeline demonstrating notebook design with Markdown and Databricks utilities on Volumes:

* Created the volume `inc_asp_volume_wd38` and the folder structure `raw`, `processed`, `archive` using `dbutils.fs.mkdirs`
* Generated a sample healthcare CSV (patient data) and wrote it to the raw folder with `dbutils.fs.put`, then validated it by reading with `spark.read.csv`
* Explored file operations: `dbutils.fs.ls`, `dbutils.fs.cp` (raw → processed), and `dbutils.fs.mv` (processed → archive)
* Parameterized execution with `dbutils.widgets`: dropdown widgets (`Environment`: dev/qa/prod, `Stage`: Raw/Processed/Archive), text widget (owner name), `dbutils.widgets.get`, and `dbutils.widgets.getAll`
* Driven widget-based logic: moving the processed file to archive based on the selected Stage widget value
* Demonstrated `dbutils.notebook.run` to invoke the child notebook and `dbutils.notebook.exit` to return execution status

**Key takeaways:** notebook design with Markdown, file lifecycle management (raw → processed → archive) on Volumes, and parameterizing notebook execution with widgets and `dbutils`.