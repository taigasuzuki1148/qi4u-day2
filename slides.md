---
# Slidev frontmatter
theme: default
title: QI4U in Finland Day2
class: text-center font-sans
transition: slide-left
mdc: true
duration: 35min
colorSchema: dark
# 背景をグラデーション風に
background: linear-gradient(180deg, #0f1c47 0%, #1e2a78 100%)
---

# QI4U in Finland Day2
## The basics of Quantum Algorithms

<div
  @click="$slidev.nav.next"
  class="mt-12 mx-auto py-3 px-6 w-100 rounded-xl text-white font-bold cursor-pointer
         relative overflow-hidden text-center transition-all duration-300
         hover:scale-[1.02] active:scale-[0.99]
         bg-[#0b0f19]/70 backdrop-blur border border-white/10 shadow-lg"
>
  <!-- うっすらグラデ（Day2: 紫→青→シアン） -->
  <div class="absolute inset-0 bg-gradient-to-r from-purple-700/25 via-blue-500/20 to-cyan-400/25 -z-10"></div>

  <!-- ハイライトが流れる -->
  <div class="shine absolute -inset-y-2 -left-1/2 w-1/2 rotate-12 -z-10"></div>

  <!-- テキスト：1行固定で自動縮小 -->
  <span class="inline-flex items-center justify-center w-full whitespace-nowrap tracking-[0.07em]">
    <span class="text-sm leading-tight">
      How can a quantum computer search faster?
    </span>
    <carbon:arrow-right class="inline w-8 h-6 ml-1 opacity-90 flex-none" />
  </span>
</div>

<style>
/* 流れるハイライト */
.shine{
  background: linear-gradient(
    90deg,
    rgba(255,255,255,0) 0%,
    rgba(255,255,255,.10) 45%,
    rgba(255,255,255,.18) 50%,
    rgba(255,255,255,.10) 55%,
    rgba(255,255,255,0) 100%
  );
  animation: shine-move 3.5s ease-in-out infinite;
}
@keyframes shine-move{
  0%   { transform: translateX(0) rotate(12deg); opacity:0; }
  15%  { opacity:.9; }
  50%  { opacity:.35; }
  100% { transform: translateX(200%) rotate(12deg); opacity:0; }
}


/* “Oracle hit”っぽい控えめパルス */
.pulse{
  width: 14px; height: 14px; border-radius: 9999px;
  background: rgba(6,182,212,.35);
  box-shadow: 0 0 18px rgba(6,182,212,.35);
  animation: pulse 1.6s ease-in-out infinite;
}
@keyframes pulse{
  0%,100% { transform: translateY(-50%) scale(1); opacity:.55; }
  50%     { transform: translateY(-50%) scale(1.45); opacity:.95; }
}
</style>

---
transition: slide-left
---
# Part1 Lecture
17:00~17:30
<div class="flex justify-center mt-12">
<div class="flex w-full max-w-3xl bg-#222222 rounded-lg overflow-hidden shadow-lg transition-all duration-300 hover:bg-#333333 cursor-pointer">
  
  <!-- 左：説明エリア -->
  <div class="flex flex-col justify-between p-6 flex-1">
    <div>
      <h3 class="text-xl font-bold text-white mb-2">Grover's Algorithm</h3>
      <p class="text-sm text-gray-300">
        On the second day, we’ll give a lecture on algorithms where you can actually apply the qubit and quantum-circuit concepts you learned on the first day.
      </p>
      <p class="text-sm text-gray-400 mb-3">Lecturer: Taiga Suzuki</p>
    </div>
  </div>
  
  <!-- 右：写真 -->
  <div class="w-55 h-full">
    <img src="/images/IMG_1947.png" alt="Quantum" class="w-full h-full object-cover">
  </div>
</div>
</div>


---
transition: fade-out
---
# Reflection of Day1

<div style="position:relative;padding-bottom:50%;">
    <!-- 56.25 comes from aspect ratio of 16:9, change this accordingly -->
    <iframe
        style="width:100%;height:100%;position:absolute;left:0px;top:0px;"
        frameborder="0"
        width="100%"
        height="100%"
        allowfullscreen
        allow="autoplay"
        src="day1_refrection4.html">
    </iframe>
</div>


---
transition: fade-out
---
# Reflection of Day1
## Quantum Computation
- In **Encode**, we represent classical **0** and **1** using **qubits**.
  - *(Insert a Circle Notation visualization here.)*
- In **Compute**, we perform computation using a **quantum circuit** made of **quantum gates**, and finally we **measure**.
  - *(Insert a Manim animation here.)*
- In **Decode**, we interpret and combine the measured bitstrings (e.g., `00001`) into a meaningful answer.


---
transition: fade-out
---
# Quantum Algorithms
- A quantum algorithm is a procedure in which the computation is carried out using a quantum circuit.

There are many kinds of quantum algorithms, for example:
- A database search algorithm (Grover’s algorithm)
- An integer factorization algorithm (Shor’s algorithm)

Some quantum algorithms are theoretically faster than classical algorithms, achieving polynomial speedups (and in some cases even more) under appropriate assumptions.

In this workshop, we will focus mainly on Grover’s algorithm, and we will also discuss practical applications and ask you to think about how it could be used in real-world problems.

---
transition: fade-out
---

# Grover’s Algorithm

### What problem does it solve?
- An algorithm to **find a “good answer” quickly** from many candidates.
  - Example (graph coloring): among bitstrings like `00000000`, `00010110`, ... find one that satisfies the constraints.

<br>

### Classical search (baseline)
- We have a device that outputs whether a candidate satisfies the condition.
- In the worst case, to find 1 solution among `N` candidates, we may need `N` queries: **O(N)**.
<div style="height:10vh; width:100%;">
  <iframe src="day2_oracle_demo.html"
          style="display:block; width:100%; height:100%; border:0; border-radius:12px;"></iframe>
</div>
<br>

### Quantum search (Grover's Algorithm)
- With $O(\sqrt{N})$ queries to the oracle, we can obtain the correct answer with probability at least $1-1/N$

---
transition: fade-out
---
#  The process of Grover's Algorithm
When we want to find the state in which two bits are both 1, among 00, 01, 10, 11.
<div style="position:relative;padding-bottom:47%;">
    <!-- 56.25 comes from aspect ratio of 16:9, change this accordingly -->
    <iframe
        style="width:100%;height:100%;position:absolute;left:0px;top:0px;"
        frameborder="0"
        width="100%"
        height="100%"
        allowfullscreen
        allow="autoplay"
        src="TwoQubit_grover.html">
    </iframe>
</div>

---
transition: fade-out
---
# Oracle operator
How do me mark the state without knowing the answer

<div style="position:relative;padding-bottom:47%;">
    <!-- 56.25 comes from aspect ratio of 16:9, change this accordingly -->
    <iframe
        style="width:100%;height:100%;position:absolute;left:0px;top:0px;"
        frameborder="0"
        width="100%"
        height="100%"
        allowfullscreen
        allow="autoplay"
        src="oracle_slide.html">
    </iframe>
</div>

---
transition: fade-out
---
# Diffusion operator

The parts with a phase flip get amplified
<div style="position:relative;padding-bottom:47%;">
    <!-- 56.25 comes from aspect ratio of 16:9, change this accordingly -->
    <iframe
        style="width:100%;height:100%;position:absolute;left:0px;top:0px;"
        frameborder="0"
        width="100%"
        height="100%"
        allowfullscreen
        allow="autoplay"
        src="DiffusionCircleNotation_Mean.html">
    </iframe>
</div>

---
transition: fade-out
---
## Notes on Grover’s Algorithm

- By repeatedly applying the oracle and the diffusion operator, we can amplify the amplitude of the correct answer states.

- As a result, we need only $O(\sqrt{N})$ oracle (checker) queries to obtain the answer with probability at least $1 - 1/N$.

- Classically, the number of checker queries is $O(N)$.
  - For example, using a quantum algorithm can reduce about 10,000 queries to about 100.

### Now, let’s build Grover’s algorithm together!

---
transition: fade-out
---
# Part2 Hands-on
17:30~18:00
<div class="flex justify-center mt-12">
<div class="flex w-full max-w-3xl bg-#222222 rounded-lg overflow-hidden shadow-lg transition-all duration-300 hover:bg-#333333 cursor-pointer">
  
  <!-- 左：説明エリア -->
  <div class="flex flex-col justify-between p-6 flex-1">
    <div>
      <h3 class="text-xl font-bold text-white mb-2">Implementation of Simple Grover's Algorithm</h3>
      <p class="text-sm text-gray-300">
        To help you get familiar with Grover’s algorithm, we will explain a simple version of Grover’s algorithm here.
      </p>
      <p class="text-sm text-gray-400 mb-3">Lecturer: Kimata Sasuke</p>
    </div>
    <!-- 左下のボタン -->
    <div class="mt-4 flex gap-3">
  <a
    href="https://colab.research.google.com/drive/1BJ63AD2JZBPOE8-7FUm3tTwDoY7vvSjG?usp=sharing"
    target="_blank"
    rel="noopener noreferrer"
    class="inline-flex w-40 py-2 px-4 border border-white text-white
           bg-transparent hover:bg-white hover:text-black transition-colors duration-200
           items-center justify-center"
  >
    Grover's Algorithms
  </a>
  <a
    href="https://colab.research.google.com/drive/1Xuq6iqGgiFZm-cBUONJV4oY72KQcBv58?usp=sharing"
    target="_blank"
    rel="noopener noreferrer"
    class="inline-flex w-40 py-2 px-4 border border-white text-white
           bg-transparent hover:bg-white hover:text-black transition-colors duration-200
           items-center justify-center"
  >
    IQM real device
  </a>
</div>
  </div>
  
  <!-- 右：写真 -->
  <div class="w-55 h-full">
    <img src="/images/Kimata.JPG" alt="Quantum" class="w-full h-full object-cover">
  </div>
</div>
</div>


---
transition: fade-out
---
# Part3 Lecture
18:05~19:00(max)
<div class="flex justify-center mt-12">
<div class="flex w-full max-w-3xl bg-#222222 rounded-lg overflow-hidden shadow-lg transition-all duration-300 hover:bg-#333333 cursor-pointer">
  
  <!-- 左：説明エリア -->
  <div class="flex flex-col justify-between p-6 flex-1">
    <div>
      <h3 class="text-xl font-bold text-white mb-2">Social Implementation of Grover's Algorithm</h3>
      <p class="text-sm text-gray-300">
        Here, we’ll show how to construct the oracle when the problem is formulated as a graph problem, and we’ll introduce tools that help you build it, along with implementation examples!
      </p>
      <p class="text-sm text-gray-400 mb-3">Lecturer: Aditya Mukherjee, Rafet Uregen, Niklas Näsman, Upanyan Baskota and Taiga Suzuki</p>
    </div>
  </div>
  
  <!-- 右：写真 -->
  <div class="w-55 h-full">
    <img src="/images/IMG_1947.png" alt="Quantum" class="w-full h-full object-cover">
  </div>
</div>
</div>

---
transition: slide-left
---

# Workshop Focus : Graph Coloring
<div style="position:relative;padding-bottom:50%;">
    <!-- 56.25 comes from aspect ratio of 16:9, change this accordingly -->
    <iframe
        style="width:100%;height:100%;position:absolute;left:0px;top:0px;"
        frameborder="0"
        width="100%"
        height="100%"
        allowfullscreen
        allow="autoplay"
        src="graph-coloring-demo2.html">
    </iframe>
</div>

---
transition: slide-left
---

# Workshop flow

### 1. Identify the real world issue

- This is what you all will do!

<br>

### 2. Map the problem into graph-coloring problem
- This is what you all will do!

<br>

### 3. Express the graph as oracle
- You can use the special tool for this!

<br>

### 4. Experiment on simulater or the real hardware device
- You can use the special tool for this!

<br>

---
transition: slide-left
---

# How did we create oracle for graph coloring

<div style="position:relative;padding-bottom:47%;">
    <!-- 56.25 comes from aspect ratio of 16:9, change this accordingly -->
    <iframe
        style="width:100%;height:100%;position:absolute;left:0px;top:0px;"
        frameborder="0"
        width="100%"
        height="100%"
        allowfullscreen
        allow="autoplay"
        src="oracle_slide.html">
    </iframe>
</div>


---

# Oracle Creation tool

<div style="position:relative;padding-bottom:50%;">
    <!-- 56.25 comes from aspect ratio of 16:9, change this accordingly -->
    <iframe
        style="width:100%;height:100%;position:absolute;left:0px;top:0px;"
        frameborder="0"
        width="100%"
        height="100%"
        allowfullscreen
        allow="autoplay"
        src="graph-builder2.html">
    </iframe>
</div>
---

# Simulators and Real device lab

### 1. Simulators
Please take a try on simulators firstly via url below:

<div>
<a
  href="https://colab.research.google.com/drive/1KUEcG-ZruzZ0fZ8RvVLlCFV6sqcTZrZ9?usp=sharing"
  target="_blank"
  rel="noopener noreferrer"
  class="mt-3 inline-flex items-center justify-center w-44 py-2 px-4
         border border-white text-white bg-transparent
         hover:bg-white hover:text-black transition-colors duration-200 rounded"
>
  Open Colab
</a>
</div>
<br>


### 1. Real Devices
IQM real devices are available, しかしながら，

<div>
<a
  href="https://colab.research.google.com/drive/1sDnTwamY908I10nOLZGrxRsZ3YgGbyCt?usp=sharing"
  target="_blank"
  rel="noopener noreferrer"
  class="mt-3 inline-flex items-center justify-center w-44 py-2 px-4
         border border-white text-white bg-transparent
         hover:bg-white hover:text-black transition-colors duration-200 rounded"
>
  Open Colab
</a>
</div>


---

# The use-cases by students from Aalto university

### 1. Aditya Mukherjee
<br>

### 2. Rafet Uregen
<br>

### 3. Niklas Nasman
<br>

### 4. Upanyan Baskota


---

# Group work

## Please fill out the form provided in the group chat at discord!!
<br>

## The problem you can deal with might be small but it will be  theoretically much faster than classical part!!
-> your ideas may change and save the world!