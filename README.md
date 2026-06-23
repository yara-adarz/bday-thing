# bday-thing
a bday card for my friend idk manz

import streamlit as st

PASSWORD = "24/06/2010"

st.set_page_config(page_title="HAPPY 16th BIRTHDAY!!!", page_icon="🎂<3", layout="wide")
st.markdown(
    """
    <style>
      .block-container {
        padding-left: 0rem;
        padding-right: 0rem;
        max-width: 90%;
      }
      .stApp {
        padding: 0rem;
      }
      .main {
        padding: 0rem;
      }
      .css-18e3th9, .css-1d391kg {
        padding: 0rem;
      }
      .css-6qob1r { padding-top: 0rem; }
    </style>
    """,
    unsafe_allow_html=True,
)
st.title("🎉 HAPPY BIRTHDAY!!")

st.markdown(
    "<div style='background:#FBC6E7; border: 3px solid #E73399; border-radius: 24px; padding: 20px; text-align:center; margin-bottom: 20px;'>"
    "<div style='font-size: 72px; font-weight: 900; color: #E73399;'>YOUR FINALLY 16!</div>"
    "<div style='font-size: 20px; color: #2C3E50; margin-top: 10px;'>Enter your birth date to unlock the birthday surprise</div>"
    "</div>",
    unsafe_allow_html=True,
)

if "authenticated" not in st.session_state:
    st.session_state.authenticated = False

password_input = st.text_input("Password", type="password")
if 'tries' not in st.session_state:
    st.session_state.tries = 0
    
if st.button("Unlock card"):
    if password_input == PASSWORD:
        st.session_state.authenticated = True
        st.success("Correct password! Enjoy your birthday card!")
    else:
        st.session_state.authenticated = False
        st.error("Wrong password, try again!")
        st.session_state.tries += 1
if not st.session_state.get("authenticated", False):
    if st.session_state.tries >= 1:
         st.markdown(
        "<div style='color: #E73399; background: #FBC6E7; padding: 14px; border-radius: 16px; border: 2px solid #E73399; font-weight: 600;'>Hint: try typing in (DD/MM/YYYY).</div>",
        unsafe_allow_html=True,
    )
    st.stop()


st.header("📸US?")

images = [
    "https://images.unsplash.com/photo-1529905236360-2a9b16a3b6c8?auto=format&fit=crop&w=800&q=80",
    "https://images.unsplash.com/photo-1512436991641-6745cdb1723f?auto=format&fit=crop&w=800&q=80",
    "https://images.unsplash.com/photo-1483985988355-763728e1935b?auto=format&fit=crop&w=800&q=80",
]

if "carousel_index" not in st.session_state:
    st.session_state.carousel_index = 0

st.image(
    images[st.session_state.carousel_index],
    caption=f"Slide {st.session_state.carousel_index + 1} of {len(images)}",
    use_column_width=True,
)

cols = st.columns([1, 1, 1])
with cols[0]:
    if st.button("◀️ Previous"):
        st.session_state.carousel_index = max(0, st.session_state.carousel_index - 1)
with cols[2]:
    if st.button("Next ▶️"):
        st.session_state.carousel_index = min(len(images) - 1, st.session_state.carousel_index + 1)

st.markdown("---")

col1, col2, col3 = st.columns([1, 1, 1])
with col2:
    if st.button("What's next? 🤔", key="whats_next", use_container_width=True):
        st.session_state.show_cake_section = True
        st.rerun()

if not st.session_state.get("show_cake_section", False):
    st.stop()

if "cake_blown" not in st.session_state:
    st.session_state.cake_blown = False

st.markdown(
    """
    <style>
    @keyframes blow_animation {
        0% { transform: rotate(0deg) scale(1); }
        20% { transform: rotate(-10deg) scale(1); }
        50% { transform: rotate(10deg) scale(1); }
        80% { transform: rotate(-10deg) scale(1); }
        90% { transform: rotate(-5deg) scale(1); }
        100% { transform: rotate(0deg) scale(1.5); }
    }
    </style>
    """,
    unsafe_allow_html=True,
)

cake_size = 30
shake_style = "animation: blow_animation 0.8s ease-in-out forwards; transform-origin: center;" if st.session_state.cake_blown else ""
text_margin = 80 if st.session_state.cake_blown else 5

st.markdown(
    f"<div style='text-align: center; padding: 40px 0;'>"
    f"<div style='font-size: {cake_size}vw; line-height: 1; margin: 0; {shake_style}'>🎂</div>"
    f"<div style='font-size: 32px; color: #E73399; font-weight: 900; margin-top: {text_margin}px;'>Make a wish and blow out the candles!</div>"
    f"</div>",
    unsafe_allow_html=True,
)

st.markdown("<div style='margin-top: -10px;'></div>", unsafe_allow_html=True)

col1, col2, col3 = st.columns([1, 1, 1])
with col2:
    if st.button("🌬️ BLOW THE CANDLES!", key="blow_button_full", use_container_width=True):
        st.session_state.cake_blown = True
        st.rerun()

if st.session_state.cake_blown:
    st.markdown("<br><br>", unsafe_allow_html=True)
    
    card_markdown = """
<div style='border: 3px dashed #E73399; padding: 24px; border-radius: 20px; background: #FBC6E7; margin-top: 40px;'>
  <h2 style='color: #E73399; text-align: center; font-size: 28px;'>Happy 16th Birthday!</h2>
  <p style='font-size: 18px; text-align: center;'>To my most favourite person in the whole wide world:</p>
  <p style='font-size: 18px; text-align: center; margin-top: 16px;'>Happy Birthday, I love you sooo muchh and I hope you have the best birthday everrr <3</p>
  <p style='text-align: center; font-size: 32px;'>❤️😘🎂</p>
</div>
"""

    st.markdown(card_markdown, unsafe_allow_html=True)

