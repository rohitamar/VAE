# VAE

Implementing VAE, Gumbel VAE and VQVAE

I tried Convolutional VAE on CIFAR10 for about 2 days, and the results weren't very good. It's either you need a larger model, better hyparameter tuning, or my code is wrong. Maybe I'll come back some time later to check on this (probably not).

Some modifications I found useful (or things I noticed) for CIFAR10 VAE:
- No biases, lower batch size [(source)](https://stats.stackexchange.com/questions/505027/can-i-use-the-mse-loss-function-along-with-a-sigmoid-activation-in-my-vae)

I think normal VAE is better than Gumbel Softmax, but maybe the embedding of the Gumbel VAE is easier to use and understand (because it's categorical embedding? not sure)

I came into this project thinking that VQVAEs were similar to VAEs, but I'd say they're pretty different. The reconstructions from VQVAE are similar to the other 3 models:
![idk](https://github.com/rohitamar/VAE/blob/main/reconstructions.png)

Sampling is much more interesting. You need some type of trained prior to correctly sample with a VQVAE. I didn't want to train a PixelCNN or any model for that matter. Instead, I resorted to independent sampling of the indices. My embedding layer is of size 9, so I found the probability distribution to generate each index (run through every sample in the dataset, encode, maintain counts). Then, I independently sampled each index and decoded. Obviously, I wasn't expecting very good results because a joint distribution prior is necessary to fully capture the relationships within the embedding layer. However, the sampling results were better than expected:
![idk](https://github.com/rohitamar/VAE/blob/main/sampling.png)

The results aren't that bad! I was expecting complete gibberish; perhaps, this speaks to the simplicity of the MNIST dataset. Anyhow, if you notice, when trying to sample the number 3, a perfect number 8 appears (row 4, column 2). This actually happened many times - that is, trying to sample one number and another number appearing instead. Here's a Jenson-Shannon matrix that I made to determine the relationship between the sampling distributions: 
![idk](https://github.com/rohitamar/VAE/blob/main/js_matrix.png)

You can see that the probability distribution for 1 is far from the other numbers -- this is important because in all my trials, I actually never experienced trying to sample for a 1 and getting another number (of course, I've had many trials where I sampled a one and got random pixels). Most of the other relationships, however, are pretty close as seen in the above matrix. If you want a closer look, I also made a dendrogram and visualized with MDS. 
