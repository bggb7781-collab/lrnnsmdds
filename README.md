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
