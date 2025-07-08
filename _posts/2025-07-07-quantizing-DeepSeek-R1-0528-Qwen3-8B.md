In May 2025, DeepSeek released an impressive update to their R1 model: the
[DeepSeek-R1-0528-Qwen3-8B](https://huggingface.co/deepseek-ai/DeepSeek-R1-0528-Qwen3-8B).
The full baseline currently ranks in the Top-10 on the
[LLM leaderboard](https://llm-stats.com).

I set out to run this on a low-cost
[OrangePi 5](http://www.orangepi.org/html/hardWare/computerAndMicrocontrollers/details/Orange-Pi-5.html) —
a single board computer with just **8GB** of RAM and an ARM SoC.

### Background

Earlier this year, I used the original DeepSeek-R1 model for a
[Stanford Continuing Studies](https://continuingstudies.stanford.edu)
class and documented the setup in this
[GitHub repo](https://github.com/guynich/deepseek_opi5plus).

### Challenge: Model Requires Quantization

The 8B parameter model with bfloat16 precision weighs in at ~16GB, far
beyond the 8GB RAM capacity of the OrangePi 5. Quantization is necessary to
make it run.

---

### 1. Baseline Colab Test (unquantized)

I first verified the bfloat16 8B model on
[Google Colab](https://huggingface.co/deepseek-ai/DeepSeek-R1-0528-Qwen3-8B/colab)
using a 40GB A100 GPU with a classic reasoning riddle. The model responded
correctly with **"heroine"** — ideal behavior.

> *Riddle:*
> I’m a word in the English language.
> My first two letters signify a male.
> My first three letters signify a female.
> My first four letters signify a great man.
> And my entire meaning signifies a great woman.
> What am I?

---

### 2. Ollama's Quantized Version

[Ollama](https://ollama.com/library/deepseek-r1)
provides a quantized version of DeepSeek R1-8B. While it ran on the OrangePi,
the model got stuck in a loop and failed to converge on “heroine”:

```
“I'm tired of these riddles... I’m overthinking…”
```

This prompted me to try my own quantized build.

---

### 3. My Quantized Version (via `llama.cpp` + Ollama)

I used `llama.cpp` to quantize the model to 4-bit (Q4_K_M), reducing the file
size to ~4.7GB.  I published it on
[HuggingFace](https://huggingface.co/guynich/DeepSeek-R1-0528-Qwen3-8B_Q4_K_M).

```bash
ollama run hf.co/guynich/DeepSeek-R1-0528-Qwen3-8B_Q4_K_M:Q4_K_M --verbose
```
This run consumed about 76% of the 8GB RAM. It showed better convergence than
the built-in Ollama model, repeatedly returning to the word "heroine", though it
still looped somewhat:
```
"So I think HEROINE is the word. Final Answer... Another thought..."
```
I manually stopped the run.

---

### 4. llama-run with My Quantized Model

To get better control over inference, I switched to using llama-run from
llama.cpp, built for ARM.  The command `--ngl` enables layer offload which
prioritizes the fast cores on the ARM SoC.

Here's the command I used:
```bash
./build/bin/llama-run \
  ./deepseek-r1-0528-qwen3-8b-q4_k_m.gguf \
  -c 10000 \
  --ngl 99 \
  --prompt "I’m a word in the English language. My first two letters signify a male. My first three letters signify a female. My first four letters signify a great man. And my entire meaning signifies a great woman. What am I?"
```
This run completed cleanly with less looping and produced the expected result:

```console
So the word is heroine.
</think>
The word that satisfies all the conditions is **heroine**.

- **First two letters: "HE"** – male pronoun
- **First three letters: "HER"** – female pronoun
- **First four letters: "HERO"** – great man
- **Entire word: "heroine"** – great woman

This word works because it leverages common pronouns and titles in an English language puzzle.
```
Success!

## Discussion

This single riddle prompt illustrates how the 8B model behavior can vary
significantly depending on:

* Quantization precision
* Inference framework
* Runtime configuration

| Framework (Precision) | Result  | Notes                            |
|-----------------------|---------|----------------------------------|
| Colab (bfloat16)      | Correct | Fast on A100 GPU and accurate    |
| Ollama (Q4_K_M)       | Loops   | Some convergence, but repetitive |
| llama-run (Q4_K_M)    | Correct | Clean result                     |

Framework and quantization compatibility matter — especially on
resource-constrained devices like the OrangePi 5.

## Next Steps

- [ ] Check model temperature and test other Ollama hyperparameters
- [ ] Try a broader test set of riddles and reasoning prompts

Want to try it yourself? Grab the quantized model on HuggingFace:
[DeepSeek-R1-0528-Qwen3-8B_Q4_K_M](https://huggingface.co/guynich/DeepSeek-R1-0528-Qwen3-8B_Q4_K_M)
