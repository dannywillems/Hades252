# Hades252

Implementation of Hades252 over the Ristretto Scalar field.

*Unstable* : No guarantees can be made regarding the API stability.

## Parameters

- p = 2^252 + 27742317777372353535851937790883648493

- Security level is 126 bits

- width = 6

- Number of full rounds = 8 . There are four full rounds at the beginning and four full rounds at the end

- Number of partial rounds = 127, where each partial round has one inversion s-box.

- Number of round constants = 810

## Example
```
        // Initiate hash function with default parameters
        let mut h = Hash::new();
        // Add "hello" to input
        h.input_bytes(b"hello").unwrap();
        // Add "world" to input
        h.input_bytes(b"world").unwrap();
        // Add a number to input
        let scalar = Scalar::from(10 as u64);
        h.input(scalar).unwrap();
        // Return digest
        let digest = h.result().unwrap(); // c300e197466998bd49ac170fa48d4adf4922cd64b5d18ca0af63973a4fdd7305
```
## Deviations

- Round constants are generated by first hashing the seed 'hades252_full_rounds', the digest is then mapped onto a scalar in the ristretto scalar field. We then take the byte encoding of the scalar and use it as the seed for the next constant, and so on.

- The MDS matrix is a cauchy matrix, the method used to generate it, is noted in section "Concrete Instantiations Poseidon and Starkad"

## Reference

https://eprint.iacr.org/2019/458.pdf