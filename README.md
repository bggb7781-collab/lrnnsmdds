# lrnn-SMDDS

Linear RNN with **exact recall** over unbounded context at O(1) generation cost.

| Feature | Mamba | RWKV | lrnn-SMDDS |
|---------|-------|------|------------|
| Context | Approx | Approx| **Exact (slot reservoir)** |
| Gen.    | O(1)   | O(1) | **O(1)** |
| Recall  | Decays | Decays | **Perfect** |
| Dependencies | Many | Many | **Zero** |


<b>Contents:</b>
<i>
1. 30-second quickstart
2. More info
3. TODO/NAQ (never asked questions)
4. Quo vadis...the future</i>

## 30-second quickstart
gcc -std=c17 -O3 -march=native --fast-math -o lrnn aismdd.c -lm

./lrnn --train corpus.txt --save model.bin

./lrnn --load model.bin --seed "AI" --tokens 500

<img src="https://i.imgur.com/zm6v1u8.png"></img>

Training, small example:

<img src="https://i.imgur.com/I7lsRSh.png"></img>

Generation:

<img src="https://i.imgur.com/Terg7X8.png"></img>

<b>2. More info</b>

Below are screenshots from my chats with Gemini 3.1 pro and Sonnet 4.6 in addition to other screenshots that should get you started with the project:

a. What is lrnnsmdds? (Gemini 3.1 pro):
<img src="https://i.imgur.com/tHfOZHX.png"></img>
<img src="https://i.imgur.com/dwDcz7H.png"></img>

b. Features/advantages
<img src="https://i.imgur.com/bdlkr8B.png"></img>

 Memory improvement over RNNs (Mamba/RWKV):

<img src="https://i.imgur.com/Sk9kVm9.png"></img>

c. The math
<img src="https://i.imgur.com/eyNdpdV.png"></img>
<img src="https://i.imgur.com/qZtIPw1.png"></img>
<img src="https://i.imgur.com/uojftGO.png"></img>

<b>3. TODO/NAQ (never asked questions)</b>

Todo:

a. Non-gpu port: 
Since the goal was to have anti-GPU, CPU-friendly LLM as you can see there are zero attempts to port this to CUDA/GPU. However...it should be possible, thought not with 5-minute tweak even if you vibecode it. As you can see from the screenshot 3.6 million params model gets trained literally in seconds on my ancient Intel cpu, if you're armed with Ryzen you can actually have something that produces novel knowledge and be useful on couple of books or so, maybe it would take hours/days. 



b. No Python? 

Porting this to python should be very possible, in fact just go to claude/gpt and "vibeport it" (we'll pretend that's a word...). The C code has little-to-no dependencies and it's mostly loops/if-else statements without many nests, python or c# or Java should handle it easily. 


NAQ (never asked questions...):

a. what do i need to train something useful?

You likely need VERY good CPU (Ryzen/i7 etc.) and corpus of hundreds of KBs+ and hours/day time. For word tokenizer you'd need perplexity of 1.2 or less and validation loss under 1, for character tokenizer the perplexity may need to be as low as 1.05 (cruel but true... - yet unironically possible with this program).
Ideally try with --word tokenizer as with --character tokenizer you need very, very low perplexity reached to avoid gibberish words, but the flip side is that character tokenizer reaches lower perplexity much quicker than word-based one. Oh and btw: you can try to program BPE-tokenizer - serious feature currently lacking, for production!

b. "segmentation fault" wtf?

You should not see this (well) but if you do:
1. easiest/best way to fix: copy the error to Claude and the full source code.
2. second option: the classic way - decrease numbers, make sure files are present, hard disk isn't full, fire gdb;
3. just switch between cygwin and pure native Linux/Ubuntu/Debian to see if the erro persists;
4. And btw: reduce corpus size significantly, if you train over 2 mb of text, assuming the stack on Windows may crash. Then either put everything on the heap or just use lower size - for good test 1 mb is ok. If you pplan to compete with Sam Altman, then yeah: get ready for some real work and port the stack to heap (frankly i've never tried it with large corpus, some chance it may actually not-crash).

c. can it code, make images or videos?
In theory: yes. Have I tested it for anything other than fiction and non-fiction text? No. 
It's actually very promising for coding something classic RNNs struggle with greatly, for videos you're guaranteed to have quite the problem given the sequential non-parellilism, but it can be fixed...with some effort. 

<b>4. Quo Vadis: the future.</b>

This is assistant, it's not the "AGI".

Lrnnsmdds is trying to be alternative to transformers by having exceptionally long memory and fast generation, it would be a tool one can have very long and fast conversations with with the goal to reach truth one small-hill at a time. It's not "AGI", one question followed by one p=np solution answer. Claude, GPT and Gemini were amazing assistants and wrote some ~70% of the code of lrnnsmdds - it would be interesting to see now if lrnnsmdds can help you on its turn to create something of great value.
