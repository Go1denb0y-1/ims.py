import streamlit as st
import pandas as pd

st.set_page_config(page_title="IMS Dashboard Prototype", layout="wide")

# Dummy inventory data
inventory = pd.DataFrame([
    {"Item ID": "A001", "Name": "Laptop", "Category": "Electronics", "Stock": 12},
    {"Item ID": "A002", "Name": "Keyboard", "Category": "Accessories", "Stock": 3},
    {"Item ID": "A003", "Name": "Mouse", "Category": "Accessories", "Stock": 25},
    {"Item ID": "A004", "Name": "Monitor", "Category": "Electronics", "Stock": 1},
])

# Sidebar Navigation
page = st.sidebar.selectbox("Navigation", ["Dashboard", "Add Item", "Update Stock", "Low Stock Report"])

# Title
st.title("Inventory Management System - Prototype UI")

# ---------------------- Dashboard ----------------------
if page == "Dashboard":
    st.subheader("Live Inventory Overview")

    # Highlight low stock rows
    def highlight_low(s):
        return ["background-color: #ffcccc" if v < 5 else "" for v in s]

    st.dataframe(
        inventory.style.apply(highlight_low, subset=["Stock"]),
        use_container_width=True
    )


# ---------------------- Add Item ----------------------
elif page == "Add Item":
    st.subheader("Add New Inventory Item")

    col1, col2 = st.columns(2)
    with col1:
        item_id = st.text_input("Item ID")
        item_name = st.text_input("Item Name")
    with col2:
        category = st.selectbox("Category", ["Electronics", "Accessories", "Clothing", "Other"])
        starting_stock = st.number_input("Starting Stock", min_value=0)

    if st.button("Add Item"):
        st.success("Item successfully added (prototype).")


# ---------------------- Update Stock ----------------------
elif page == "Update Stock":
    st.subheader("Add or Remove Stock")

    item = st.selectbox("Select Item", inventory["Name"])
    action = st.radio("Action", ["Add Stock", "Remove Stock"])
    amount = st.number_input("Amount", min_value=1)

    if st.button("Update"):
        if action == "Add Stock":
            st.success(f"Added {amount} units to {item}. (prototype)")
        else:
            st.warning(f"Removed {amount} units from {item}. (prototype)")


# ---------------------- Low Stock Report ----------------------
elif page == "Low Stock Report":
    st.subheader("Low Stock Items (Less than 5 left)")

    low_stock = inventory[inventory["Stock"] < 5]

    if low_stock.empty:
        st.success("No items are currently low on stock.")
    else:
        st.dataframe(low_stock, use_container_width=True)
