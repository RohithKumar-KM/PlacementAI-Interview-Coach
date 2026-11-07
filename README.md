# 🎯 PlacementAI – AI-Powered Interview Coach

**Practice technical interviews, evaluate your answers, understand your improvement areas, and become placement-ready with AI.**

PlacementAI is an AI-powered interview practice application built with **Python, Streamlit, LangChain, LangGraph, and OpenRouter**. It generates role-specific technical interview questions based on the candidate's experience level, evaluates submitted answers, and provides personalized feedback and an evaluation report.

---

## ✨ Features

### 🎯 Personalized Interview Questions
- Select from roles such as Python Developer, Data Scientist, Machine Learning Engineer, Full Stack Developer, AI Engineer, Software Developer, Data Analyst, and Cloud Engineer.
- Choose an experience level:
  - Fresher
  - 0–1 Years
  - 1–3 Years
  - 3–5 Years
  - 5+ Years
- Generate questions with difficulty and complexity adapted to the selected experience level.
- Enter a custom interview question when you prefer manual practice.

### 📝 Answer Submission and Evaluation
- Write your answer directly in the application.
- Evaluate answers using an AI-powered LangGraph workflow.
- Analyze technical correctness, relevance, clarity, and completeness.
- Receive an interview score out of 10.

### 💡 Personalized Improvement Feedback
- Understand what you answered well.
- Identify areas that need improvement.
- Receive three specific improvement suggestions.
- Review a sample improved answer when additional feedback is required.

### 📊 Evaluation Dashboard
- View your latest interview score and performance status.
- Review answer analysis and improvement feedback.
- Read and download the final evaluation report.
- Track the number of completed evaluations during the current application session.

### 🌙 Dark User Interface
- Dark navy interface with readable text and contrast.
- Role and experience selection controls.
- Separate sections for interview practice, evaluation, and project information.

---

## 🧰 Technology Stack

| Technology | Purpose |
|---|---|
| Python | Core application logic |
| Streamlit | Interactive web interface |
| LangChain | Language-model integration |
| LangGraph | Multi-step interview evaluation workflow |
| OpenRouter | Access to the configured GPT-OSS model |
| LangSmith | Workflow monitoring and tracing |
| python-dotenv | Loading environment variables |

---

## 🏗️ Workflow Architecture

PlacementAI uses LangGraph to coordinate the answer-evaluation process.

```text
                         START
                           |
                           v
                    Analyze Answer
                           |
                           v
                    Evaluate Answer
                           |
                           v
                   Conditional Routing
                      /         \
               Score < 7       Score >= 7
                   |               |
                   v               |
            Generate Feedback      |
                   |               |
                   +-------+-------+
                           |
                           v
                  Generate Final Report
                           |
                           v
                          END
```

### Question generation

The question-generation function receives the selected job role and experience level. It uses experience-specific prompt guidance to generate a suitable technical interview question.

### Answer evaluation

The LangGraph workflow contains four nodes:

1. **Analyze Answer** – reviews technical correctness, relevance, clarity, and completeness.
2. **Evaluate Answer** – assigns a score from 0 to 10 using the evaluation rubric.
3. **Generate Feedback** – when the score is below 7, provides strengths, improvement areas, suggestions, and a sample improved answer.
4. **Generate Final Report** – prepares a report containing the question, answer, score, analysis, feedback, and recommendation.

---

## 📁 Project Structure

```text
PlacementAI/
│
├── app.py                 # Streamlit interface and application flow
├── nodes.py               # Question generation and evaluation nodes
├── graph.py               # LangGraph workflow and conditional routing
├── state.py               # TypedDict definition for workflow state
│
├── requirements.txt       # Python dependencies
├── .env                   # OpenRouter and optional model configuration
├── .gitignore              # Files excluded from Git
└── README.md               # Project documentation
```

---

## ⚙️ Installation and Setup

### 1. Clone the repository

```bash
git clone https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
```

### 2. Open the project directory

```bash
cd YOUR-REPOSITORY
```

### 3. Create a virtual environment (recommended)

**Windows:**

```bash
py -3.11 -m venv venv
venv\Scripts\activate
```

**macOS / Linux:**

```bash
python3.11 -m venv venv
source venv/bin/activate
```

If you prefer not to use a virtual environment and Python 3.11 is installed, you can use `py -3.11 -m pip` to install packages and `py -3.11 -m streamlit` to run the application on Windows.

### 4. Install dependencies

```bash
python -m pip install -r requirements.txt
```

### 5. Configure environment variables

Create a `.env` file in the project root:

```env
OPENROUTER_API_KEY=your_openrouter_api_key
```

The current `nodes.py` configures the model as `openai/gpt-oss-20b` in the `ChatOpenRouter` initialization. Keep your API key private and never commit the `.env` file.

### 6. Run the application

```bash
python -m streamlit run app.py
```

On Windows, to explicitly use Python 3.11:

```bash
py -3.11 -m streamlit run app.py
```

Streamlit will display a local URL in the terminal. Open that URL in your browser.

---

## 🚀 How to Use PlacementAI

1. Start the application.
2. Open **Interview Practice**.
3. Select your target job role.
4. Select your experience level.
5. Choose **Generate with AI** to create a role- and experience-based question, or choose **Enter manually** to provide your own question.
6. Enter your answer in the answer box.
7. Click **Evaluate My Answer**.
8. Review your score, answer analysis, improvement feedback, and final report.
9. Download the evaluation report if required.

**New-question behaviour:** When a new AI-generated question is created, the previous answer and evaluation result are cleared so that an old answer is not accidentally submitted for a new question.

---

## 📏 Evaluation Rubric

The answer evaluation prompt uses the following 10-point rubric:

| Evaluation criterion | Marks |
|---|---:|
| Technical correctness | 4 |
| Relevance | 2 |
| Clarity | 2 |
| Completeness | 2 |
| **Total** | **10** |

When the score is below **7**, the workflow generates additional improvement feedback before preparing the final report. Scores of 7 or above proceed directly to report generation.

---

## 🔐 Security Notes

- Store your OpenRouter API key in `.env`.
- Do not hardcode API keys in source files.
- Do not commit `.env`, virtual environments, or Python cache files.
- If an API key is accidentally exposed, revoke it and generate a replacement.

Example `.gitignore` entries:

```gitignore
.env
venv/
.venv/
__pycache__/
*.py[cod]
.streamlit/secrets.toml
```

---

## 🔮 Possible Future Enhancements

- Resume-based personalized interview questions.
- Multiple-question mock interview sessions.
- Persistent evaluation history across application restarts.
- Interview performance trends and analytics.
- Voice-based interview practice.
- Coding questions with code execution and automated test evaluation.
- Export reports as PDF.

---

## 🎯 Project Objective

The goal of PlacementAI is to make technical interview preparation more personalized and practical. By combining experience-aware question generation with structured answer evaluation and targeted feedback, the application helps candidates identify knowledge gaps and improve how they communicate technical concepts.

---

## 👨‍💻 Author

**Rohith Kumar K M**

- LinkedIn: [Your LinkedIn Profile](https://www.linkedin.com/in/rohith-kumar-k-m/)

---

⭐ If you find this project useful, consider giving the repository a star.

**Built with Python, LangChain, LangGraph, and Generative AI.**
