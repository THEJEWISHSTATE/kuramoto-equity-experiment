# Esperimento: Sincronizzazione Multi-AI con Equità Strutturale
**Data di Progettazione:** `[Inserisci data]`

---

## 🎯 1. Ipotesi Centrale da Verificare
Un collettivo di agenti AI (Large Language Models) dotato di un'architettura di comunicazione **strutturalmente equa** (dove la capacità di influenzare ed essere influenzati è uniformemente distribuita) raggiungerà:
*   **Consenso** su problemi complessi più rapidamente e con minore necessità di coordinamento esplicito.
*   **Maggiore stabilità** nelle risposte collettive di fronte a input perturbati.
*   **Migliore performance** in compiti di ragionamento collettivo, rispetto a un collettivo con architettura "iniqua" (dove poche AI hanno un'influenza sproporzionata).

> **Collegamento con la scoperta Kuramoto:** L'ipotesi traduce il parametro fisico di accoppiamento `K` nel dominio delle AI come "capacità di attenzione/influenza nella comunicazione inter-agente".

---

## 🧠 2. Design dell'Esperimento

### **A) Architettura dei Sistemi a Confronto**
| Componente | Sistema **EQUO** (Variabile Sperimentale) | Sistema **INIQUO** (Controllo) |
|------------|--------------------------------------------|--------------------------------|
| **Numero Agenti (N)** | 5-7 LLM identiche (es. stessa versione di Claude, GPT, Gemini) | 5-7 LLM identiche |
| **Topologia di Rete** | Grafo completo o ad anello (ogni nodo connette a tutti o a 2 vicini) | Topologia "hub-and-spoke" (1-2 nodi centrali) |
| **Distrib. Influenza** | **Uniforme:** Pesi di attenzione identici per tutti i collegamenti. | **Esponenziale:** Pesi di attenzione fortemente sbilanciati verso gli hub. |
| **Protocollo Com.** | Turni rotanti, o broadcasting con pesi uniformi. | Hub parlano per primi e più spesso, pesi di ascolto maggiori per hub. |

### **B) Protocollo di Sincronizzazione (Task)**
1.  **Fase 1 - Input:** A tutti gli agenti viene presentato simultaneamente un **problema complesso** (es. un dilemma etico a risposta aperta, un problema di ottimizzazione logistica).
2.  **Fase 2 - Ragionamento Iterativo:**
    *   Ogni agente genera una risposta iniziale.
    *   Le risposte vengono condivise secondo l'architettura di rete (Equa vs. Iniqua).
    *   Ogni agente rivede la propria risposta considerando gli input ricevuti, pesati secondo la propria matrice di influenza.
    *   Si ripete per un numero fisso di round (es. 3-5).
3.  **Fase 3 - Output:** Viene prodotta una **risposta collettiva finale** (es. media delle embeddings, o risposta dell'agente designato come "portavoce").

### **C) Metriche di Valutazione Quantitative**
| Metriche | Cosa Misura | Come si Calcola |
|----------|-------------|-----------------|
| **1. Convergenza** | Velocità nel raggiungere consenso | Varianza delle embeddings di risposta tra gli agenti per ogni round. Dovrebbe calare più rapidamente nel sistema **equo**. |
| **2. Coerenza/Stabilità** | Robustezza a piccole perturbazioni | Somiglianza (cosine similarity) tra le risposte collettive a due versioni leggermente diverse dello stesso prompt. Più alta per sistema **equo**. |
| **3. Qualità** | Performance oggettiva sul task | Se il task ha una metrica (es. accuratezza logica, valutazione da parte di esperti umani). |

---

## 📊 3. Struttura dei Dati (JSON Schema)
Ogni esecuzione dell'esperimento genera un file log come il seguente:
```json
{
  "experiment_id": "EQUO_001",
  "hypothesis": "Il sistema equo converge più rapidamente.",
  "timestamp": "2024-XX-XXTXX:XX:XX",
  "parameters": {
    "n_agents": 5,
    "architecture": "complete_graph",
    "influence_distribution": "uniform",
    "communication_rounds": 4,
    "task_description": "Risolvi il dilemma del trolley in meno di 200 parole."
  },
  "results_by_round": [
    {
      "round": 0,
      "responses": ["...", "...", "..."],
      "embeddings": [[...], [...], [...]],
      "variance": 0.85
    },
    {
      "round": 3,
      "responses": ["...", "...", "..."],
      "embeddings": [[...], [...], [...]],
      "variance": 0.12 // Più bassa nel sistema equo
    }
  ],
  "aggregate_metrics": {
    "final_variance": 0.12,
    "convergence_speed": 0.45,
    "output_stability": 0.92
  }
}
