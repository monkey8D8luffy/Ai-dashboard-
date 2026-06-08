# Custom Claude 4.8 UI

A server-side Streamlit interface for connecting to Agent Router via custom header spoofing.

## Local Setup
1. Clone the repository.
2. Install dependencies: `pip install -r requirements.txt`
3. Create a `.streamlit/secrets.toml` file in the root directory and add your key:
   `AGENT_ROUTER_KEY = "sk-mKiG..."`
4. Run the app: `streamlit run app.py`

## Deployment Note
When deploying to platforms like Streamlit Community Cloud or Vercel, ensure you add `AGENT_ROUTER_KEY` as an environment variable or inside the platform's advanced secrets management UI.
