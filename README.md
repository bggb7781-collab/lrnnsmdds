# lrnn-SMDDS

Linear RNN with **exact recall** over unbounded context at O(1) generation cost.

| Feature | Mamba | RWKV | lrnn-SMDDS |
|---------|-------|------|------------|
| Context | Approx | Approx| **Exact (slot reservoir)** |
| Gen.    | O(1)   | O(1) | **O(1)** |
| Recall  | Decays | Decays | **Perfect** |
| Dependencies | Many | Many | **Zero** |

## 30-second quickstart
gcc -std=c17 -O3 -march=native --fast-math -o lrnn aismdd.c -lm
./lrnn --train corpus.txt --save model.bin

./lrnn --load model.bin --seed "AI" --tokens 500

Below are screenshots from my chats with Gemini 3.1 pro and Sonnet 4.6 in addition to other screenshots that should get you started with the project:

1. What is lrnnsmdds? (Gemini 3.1 pro):
<img src="https://i.imgur.com/tHfOZHX.png"></img>
<img src="https://i.imgur.com/dwDcz7H.png"></img>
