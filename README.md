# Peeking Inside BERT's Attention

A tool that asks BERT to fill in the blank and then draws what each of its attention heads is "looking at".

Type a sentence with a `[MASK]` in it, and the program:
1. predicts the top 3 words that could fill the gap, using the pre-trained `bert-base-uncased` model
2. saves a heatmap for **every attention head in every layer** (12 × 12 = 144 images), where lighter squares mean stronger attention between two tokens

```
Text: How do Python [MASK] eat spaghetti code?
how do python developers eat spaghetti code?
...
```

## What I found

Looking through the heatmaps, some heads clearly specialize. My notes are in [`analysis.md`](analysis.md). A few highlights:

- **Layer 6, Head 12** links the helper verb "do" to the main verb of a question ("eat", "learn"). It seems to track grammatical structure.
- **Layer 4, Head 6** shows a clean diagonal: each token attends mostly to the token right before it. That head seems to track word order.

## Run it

```bash
pip install -r requirements.txt
python mask.py
```

> The script expects an `OpenSans-Regular.ttf` font in `assets/fonts/`. Add it there, or point `FONT` in `mask.py` to any `.ttf` file on your machine.

## Built with

Python · TensorFlow · Hugging Face Transformers · Pillow
