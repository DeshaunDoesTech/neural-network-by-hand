# Build a neural network by hand

Can two switches control a light that turns on only when the switches disagree? With a pencil and paper, you can build a neural network that makes this decision and check every prediction it can make.

## 1. Write down the target

Label the switches A and B. Use 0 for off and 1 for on. The light should turn on for (0, 1) and (1, 0). It should stay off for (0, 0) and (1, 1). This rule is called exclusive OR, or **XOR**.

## 2. Draw the connections

Draw A and B on the left, two neurons named **Any** and **Both** in the middle, and a **Light** neuron on the right. Draw an arrow from each switch to each middle neuron. Draw an arrow from each middle neuron to Light. The middle neurons form the hidden layer. Their answers to two simpler questions let Light decide whether exactly one switch is on.

## 3. Give each neuron a decision rule

A **weight** belongs to a connection. Multiply each incoming value by its weight, then add the products to get the **weighted sum**. Each neuron also has one **bias**, a number added to that sum once. The result is its score.

**Score = (first input × first weight) + (second input × second weight) + bias**

Use a **step activation** for all three neurons. A score of zero or higher gives an output of 1. A negative score gives an output of 0. Each arrow carries the activated output to the next neuron.

## 4. Label the weights and biases

Copy each weight onto its arrow and each bias inside its neuron.

| Neuron | Incoming values, in order | First weight | Second weight | Bias |
| --- | --- | ---: | ---: | ---: |
| Any | A, B | 1 | 1 | −0.5 |
| Both | A, B | 1 | 1 | −1.5 |
| Light | Any, Both | 1 | −2 | −0.5 |

Any and Both receive the same weighted sum. Their biases explain why they answer different questions. With one switch on, the sum is 1. Any gets a score of 0.5 and activates. Both gets −0.5 and stays silent. At the output, the negative weight from Both lets it cancel the signal from Any when both switches are on.

## 5. Run one prediction from left to right

Set A to 1 and B to 1. Work through the middle layer before calculating the light.

| Neuron | Weighted sum | Add bias | Activated output |
| --- | --- | --- | ---: |
| Any | (1 × 1) + (1 × 1) = 2 | 2 − 0.5 = 1.5 | 1 |
| Both | (1 × 1) + (1 × 1) = 2 | 2 − 1.5 = 0.5 | 1 |
| Light | (1 × 1) + (1 × −2) = −1 | −1 − 0.5 = −1.5 | 0 |

The light stays off. This trip from inputs through the hidden layer to a prediction is a **forward pass**.

## 6. Test every switch setting

Cover the last four columns and work each row on paper. Then compare your numbers. Every predicted light value should match the target from step 1.

| A | B | Any | Both | Light score | Predicted light |
| ---: | ---: | ---: | ---: | ---: | ---: |
| 0 | 0 | 0 | 0 | −0.5 | 0 |
| 0 | 1 | 1 | 0 | 0.5 | 1 |
| 1 | 0 | 1 | 0 | 0.5 | 1 |
| 1 | 1 | 1 | 1 | −1.5 | 0 |

## 7. Change one bias and predict the effect

Move the bias of Both from −1.5 to −0.5. Which rows change? For either one-switch setting, Both now activates alongside Any. Light receives a score of −1.5 and turns off, so the network misses both cases it should recognize. Restore the original bias to recover all four predictions.

You chose the weights and biases by reasoning from the target. In a trained network, a learning algorithm adjusts those numbers using examples and a measure of prediction error. Here, choosing them by hand makes every decision visible.

## Support this guide

If this walkthrough helped you understand what happens inside a neuron, you can support my next tech guide on [Buy Me a Coffee](https://buymeacoffee.com/DeshaunDoesTech).

## License

© 2026 DeshaunDoesTech. This guide is licensed under [Creative Commons Attribution 4.0 International](LICENSE.md).
