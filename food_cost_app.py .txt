import streamlit as st

st.set_page_config(page_title="Food Cost Domestico", page_icon="🍽️")

st.title("🍽️ Calcolatore Food Cost Domestico")

nome_ricetta = st.text_input("Nome della ricetta", "Insalata di farro")
porzioni = st.number_input("Numero di porzioni", min_value=1, value=2)

st.subheader("Ingredienti (max 5)")

ingredienti = []

for i in range(1, 6):
    nome = st.text_input(f"Ingrediente {i} - Nome", key=f"nome_{i}")
    quantita = st.number_input(f"Ingrediente {i} - Quantità", min_value=0.0, step=1.0, key=f"quantita_{i}")
    costo_unitario = st.number_input(f"Ingrediente {i} - Costo unitario (€)", min_value=0.0, step=0.01, key=f"costo_{i}")
    
    if nome and quantita > 0 and costo_unitario > 0:
        ingredienti.append({
            "nome": nome,
            "quantita": quantita,
            "costo_unitario": costo_unitario
        })

if st.button("Calcola Food Cost"):
    if not ingredienti:
        st.warning("Inserisci almeno un ingrediente.")
    else:
        costo_totale = sum(i["quantita"] * i["costo_unitario"] for i in ingredienti)
        costo_porzione = costo_totale / porzioni
        st.success(f"💰 Costo totale: {round(costo_totale, 2)} €")
        st.info(f"💸 Costo per porzione: {round(costo_porzione, 2)} €")
