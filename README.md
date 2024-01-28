import pandas as pd
import pyodbc

# Define the connection parameters
server = 'Yrkmill-trux01'
database = 'TRUX_MT_COMP'
username = 'dwuser'
password = 'xxx'

# Construct the connection string
conn_str = f'DRIVER={{SQL Server}};SERVER={server};DATABASE={database};UID={username};PWD={password}'

# Establish a connection to the database
conn = pyodbc.connect(conn_str)
print("Connection established successfully!")

# Create a cursor to execute SQL commands
cursor = conn.cursor()

# Example: Execute a SQL command
cursor.execute("SELECT * FROM LM02 where LM02.LM02_date > '2024/01/01' ")

# Fetch all rows
rows = cursor.fetchall()

# Get the column names from the cursor description
columns = [column[0] for column in cursor.description]

# Convert rows to DataFrame
df = pd.DataFrame.from_records(rows, columns=columns)

# Print the DataFrame
print(df)

# Close the cursor and connection
cursor.close()
conn.close()
