import streamlit as st

st.set_page_config(
    page_title="Predictive Energy Guardian",
    page_icon="⚡",
    layout="wide"
)

st.title("⚡ Predictive Energy Guardian")
st.subheader("Smart Energy Management & Peak Load Control")

st.divider()

# Peak current setting
peak_limit = st.slider(
    "Peak Current Limit (A)",
    min_value=1.0,
    max_value=20.0,
    value=5.0,
    step=0.5
)

# Simulated electrical values
voltage = st.number_input(
    "Simulated Voltage (V)",
    min_value=0.0,
    value=230.0,
    step=1.0
)

current = st.number_input(
    "Simulated Current (A)",
    min_value=0.0,
    value=2.5,
    step=0.1
)

# Calculate power
power = voltage * current

# Display electrical values
col1, col2, col3 = st.columns(3)

col1.metric("Voltage", f"{voltage:.1f} V")
col2.metric("Current", f"{current:.2f} A")
col3.metric("Power", f"{power:.1f} W")

st.divider()

# Load control
st.header("🔌 Load Status")

col1, col2 = st.columns(2)

with col1:
    st.subheader("Critical Loads")

    critical_bulb = st.checkbox(
        "💡 Critical Bulb",
        value=True
    )

    coolant_fan = st.checkbox(
        "❄️ AC Coolant Fan",
        value=True
    )

with col2:
    st.subheader("Non-Critical Loads")

    noncritical_bulb1 = st.checkbox(
        "💡 Non-Critical Bulb 1 (100 W)",
        value=True
    )

    noncritical_bulb2 = st.checkbox(
        "💡 Non-Critical Bulb 2 (100 W)",
        value=True
    )

st.divider()

# Peak detection
if current >= peak_limit:
    st.error("🔴 PEAK CURRENT LIMIT REACHED")
    st.warning(
        "The system recommends switching OFF "
        "a non-critical load."
    )
else:
    st.success("🟢 NORMAL OPERATION")

# Load summary
st.header("📊 System Summary")

summary_col1, summary_col2 = st.columns(2)

with summary_col1:
    st.write("**Critical Bulb:**", "🟢 ON" if critical_bulb else "🔴 OFF")
    st.write("**AC Coolant Fan:**", "🟢 ON" if coolant_fan else "🔴 OFF")

with summary_col2:
    st.write(
        "**Non-Critical Bulb 1:**",
        "🟢 ON" if noncritical_bulb1 else "🔴 OFF"
    )

    st.write(
        "**Non-Critical Bulb 2:**",
        "🟢 ON" if noncritical_bulb2 else "🔴 OFF"
    )

st.divider()

st.info(
    "This is currently a safe software simulation. "
    "No 230 V electrical loads are connected."
)
