# VAE

Implementing VAE (MNIST, CIFAR10), Gumbel VAE.

I tried VAE on CIFAR10 for about 2 days, and the results weren't very good. It's either you need a larger model, better hyparameter tuning, or my code is wrong. Maybe I'll come back some time later to check on this (probably not).

Some modifications I found useful (or things I noticed) for CIFAR10 VAE:
- No biases, lower batch size [(source)](https://stats.stackexchange.com/questions/505027/can-i-use-the-mse-loss-function-along-with-a-sigmoid-activation-in-my-vae)
- After about 50-60 epochs, loss seems to plateau

I think normal VAE is better than Gumbel Softmax, but maybe the embedding of the Gumbel VAE is easier to use and understand (because it's categorical embedding? not sure)
