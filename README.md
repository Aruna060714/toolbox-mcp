## MongoDB & Supabase Toolbox

This project demonstrates how to build a MongoDB and Supabase-backed tool system using the Toolbox framework. It allows you to query both MongoDB database and Supabase REST API through a Toolbox server, with tools defined in a YAML configuration file (tools.yaml).

## Project Structure
    .
    ├── toolbox.py            # Client script that connects to Toolbox server for MongoDB queries
    ├── supabase.py           # Client script that connects to Toolbox server for Supabase queries
    ├── tools.yaml            # Toolbox configuration (sources + tools for both MongoDB and Supabase)
    ├── docker-compose.yaml   # Docker config to run MongoDB + Toolbox server

## Data Sources
- **MongoDB**: Stores user data (email, name, etc.)
- **Supabase**: Stores product data with REST API endpoints

## Available Tools
1. **get_user_profile**: Query MongoDB for user profiles by email address
2. **get_product_by_ref**: Fetch product details from Supabase by product reference
3. **get_product_by_barcode**: Fetch product details from Supabase by barcode

## Workflow Overview
1. MongoDB stores user data, Supabase stores product data
2. tools.yaml defines tools to query both data sources
3. Toolbox Server (runs on http://localhost:5000) exposes these tools as an API
4. toolbox.py → connects to Toolbox server for MongoDB queries
5. supabase.py → connects to Toolbox server for Supabase product queries

## Environment Variables (.env file)
Create a `.env` file in the project root with the following variables:

```env
# MongoDB Connection
MONGODB_URI=<YOUR MONGODB_URI>

# Supabase Configuration
SUPABASE_URL=<YOUR SUPABASE_URL>
SUPABASE_API_KEY=<your-supabase-anon-key>
```
## Setup Instructions
1. **Create & Activate Python Virtual Environment**:
    ```bash
    python -m venv venv
    ```

    To activate:
    - Windows: `venv\Scripts\activate`
    - macOS/Linux: `source venv/bin/activate`

2. **Install Python Dependencies**:
    ```bash
    pip install toolbox-core
    ```

3. **Start Services with Docker**
    ```bash
    docker-compose up -d
    ```

    This will:
    - Start a MongoDB container
    - Start a Toolbox server on http://localhost:5000, using tools.yaml

4. **Run Toolbox Clients**
    - For MongoDB queries:
      ```bash
      python toolbox.py
      ```
      - Connects to Toolbox server (http://localhost:5000)
      - Loads the get_user_profile tool
      - Calls it with email="john@example.com"
      - Prints the result as JSON

    - For Supabase product queries:
      ```bash
      python supabase.py
      ```
      - Connects to Toolbox server (http://localhost:5000)
      - Loads both product query tools (by ref and by barcode)
      - Executes queries and prints results

## Example Outputs

**MongoDB Query Output**:
```json
{
  "_id": {
    "$oid": "689d9a9d234aacd0c6661a7e"
  },
  "age": 30,
  "email": "john@example.com",
  "name": "John Doe",
  "role": "designer"
}

**Supabase Query Output:**
    Supabase tools loaded successfully
    Searching by ref...
    Results by ref: [{...product data...}]
    Searching by barcode...
    Results by barcode: [{...product data...}]