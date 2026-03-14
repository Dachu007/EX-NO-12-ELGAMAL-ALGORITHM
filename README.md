# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```
#include <stdio.h>
#include <stdlib.h>
#include <math.h>

// function for modular exponentiation
long long power(long long a, long long b, long long p)
{
    long long result = 1;
    a = a % p;

    while (b > 0)
    {
        if (b % 2 == 1)
            result = (result * a) % p;

        a = (a * a) % p;
        b = b / 2;
    }
    return result;
}

int main()
{
    long long p, g, x, y, k, m;
    long long a, b;

    printf("Enter prime number p: ");
    scanf("%lld", &p);

    printf("Enter primitive root g: ");
    scanf("%lld", &g);

    printf("Enter private key x: ");
    scanf("%lld", &x);

    printf("Enter message (number): ");
    scanf("%lld", &m);

    // Public key
    y = power(g, x, p);

    printf("Public Key (p, g, y) = (%lld, %lld, %lld)\n", p, g, y);

    printf("Enter random key k: ");
    scanf("%lld", &k);

    // Encryption
    a = power(g, k, p);
    b = (m * power(y, k, p)) % p;

    printf("\nEncrypted Message: (a, b) = (%lld, %lld)\n", a, b);

    // Decryption
    long long s = power(a, x, p);
    long long s_inv = power(s, p - 2, p);  // modular inverse

    long long decrypted = (b * s_inv) % p;

    printf("Decrypted Message: %lld\n", decrypted);

    return 0;
}
```


## Output:





## Result:
The program is executed successfully.
