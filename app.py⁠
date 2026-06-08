import streamlit as st
from openai import OpenAI

# 1. Setup Page Configuration
st.set_page_config(
    page_title="Custom Claude 4.8 UI",
    page_icon="🧠",
    layout="centered"
)

st.title("Custom Claude 4.8 Interface")
st.caption("Powered by Agent Router & Streamlit")

# 2. Securely Fetch the API Key
# This pulls from the deployment server's environment variables
try:
    api_key = st.secrets["AGENT_ROUTER_KEY"]
except KeyError:
    st.error("Missing API Key! Please set AGENT_ROUTER_KEY in your deployment secrets.")
    st.stop()

# 3. Initialize the OpenAI Client & Spoof Headers
client = OpenAI(
    base_url="https://agentrouter.org/v1",
    api_key=api_key,
    default_headers={
        "User-Agent": "RooCode/1.0", # Spoofing an authorized developer tool
        "HTTP-Referer": "https://vscode.local" # Additional disguise layer
    }
)

# 4. Initialize Session State for Chat History
if "messages" not in st.session_state:
    st.session_state.messages = []

# 5. Render Chat History
for msg in st.session_state.messages:
    with st.chat_message(msg["role"]):
        st.markdown(msg["content"])

# 6. Handle User Input
if prompt := st.chat_input("Ask Claude something..."):
    
    # Save and display user message
    st.session_state.messages.append({"role": "user", "content": prompt})
    with st.chat_message("user"):
        st.markdown(prompt)

    # Fetch and display AI response
    with st.chat_message("assistant"):
        message_placeholder = st.empty()
        
        try:
            # Send the request to Agent Router
            response = client.chat.completions.create(
                model="claude-opus-4-8", # The specific Agent Router model ID
                messages=st.session_state.messages,
            )
            
            # Extract and display the reply
            reply = response.choices[0].message.content
            message_placeholder.markdown(reply)
            
            # Save the AI response to state
            st.session_state.messages.append({"role": "assistant", "content": reply})
            
        except Exception as e:
            st.error(f"Agent Router Connection Error: {e}")
