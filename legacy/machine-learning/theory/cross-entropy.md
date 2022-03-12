# Entropy, Cross Entropy, and KL Divergence

## Entropy

p: true distribution

H(p) = sum(p_i * -log_2(p_i))

## Cross entropy

q: predicted distribution

H(p, q) = sum(p_i * -log_2(q_i))
H(p,q) = entropy + KL_divergence

Example:

p = [0.5, 0.5]
q = [0.1, 0.9]

entropy(p) = 1
cross_entropy(p,q) = 1.737