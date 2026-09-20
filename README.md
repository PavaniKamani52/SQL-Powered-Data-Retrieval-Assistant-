**SQL Voice Assistant – LLM-Powered Data Retrieval & Visualization**

An AI-powered Streamlit application that allows users to interact with a database using natural language instead of manually writing SQL queries.

Users can enter their questions through text or speech. The application uses an EURI LLM to convert the natural-language question into an executable SQL query, retrieves the required data from a PostgreSQL database hosted on Neon, and presents the results in both tabular and interactive visual form.

**🚀 Key Features**
🎙️ Speech-to-Text: Accepts voice input and converts speech into text.
🧠 Natural Language to SQL: Uses the EURI LLM to convert user questions into SQL queries.
🗄️ Database Integration: Connects to PostgreSQL using SQLAlchemy, with PostgreSQL hosted on Neon.
🔗 Complex Query Support: Handles queries involving multiple tables and joins.
📊 Automatic Visualization: Converts query results into Pandas DataFrames and uses predefined conditions to select an appropriate visualization.
📈 Interactive Charts: Uses Plotly to generate interactive bar charts, line charts, scatter plots, and histograms.
🔐 Secure Configuration: Stores database credentials and API keys using environment variables.
⚡ Modular Architecture: Separates the UI, database/LLM logic, configuration, and prompt template.
**🏗️ Architecture Flow**
                User
             /       \
          Text       Speech
            \         /
             ↓       ↓
            Streamlit UI
                 ↓
          Speech-to-Text
            (if needed)
                 ↓
       Database Schema Extraction
                 ↓
       Prompt + Schema + Question
                 ↓
             EURI LLM
                 ↓
        Generated SQL Query
                 ↓
            SQLAlchemy
                 ↓
       Neon PostgreSQL Database
                 ↓
          Query Results
                 ↓
        Pandas DataFrame
                 ↓
      Visualization Selection Logic
                 ↓
              Plotly
                 ↓
       Interactive Visualization

**🛠️ Tech Stack**
| Technology                      | Purpose                                     |
| ------------------------------- | ------------------------------------------- |
| **Python 3.10**                 | Core programming language                   |
| **Streamlit**                   | Web application and UI                      |
| **EURI GPT-4.1 Nano**           | Natural-language-to-SQL generation          |
| **SQLAlchemy**                  | Database connectivity and SQL execution     |
| **PostgreSQL**                  | Relational database                         |
| **Neon**                        | Cloud-hosted/serverless PostgreSQL platform |
| **Pandas**                      | DataFrame-based result processing           |
| **Plotly**                      | Interactive data visualization              |
| **SpeechRecognition + PyAudio** | Speech-to-text input                        |
| **python-dotenv**               | Environment variable management             |

**📊 Visualization Logic****

After retrieving the query results, the application converts them into a Pandas DataFrame.
The application then examines the DataFrame and selects a visualization based on its structure:

Date/time column → Line chart
2 columns → Bar chart
3 columns → Scatter plot
1 column → Histogram

Plotly Express is then used to create the interactive visualization, which is displayed through Streamlit.

**🔄 How the Application Works**
1. User Input
The user enters a question through text or speech.
Example:
"Show me the employees in the IT department."

2. Schema Extraction
The application retrieves information about the database tables and their columns.

3. LLM Processing
The database schema, prompt instructions, and user's question are provided to the EURI LLM.
The LLM generates an SQL query such as:
SELECT * 
FROM employees
WHERE department = 'IT';

4. Query Execution
The generated SQL query is executed against the PostgreSQL database hosted on Neon, using SQLAlchemy.

5. Result Processing
The returned data is converted into a Pandas DataFrame.

6. Visualization
Your application checks the DataFrame structure and selects an appropriate chart.
For example:
Date + Sales
     ↓
Line Chart

7. Output
The user receives:
SQL Query + Tabular Result + Visualization

**📁 Project Structure**
project/
│
├── app.py
├── utills.py
├── config.py
├── prompt_template.txt
├── requirements.txt
└── .env

app.py
→ Streamlit UI and main application workflow
utills.py
→ Database schema extraction, EURI API interaction, SQL execution, and supporting functions
config.py
→ Environment/configuration handling
prompt_template.txt
→ Prompt instructions used for generating SQL
.env
→ Database URL and EURI API key

**🔐 Environment Variables**
DATABASE_URI=your_database_uri
EURI_API_KEY=your_api_key

Sensitive credentials are kept outside the source code using environment variables.

**⚙️ Installation**
conda create -n sqlvoice python=3.10
conda activate sqlvoice

pip install -r requirements.txt

streamlit run app.py






