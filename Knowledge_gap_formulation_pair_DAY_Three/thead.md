## Key Points

1. When your DPO/SimPO data is full of style-guide violations + templated winners, how do you know the model learned real reasoning instead of just surface compliance?
   - A common trap I helped close for a partner building a sales email judge.

2. The mechanism is shortcut learning.
   - Models optimize the easiest signal in preference pairs.
   - Deterministic style fixes + templated “good” outputs = strong style signal, weak reasoning signal.

3. Real experiment (tiny Qwen LoRA on Colab):
   - Surface-heavy data → +18% style rubric, only +3% on decisive-action probes.
   - Reasoning-augmented data flipped the pattern.

4. Key paper:
   - “Style Outweighs Substance” (Feuer et al., ICLR 2025)
   - SOS-Bench shows LLM judges (and models trained on them) heavily favor style over substance.

5. Fix:
   - Add reasoning-only probes.
   - Diversify chosen outputs.
   - Measure style vs reasoning deltas separately.
   - Style compliance is cheap. Good judgment is expensive.
