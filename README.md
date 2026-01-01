# Encoder — Hindi & English Character-Level Tokenizer

A lightweight, language-agnostic tokenizer that converts text into integer token IDs and back.
Supports **Hindi**, **English** at the **character level**.


## ✨ Features

* Handles **Hindi (U+0900–U+097F)**, **English (U+0020–U+007E)**, and **Emoji (U+1F600–U+1F64F)**
* Adds special tokens: `<PAD>`, `<UNK>`, `<SOS>`, `<EOS>`
* Simple character-level tokenization — no external libraries
* Bi-directional: **encode()** and **decode()**
* Unicode-safe (supports mixing Hindi, English, Emojis)


## 🗂️ Project Structure

```
.
├── char2id.json      # Mapping from character → token ID
├── id2char.json      # Mapping from token ID → character
├── encoder.py        # Contains the Encoder class
└── README.md
```


## ⚙️ Requirements

* Python 3.8+
* No external dependencies (uses only the `json` and `unicodedata` modules)


## 🧩 How It Works

### 1. Build Vocabulary

You generate the vocabulary once:

* Hindi characters: `0x0900–0x097F`
* English characters: `0x0020–0x007E`
* Emojis: `0x1F600–0x1F64F`
* Add special tokens manually:

  ```python
  ["<PAD>", "<UNK>", "<SOS>", "<EOS>"]
  ```

Save them into:

* `char2id.json`
* `id2char.json`


### 2. Encoder Class Overview

```python
class Encoder:
    def __init__(self):
        # Loads char2id.json and id2char.json
        # Converts id2char keys back to integers
        # Caches special token IDs (<UNK>, <SOS>, <EOS>)
    
    def encode(self, text):
        # Adds <SOS> at start, <EOS> at end
        # Converts each character → ID
        # Uses <UNK> for unknown characters
        # Returns list of integers
    
    def decode(self, ids):
        # Converts IDs → characters
        # Skips <SOS> and <EOS>
        # Joins them into a string
```

## 💡 Example Usage

```python
from encoder import Encoder

obj = Encoder()

text = "हेलो क्या हाल है 😀"
encoded = obj.encode(text)
decoded = obj.decode(encoded)

print("Original:", text)
print("Encoded:", encoded)
print("Decoded:", decoded)
```

**Output:**

```
Original: हेलो क्या हाल है 😀
Encoded: [2, 245, 259, 251, 253, 247, 259, 243, 3]
Decoded: हेलो क्या हाल है 😀
```


## 🧾 License

MIT License — free to use, modify, and distribute.

## 👨‍💻 Author

Developed by **[Your Name]**
For multilingual text preprocessing and deep learning pipelines.
