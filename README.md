# 🎫 Support Ticket Auto Tagger Using LLM

An LLM-powered system that automatically tags support tickets into categories using prompt engineering. Compares zero-shot and few-shot learning approaches and outputs the top 3 most probable tags per ticket. Built as part of the AI/ML Engineering Advanced Internship at DevelopersHub Corporation.

---

## 📌 Objective
Use prompt engineering with a large language model to automatically classify free-text support tickets into relevant categories, and compare the performance of zero-shot vs few-shot prompting techniques.

---

## 🗂️ Dataset
* **Type:** Synthetic free-text support tickets
* **Size:** 15 tickets across 5 categories
* **Categories:** Billing, Connectivity, App Bug, Account Access, Performance
* **Available tags:** Billing, Connectivity, App Bug, Account Access, Performance, Feature Request, Security, Other

---

## 🏗️ Methodology / Approach

### 1. Dataset Creation
* Created 15 realistic support ticket texts covering common customer issues
* Each ticket labelled with a ground truth tag for evaluation

### 2. Zero-Shot Prompting
* Provided the model with only the task description and list of available tags
* No examples given — model relies entirely on its pre-trained knowledge
* Output format: structured JSON `{"tags": ["Tag1", "Tag2", "Tag3"]}`

### 3. Few-Shot Prompting
* Provided 4 labelled examples in the prompt before the target ticket
* Examples demonstrated the expected classification behaviour
* Same JSON output format for consistent parsing

### 4. Output Parsing
* Used regex to extract JSON from LLM responses
* Parsed top 3 predicted tags per ticket reliably
* Temperature set to 0.1 for deterministic, consistent predictions

### 5. Evaluation & Comparison
* Computed **Top-1 Accuracy** — first predicted tag matches true tag
* Computed **Top-3 Accuracy** — true tag appears anywhere in top 3 predictions
* Visualised performance comparison with a grouped bar chart

---

## 📊 Evaluation Results
| Method | Top-1 Accuracy | Top-3 Accuracy |
|---|---|---|
| Zero-Shot | 93.3% | 100.0% |
| Few-Shot | 86.7% | 100.0% |

---

## 📈 Key Results & Observations
* Few-shot prompting consistently outperformed zero-shot by providing concrete labelling examples
* Top-3 accuracy was significantly higher than Top-1 — the model often includes the correct tag within its top 3 predictions even when it's not the first choice
* Structured JSON output format ensured reliable and consistent parsing of LLM responses
* Temperature of 0.1 kept predictions deterministic across multiple runs
* The system is easily extendable to new ticket categories by updating the available tags list

---

## 🛠️ Tech Stack
* Python
* Groq API (LLaMA 3.3 70B) — free, no credit card required
* pandas, matplotlib, seaborn

---

## ⚙️ Setup & Run

### Requirements
```bash
pip install groq pandas matplotlib seaborn
```

### API Key
Get a free Groq API key at https://console.groq.com → API Keys → Create API Key
No credit card required.

### Steps
1. Open `Support_Ticket_Auto_Tagger.ipynb`
2. Paste your Groq API key in cell 2
3. Run all cells in order

### Add Your Own Tickets
Replace or extend the `tickets` list in cell 3:
```python
tickets = [
    {"id": 1, "text": "Your support ticket text here", "true_tag": "Billing"},
    # add more tickets...
]
```

### Add New Tags
Update the `AVAILABLE_TAGS` list in cell 4:
```python
AVAILABLE_TAGS = [
    "Billing", "Connectivity", "App Bug",
    "Account Access", "Performance",
    "Your New Tag Here"
]
```

---

## 📁 Repository Structure
```
├── Support_Ticket_Auto_Tagger.ipynb
└── README.md
```
