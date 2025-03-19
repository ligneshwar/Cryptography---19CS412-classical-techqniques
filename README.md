# Cryptography---19CS412-classical-techqniques


## Caeser Cipher

Caeser Cipher using with different key values

# AIM:

To develop a simple C program to implement Caeser Cipher.


## DESIGN STEPS:

### Step 1:

Design of Caeser Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
## Developed by : K.Ligneshwar
## Reg No:212223230113
```
#include <stdio.h>
#include <string.h>

int main()
 {
    int key;
    char s[1000];

    printf("Enter a plaintext to encrypt:\n");
    fgets(s, sizeof(s), stdin);
    printf("Enter key:\n");
    scanf("%d", &key);

    int n = strlen(s);

    for (int i = 0; i < n; i++) 
    {
        char c = s[i];
        if (c >= 'a' && c <= 'z') 
        {
            s[i] = 'a' + (c - 'a' + key) % 26;
        }
        else if (c >= 'A' && c <= 'Z')
        {
            s[i] = 'A' + (c - 'A' + key) % 26;
        }
    }
    printf("Encrypted message: %s\n", s);

    for (int i = 0; i < n; i++)
    {
        char c = s[i];
        if (c >= 'a' && c <= 'z') 
        {
            s[i] = 'a' + (c - 'a' - key + 26) % 26; 
        }
        else if (c >= 'A' && c <= 'Z')
        {
            s[i] = 'A' + (c - 'A' - key + 26) % 26; 
        }
    }
    printf("Decrypted message: %s\n", s);

    return 0;
}

```

## OUTPUT:

![{AD3CFF75-BCAB-45D8-9199-D85F9B0F862B}](https://github.com/user-attachments/assets/8f0277aa-128b-47e1-aa38-ed3cf5232a63)




## RESULT:
The program is executed successfully
