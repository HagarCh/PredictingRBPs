# Predicting RNAcompete Binding from RNA Bind-n-Seq Data
**Introduction**  
RNA-binding proteins (RBPs) play key roles in essential cellular processes such as mRNA splicing, transport, stability, and translation. Understanding their binding preferences is crucial for deciphering the regulatory networks that operate at the molecular level.  

To study these preferences, we use data from two experimental technologies: **RNA Bind-n-Seq (RBNS)** and **RNAcompete**. For each RBP, we train a deep learning model on RBNS data and apply it to score RNAcompete probes. Our goal is to assign binding intensities to RNAcompete sequences. We achieve this by aggregating the model’s predicted probabilities into a single binding score per probe.

**Model architecture:**  
We developed a convolutional neural network (CNN) to predict binding preferences using RNA Bind-n-Seq data.  
The model includes:  
- A 1D convolutional layer with **128 kernels** (kernel size = 6, stride = 1)  
- A max pooling layer with **pool size = 2** and **stride = 2**  
- A fully connected layer with **64 units** and **ReLU** activation  
- An output layer with **4 units** and **softmax** activation  

The input consists of one-hot encoded sequences, padded to the maximum length observed in the RBNS or RNAcompete datasets. Labels correspond to concentration ranges:  
- `0` — original input file label  
- `1` — < 100 nM  
- `2` — 100–500 nM  
- `3` — > 500 nM  

Training is performed with the **Adam** optimizer. We apply a learning-rate decay of approximately **0.009**, executed every **5000 steps** with a decay rate of **0.9**. The loss function used is **categorical cross-entropy**.

<div align="center">
  <img width="424" height="156" src="https://github.com/user-attachments/assets/a9b718bc-9462-401e-ad64-648de47efbd2" alt="Model Diagram">
</div>
