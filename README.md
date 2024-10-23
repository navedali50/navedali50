import streamlit as st
import pandas as pd

st.title("Study Tracker")

# DataFrame Initialization
data = {'Date': [], 'Task': [], 'Duration (hours)': []}
df = pd.DataFrame(data)

# Add Task
task = st.text_input('Enter Task')
duration = st.number_input('Enter Duration (hours)', min_value=0.0, step=0.5)
if st.button('Add Task'):
    df = df.append({'Date': pd.Timestamp.now(), 'Task': task, 'Duration (hours)': duration}, ignore_index=True)
    st.success(f"Added task: {task}")

# Display DataFrame
st.write("Tasks:", df)

# Save and Load
if st.button('Save Data'):
    df.to_csv('study_data.csv', index=False)
    st.success("Data saved successfully!")

if st.button('Load Data'):
    df = pd.read_csv('study_data.csv')
    st.write("Loaded data:", df)

# Plot Study Time
if st.button('Plot Study Time'):
    st.bar_chart(df.set_index('Date')['Duration (hours)'])



