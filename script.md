Let's say today you want to run some quantum computation.
There are plenty of commercial cloud servers after all.

How do you know if the result is right though?
Besides the fact that, well, the error rates are so high today you can pretty much guarantee it's wrong anyways.
Otherwise we have a lot more to worry about anyways.
But who knows, maybe next time they'll come up with a good quantum machine.
We're theoretical cryptographers anyways, so let's just pretend we have an ideal BQP server out there in the clouds.

Ok so we have our inputs, and we want to run some protocol with the server,
so at the end we either learn the right output or reject.
You might think this problem is solved by Mahadev a couple years ago.
FOCS best paper award.
That was for decision problems though. (BQP)
Turns out it's nontrivial to for...
Or at least nontrivial enough that I'm here telling you about it.

# Blindness

Another issue with this kind of cloud computing is of course privacy. Or blindness as we call it.
Basically we don't want the server to learns this input x.
Or this circuit C, but if we can hide x then hiding C becomes easy.
There's a standard transformation.

So the intuitive strategy is of course to just hit it with a homomorphic encryption scheme.
Took just a couple days.
I don't believe everyone missed it.
I honestly thought it's folklore,
but there were some previous literature claiming that getting both verifiability and blindness at the same time is hard even for BQP...
So here goes nothing I guess.

# Main theorem

TODO

# Challenges with Sampling

Ok so let me tell you a bit about why is SampBQP harder than BQP.

First of all, you can't just run Mahadev's protocol for each bit of output.
There are quite a few reasons why you can't do that,
but the first one is that you'll lose the joint distribution between qubits.
For example, let's say the output is an EPR pair, then the "correct" output will be 00 or 11.
But if you just consider this qubit by qubit, you can get 01 or 10.

I guess let me tell you how people do it classically with SampP and P,
so we can see why the same strategy wouldn't work here on the quantum server.

Let's say you have some classical circuit and its input, then the idea is to derandomize it.
You write your circuit like this (C(x; r)) with explicit random tape, then you pick a seed,
and you now have this (C'(x, seed)=C(x; H(seed))), and now you can just compute that bit-by-bit.

Now this construction will obviously not work.
Hidden variable theory and all that I guess.

# Verification of BQP

Ok so how did we actually do this.
We basically went through the relevant literature and made some non-black-box changes to the constructions and fix whatever proofs that broke.
So let me tell you a bit about the works that led up to this.

TODO table?

# MF16

# Measurement Protocol

# Parallel Repetition Theorem

TODO copy from slides notes

# Blindness

Ok here comes the funny part.
Let's say we start with our protocol earlier.
Or even better, let's just say we have some protocol.
Just any protocol from this long line of literature.
Or probably any 2-party protocol with a classical client and a quantum server really.

Let's say we have a quantum homomorphic encryption scheme.
This other one from Mahadev or maybe this one by Braverski (?) will both work.
As long as you can encrypt and decrypt classically.

so here the verifier just generates his keys and encrypts his message.
Here we're just gonna say evk is part of pk.
So he sends the pk and the encrypted message over.
The prover does the natural thing.
He just runs the next-message function on the ciphertext and sends the result back.

Now here's the tricky part.
Here we want the verifier to decrypt.
Then he computes the message, encrypt it and sends it over.
Basically you want this to be a fresh ciphertext, since the old dirty one causes some issues with security.
Some issues with simulation-based security that I'm just gonna brush under the rug.
Then well, you also want to send this thing over to the server.
So the server can update whatever intermediate computation he's got.
The rest basically follows from what you think it is.

So... yeah. Woooooo.
This thing is blind since the server just gets a bunch of ciphertexts.
And it basically preserves any soundness/completeness properties of the protocol.
Amazing, isn't it?

# thanks

Ok thanks! I'll take questions now. :)
