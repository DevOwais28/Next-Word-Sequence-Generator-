## The Sentient Punchline: Deep Sequence Generation 🤖🃏
"The Sentient Punchline" is a Natural Language Processing (NLP) project built with Deep Learning to predict and generate coherent text sequences. The model evolved from generating random "word salad" to producing grammatically structured, contextually relevant observations.

## 🚀 Tech Stack & Architecture## Core Stack

* Language: Python 3.12
* Frameworks: TensorFlow & Keras
* Libraries: Pandas, NumPy, Matplotlib, Regex

## Model Architecture: Stacked LSTM

* Embedding Layer: 128-dim vectors with mask_zero=True.
* Stacked LSTMs: Dual layers (256 → 128 units) to capture deep semantic "sense."
* Regularization: Multi-stage Dropout (0.3) and Recurrent Dropout (0.01).
* Optimization: Sparse Categorical Crossentropy for memory-efficient training on a 10,001-word vocabulary.

## 🛠 Engineering Challenges & Solutions## 1. The "Fake Accuracy" Trap

* Issue: Model hit 99.5% accuracy instantly by only predicting padding zeros.
* Solution: Switched to Pre-padding and filtered out zero-targets ($y \neq 0$), forcing the model to learn actual vocabulary logic.

## 2. RAM Management

* Issue: 60,000+ vocabulary words caused memory crashes during one-hot encoding.
* Solution: Implemented Sparse Categorical Crossentropy, allowing the model to process labels as integers.

## 3. GPU (cuDNN) Assertion Errors

* Issue: Fast GPU kernels (cuDNN) crashed when using masks with specific padding styles.
* Solution: Fine-tuned recurrent activations to force a flexible training mode compatible with mask_zero.

## 4. Achieving "Sense" (N-Grams)

* Issue: Model produced "Word Salad" (random words without flow).
* Solution: Rebuilt dataset using N-Grams (growing sentences word-by-word) so the model practiced building every part of a sentence structure.

## 📊 Results

* Final Accuracy: 26% (Real-world accuracy, post-zero filtering) (for only 20 epochs)
* Output Example: "Success is a lot I can't even see my wife in."

## 📝 How to Run

   1. Clean data using the Regex script.
   2. Tokenize with a 10,000 word limit.
   3. Generate N-gram sequences and apply the Zero-Filter.
   4. Use the generate_text function with Top-K Sampling for best results.


