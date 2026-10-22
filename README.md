# 🧠 Next Word Prediction using LSTM

A simple deep learning web app that reads a sentence you type and predicts the **next word**. The model is a Long Short-Term Memory (LSTM) network trained on text, and the interface is built with Streamlit.

---

## 📌 Table of Contents

- [How It Works](#-how-it-works)
- [Project Structure](#-project-structure)
- [Requirements](#-requirements)
- [Installation](#-installation)
- [Usage](#-usage)
- [Model Details](#-model-details)
- [Limitations](#-limitations)
- [Future Improvements](#-future-improvements)
- [License](#-license)

---

## 💡 How It Works

Think of the model as a very good autocomplete. It has learned from lots of text which words usually come after which others.

The pipeline has four steps:

1. **Tokenization:** The sentence is split into words, and each word is turned into a number using a saved vocabulary (`tokenizer.pkl`). For example, `"the cat"` might become `[4, 27]`.
2. **Padding:** The model expects every input to be the same length (`max_len - 1`). Shorter sentences are padded with zeros at the front (`padding='pre'`), so the real words stay at the end, next to the position where the prediction is needed.
3. **LSTM prediction:** The LSTM reads the sequence of numbers one step at a time and remembers context from earlier words. At the end it outputs a probability for every word in the vocabulary.
4. **Picking the word:** The word with the highest probability is selected (`argmax`) and shown on screen.

### Why an LSTM?

A plain neural network treats each input independently. An LSTM has a "memory" that carries information forward through the sentence, so it can use earlier words to decide the next one. For example, after "I went to the", it can learn that a place word is more likely than a verb.

---

## 📁 Project Structure

```
next-word-prediction-lstm/
│
├── app.py             # Streamlit app: loads the model and runs the UI
├── lstm_model.h5      # Trained LSTM model (Keras format)
├── tokenizer.pkl      # Saved Keras Tokenizer (word → number vocabulary)
├── max_len.pkl        # Saved maximum sequence length used during training
├── requirements.txt   # Python dependencies
└── README.md          # Project documentation
```

---

## ⚙️ Requirements

- Python 3.9 or newer
- TensorFlow / Keras (the version should match the one used for training, because the saved model and tokenizer depend on it)
- Streamlit
- NumPy

---

## 🛠️ Installation

**1. Clone the repository**

```bash
git clone https://github.com/<your-username>/next-word-prediction-lstm.git
cd next-word-prediction-lstm
```

**2. (Recommended) Create a virtual environment**

```bash
python -m venv venv

# Windows
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

**3. Install dependencies**

```bash
pip install -r requirements.txt
```

---

## ▶️ Usage

Make sure `app.py`, `lstm_model.h5`, `tokenizer.pkl`, and `max_len.pkl` are all in the same folder, then run:

```bash
streamlit run app.py
```

Streamlit will open the app in your browser (usually at `http://localhost:8501`).

1. Type a sentence in the text box.
2. Click **Predict Next Word**.
3. The predicted next word appears below the button.

> ⚠️ Empty input shows a warning and no prediction is made.

---

## 🧩 Model Details

| Item                | Value                                          |
|---------------------|------------------------------------------------|
| Model type          | LSTM (Recurrent Neural Network)                |
| Framework           | TensorFlow / Keras                             |
| Input length        | `max_len - 1` (`max_len` = 745)                |
| Output              | Probability distribution over the vocabulary   |
| Tokenizer           | Keras `Tokenizer` (saved as `tokenizer.pkl`)   |
| Training dataset    | quote_dataset.csv                              |
| Vocabulary size     | 9000                                           |
| Embedding dimension | 50                                             |
| LSTM units          | 128                                            |
| Optimizer / Loss    | Adam / categorical cross-entropy]              |
| Epochs              | 150                                            |

---

## ⚠️ Limitations

- The model predicts only **one** word (the most likely one). It does not generate full sentences.
- Predictions depend on the training data. Words the tokenizer has never seen are ignored, so the output may be weak for unfamiliar vocabulary.
- The model has no understanding of meaning or facts. It only learns patterns in the text it was trained on.
- Predictions can be repetitive or generic for short inputs.

---

## 🚀 Future Improvements

- Show the **top-k** predicted words with their probabilities, instead of only one.
- Generate multiple words in a loop to build full sentences.
- Replace the word lookup loop with a dictionary of `index → word` for faster inference.
- Add a Bidirectional LSTM or Transformer-based model for better accuracy.
- Add temperature sampling to control how creative the predictions are.
- Deploy the app on Streamlit Community Cloud or Hugging Face Spaces.

---

## 🤝 Contributing

Contributions are welcome. Please open an issue first to discuss what you would like to change, then submit a pull request.

---

## 📄 License

This project is licensed under the [MIT License]

---

## 🙏 Acknowledgements

- [TensorFlow / Keras](https://www.tensorflow.org/)
- [Streamlit](https://streamlit.io/)


