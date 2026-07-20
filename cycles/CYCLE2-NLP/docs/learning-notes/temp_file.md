### Summarization

Condensing a longer text into a shorter version while still retaining the value of the text.

Models that are designed for such tasks are BART and T5. These are for sequence-to -sequence patterns

**BART**:
- Similar ot BERT
    - Token and positional embedding of text
- BART is pretrained by corruptting the input and then reconstructing it with decoder. any type of corruption
    - Text infilling corruption is the best though
    - Many tokens are replaced with one mask token and the model needs to predict the masked tokens and teaches the model to predict the number of masked tokens
    - Input embeddings and masked spans are passed through the endocer to output final hidden states

- Encoder's output is passed through the decoder
    - Decoder needs to predict the number of masked and uncorrupted tokens from encoder's output
    - Gives additional context to help decoder restore the original text
    - Output is passed through language modeling head
        - Linear transformation to convert the hidden states into logits
        - Cross entropy losss in calcultaed between the logits and the label, token shifted to the right