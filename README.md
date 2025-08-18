## MongoDB Toolbox 
This project demonstrates how to build a MongoDB-backed tool system using the Toolbox framework.It allows you to query a MongoDB database through a Toolbox server, with tools defined in a YAML configuration file (tools.yaml).
## Project Structure
    .
    ├── toolbox.py            # Client script that connects to Toolbox server
    ├── tools.yaml            # Toolbox configuration (sources + tools)
    ├── docker-compose.yaml   # Docker config to run MongoDB + Toolbox server
## Workflow Overview
1. MongoDB stores user data (email, name, etc.).
2. tools.yaml defines a tool (get_user_profile) to query MongoDB by email.
3. Toolbox Server (runs on http://localhost:5000) exposes these tools as an API.
4. toolbox.py → connects to Toolbox server, calls the tool, and prints results.
## Setup Instructions
1. Create & Activate Python Virtual Environment :
    **python -m venv venv**

    To activate :
    **venv\Scripts\activate**
2. Install Python Dependencies :
    **pip install toolbox-core**
3. Start Services with Docker
    docker-compose up -d

    This will:
    - Start a MongoDB container.
    - Start a Toolbox server on http://localhost:5000, using tools.yaml.
4. Run Toolbox Client
    python toolbox.py
    - Connects to Toolbox server (http://localhost:5000).
    - Loads the get_user_profile tool.
    - Calls it with email="john@example.com".
    - Prints the result as JSON.

## Example Output
    Query result:
    {
    "_id": {
        "$oid": "689d9a9d234aacd0c6661a7e"
    },
    "age": 30,
    "email": "john@example.com",
    "name": "John Doe",
    "role": "designer"
    }