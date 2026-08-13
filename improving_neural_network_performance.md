# Improving Neural Network Performance

## 1. Vanishing Gradients
Problem: gradients become too small in early layers during backpropagation, so those layers barely learn.
- **Activation Functions** — using ReLU (or its variants) instead of sigmoid/tanh helps, since ReLU's slope doesn't shrink to near-zero for positive inputs.
- **Weight Initialization** — starting with well-scaled random weights (e.g. Xavier/Glorot, He initialization) instead of plain random values.

## 2. Overfitting
Problem: the model memorizes training data instead of learning general patterns.
- **Reduce Complexity / Increase Data** — use a smaller network, or gather more training examples.
- **Dropout Layers** — randomly "turn off" some neurons during training so the network can't rely too heavily on any single path.
- **Regularization (L1 & L2)** — add a penalty to the loss for large weights, keeping the model simpler.
- **Early Stopping** — stop training once validation performance stops improving, instead of running to the end.

## 3. Normalization
- **Normalizing Inputs** — scale input features (e.g. to mean 0, std 1) so no single feature dominates just because of its scale.
- **Batch Normalization** — normalize a layer's output within each mini-batch, which speeds up and stabilizes training.
- **Normalizing Activations** — similar idea, keeping values flowing through the network in a stable range.

## 4. Gradient Checking and Clipping
- **Gradient Checking** — a debugging technique that confirms your backprop math is computing gradients correctly (compares against a numerical approximation).
- **Gradient Clipping** — caps how large a gradient can get during training, so it can't destabilize learning (common with RNNs).

## 5. Optimizers
Different strategies for using the gradient to update weights.
- **Momentum** — keeps a "memory" of past updates so it doesn't zig-zag as much.
- **Adagrad** — adapts the learning rate per-parameter, shrinking it for frequently-updated weights.
- **RMSprop** — fixes Adagrad's tendency to shrink the learning rate too aggressively over time.
- **Adam** — combines Momentum and RMSprop; the most commonly used default optimizer.

## 6. Hyperparameter Tuning
Settings you choose *before* training starts — the model doesn't learn these on its own.

- **Number of Layers** — how deep the network is. Too few layers may underfit; too many can overfit or bring back vanishing gradients.
- **Number of Nodes (neurons per layer)** — controls how much the network can represent. Too few = underfitting; too many = overfitting and slower training.
- **Batch Size** — how many samples are processed before one weight update. Smaller batches = noisier but sometimes better generalization; larger batches = faster but smoother updates.
- **Activation Function** — choice like ReLU, Leaky ReLU, sigmoid, tanh, or softmax (for the output layer) — affects both learning speed and vanishing-gradient risk.
- **Epochs** — how many times the model sees the full training dataset. Too few = underfitting; too many = overfitting (unless paired with early stopping).
- **Learning Rate** — how big each weight-update step is. Too high = unstable or diverges; too low = painfully slow training.
- **Callbacks** — functions that run automatically at set points during training (e.g. end of each epoch):
  - **Early Stopping** — stop training when validation loss stops improving (see Section 2).
  - **ModelCheckpoint** — automatically saves the best-performing version of the model during training.
  - **ReduceLROnPlateau** — automatically shrinks the learning rate when progress stalls.
  - **LearningRateScheduler** — changes the learning rate on a fixed schedule (e.g. decreasing every few epochs).
- **Optimizer Choice** — which optimizer to use (see Section 5).
- **Weight Initialization Strategy** — see Section 1.
- **Regularization Strength** — how strongly the L1/L2 penalty is applied (see Section 2).
