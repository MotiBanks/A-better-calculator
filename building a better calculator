import streamlit as st

st.set_page_config(page_title="Dual Calculator", layout="centered")

#  Asked gpt cause i am not familar with CSS and streamlit app is too plain
st.markdown("""
    <style>
    body {
        color: #f0f0f0;
        background-color: #0d1117;
    }
    .stTextInput, .stNumberInput, .stButton, .stSelectbox {
        color: #ffffff !important;
    }
    .stApp {
        padding: 1.5rem;
    }
    </style>
""", unsafe_allow_html=True)


st.title("🧮 Dual-Mode Calculator with History")
st.subheader("Choose between Basic and Advanced mode")


if "history" not in st.session_state:
    st.session_state.history = []


mode = st.selectbox("Select calculator mode:", ["Basic", "Advanced"])


if mode == "Basic":
    st.markdown("### Basic Mode")
    
    op = st.text_input("Enter operator (+, -, *, /)")
    num1 = st.number_input("Enter first number", key="num1")
    num2 = st.number_input("Enter second number", key="num2")
    num3 = st.number_input("Enter third number", key="num3")

    if op:
        if op == "+":
            result = num1 + num2 + num3
        elif op == "-":
            result = num1 - num2 - num3
        elif op == "*":
            result = num1 * num2 * num3
        elif op == "/":
            if num2 == 0 or num3 == 0:
                result = "❌ Error: Division by zero"
            else:
                result = num1 / num2 / num3
        else:
            result = "❌ Invalid operator"

        st.success(f"Result: {result}")
        
        
        expression = f"{num1} {op} {num2} {op} {num3}"
        st.session_state.history.append(f"{expression} = {result}")


elif mode == "Advanced":
    st.markdown("### Advanced Mode (type full expression)")
    
    expression = st.text_input("Enter your expression (e.g., 10 + 5 * 2)")

    if expression:
        try:
            result = eval(expression)
            st.success(f"Result: {result}")
            st.session_state.history.append(f"{expression} = {result}")
        except Exception as e:
            st.error(f"❌ Error: {e}")


if st.session_state.history:
    st.markdown("---")
    st.markdown("### 🧾 Calculation History")
    for calc in reversed(st.session_state.history[-5:]): 
        st.write(calc)


if st.button("Clear History"):
    st.session_state.history = []
    st.success("History cleared!")
