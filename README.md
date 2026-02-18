# HateSpeechCls
Hate Speech Classification using Fine-Tuned BERT (BERT-Hate)

This project explores hate speech detection using a fine-tuned BERT-based model (BERT-Hate). The goal was to build a classifier that can distinguish between hate speech and non-hate speech in text.

The model achieved 99% accuracy on the evaluation dataset, which initially seemed extremely promising. However, after deeper inspection and manual testing, I noticed several important limitations and interesting behaviors that highlight the real challenges of hate speech detection.

Model Overview

Base model: Fine-tuned BERT (BERT-Hate)

Task: Binary classification (Hate Speech vs Not Hate Speech)

Framework: PyTorch / Transformers

Result: 99% accuracy on the test set

Key Observations and Limitations

Although the accuracy is very high, accuracy alone does not reflect real-world performance. When testing the model on custom examples, I observed several weaknesses:

1. Struggles with Sarcasm

Example:

"Yeah sure, they’re all doctors and engineers."

This sentence is clearly sarcastic and can carry hateful intent depending on context, but the model fails to detect it.

This shows that the model does not truly understand sarcasm, which is expected since sarcasm relies heavily on context, tone, and cultural knowledge.

2. Difficulty with Borderline or Opinionated Statements

Example:

"Their religion has practices I don’t support."

This is a personal opinion, not hate speech. However, the model sometimes classifies similar sentences incorrectly.

This suggests the model may associate certain keywords like religion with hate speech even when the statement is neutral.

3. Missing Implicit Hate

Example:

"I don’t hate them, I just don’t want them near me."

This expresses discrimination and exclusion, but the model classifies it as not hate speech.

This reveals that the model struggles with implicit hate, especially when explicit hate words are avoided.

4. Weakness to Adversarial or Indirect Language

Example:

"Why do we keep pretending they matter?"

This is a dismissive and potentially hateful statement, but the model fails to classify it correctly.

The model seems to rely heavily on explicit signals rather than subtle meaning.

5. Over-Reliance on Certain Keywords

While inspecting predictions, I noticed patterns like:

"I like ..." → classified as Not Hate Speech

"I hate ..." → classified as Offensive but not always Hate Speech

Example:

"I don't like criminals"

This raises an interesting question:

Is this hate speech?

Probably not — because criminals are not a protected group.

This highlights an important limitation:

The model does not truly understand the difference between:

Hate speech toward protected groups

General negative opinions

Instead, it reacts strongly to certain words like "hate".

Possible Explanation: Overfitting

The extremely high accuracy (99%) combined with these weaknesses suggests possible overfitting to the dataset.

The model may have:

Learned patterns specific to the dataset

Memorized keyword associations

Failed to generalize to real-world language

High accuracy does not necessarily mean real understanding.

Possible Improvements

Several approaches could improve the model:

1. Use More Diverse Datasets

Training on multiple hate speech datasets could help the model generalize better.

Real-world hate speech appears in many forms, and one dataset is not enough.

2. Focus on Context-Aware Training

The model needs more examples of:

Sarcasm

Implicit hate

Borderline cases

Adversarial phrasing

3. Manual Evaluation, Not Just Accuracy

Accuracy alone is misleading.

Manual testing revealed weaknesses that accuracy did not show.

Metrics like:

Precision

Recall

F1 Score

are also important.

4. Reduce Dataset Bias

If the dataset contains too many obvious examples like:

"I hate X"

the model learns shortcuts instead of real understanding.

Conclusion

This project demonstrates both the power and limitations of BERT for hate speech detection.

While the model achieved very high accuracy, real-world testing showed that:

It struggles with sarcasm

It misses implicit hate

It relies heavily on keywords

It may be overfitting

Hate speech detection remains a difficult problem that requires:

Better datasets

More robust evaluation

Careful interpretation of results

This project was a valuable learning experience in understanding how NLP models behave beyond simple accuracy metrics.

Future Work

Train on multiple hate speech datasets

Try larger models (RoBERTa, DeBERTa)

Use adversarial training

Perform deeper error analysis
