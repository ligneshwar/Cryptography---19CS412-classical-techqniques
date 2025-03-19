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


---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To develop a simple C program to implement PlayFair Cipher.

## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

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
#include <ctype.h>

#define SIZE 5

char keyMatrix[SIZE][SIZE];
int charPosition[26][2];

void generateKeyMatrix(const char *key) {
    int used[26] = {0};
    int row = 0, col = 0;

    for (int i = 0; key[i] != '\0'; i++) {
        char c = toupper(key[i]);
        if (c == 'J') c = 'I';
        if (!used[c - 'A'] && isalpha(c)) {
            keyMatrix[row][col] = c;
            charPosition[c - 'A'][0] = row;
            charPosition[c - 'A'][1] = col;
            used[c - 'A'] = 1;

            if (++col == SIZE) {
                col = 0;
                row++;
            }
        }
    }

    for (char c = 'A'; c <= 'Z'; c++) {
        if (c == 'J') continue;
        if (!used[c - 'A']) {
            keyMatrix[row][col] = c;
            charPosition[c - 'A'][0] = row;
            charPosition[c - 'A'][1] = col;

            if (++col == SIZE) {
                col = 0;
                row++;
            }
        }
    }
}

void formatText(char *text) {
    int len = strlen(text);
    for (int i = 0; i < len; i++) {
        if (text[i] == 'J') text[i] = 'I';
    }
}

void playfairEncrypt(const char *plainText, char *cipherText) {
    formatText((char*)plainText);
    int len = strlen(plainText);
    int k = 0;

    for (int i = 0; i < len; i += 2) {
        char a = toupper(plainText[i]);
        char b = (i + 1 < len) ? toupper(plainText[i + 1]) : 'X';

        if (a == b) b = 'X';

        int row1 = charPosition[a - 'A'][0];
        int col1 = charPosition[a - 'A'][1];
        int row2 = charPosition[b - 'A'][0];
        int col2 = charPosition[b - 'A'][1];

        if (row1 == row2) {
            cipherText[k++] = keyMatrix[row1][(col1 + 1) % SIZE];
            cipherText[k++] = keyMatrix[row2][(col2 + 1) % SIZE];
        } else if (col1 == col2) {
            cipherText[k++] = keyMatrix[(row1 + 1) % SIZE][col1];
            cipherText[k++] = keyMatrix[(row2 + 1) % SIZE][col2];
        } else {
            cipherText[k++] = keyMatrix[row1][col2];
            cipherText[k++] = keyMatrix[row2][col1];
        }
    }
    cipherText[k] = '\0';
}

void printKeyMatrix() {
    printf("\nKey Matrix:\n");
    for (int i = 0; i < SIZE; i++) {
        for (int j = 0; j < SIZE; j++) {
            printf("%c ", keyMatrix[i][j]);
        }
        printf("\n");
    }
}

int main() {
    char key[100], plainText[100], cipherText[100];

    printf("Enter the key: ");
    scanf("%s", key);

    printf("Enter the plain text: ");
    scanf("%s", plainText);

    generateKeyMatrix(key);
    printKeyMatrix();
    playfairEncrypt(plainText, cipherText);

    printf("\nEncrypted Text: %s\n", cipherText);

    return 0;
}
```

## OUTPUT:
![{57E50ACE-322E-46DE-A9A4-6F31D76FD3D3}](https://github.com/user-attachments/assets/9fb7853d-7cd8-43f0-94a9-7a01fa008125)



## RESULT:
The program is executed successfully



---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:

To develop a simple C program to implement Hill Cipher.

## DESIGN STEPS:

### Step 1:

Design of Hill Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:
## Developed by : K.Ligneshwar
## Reg No:212223230113
```
#include <stdio.h>

int main() 
{
    unsigned int key[3][3] = {{6, 24, 1}, {13, 16, 10}, {20, 17, 15}};
    unsigned int inverseKey[3][3] = {{8, 5, 10}, {21, 8, 21}, {21, 12, 8}};

    char msg[4];
    unsigned int enc[3] = {0}, dec[3] = {0};

    printf("Enter plain text: ");
    scanf("%3s", msg);

    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            enc[i] += key[i][j] * (msg[j] - 'A') % 26;

    printf("Encrypted Cipher Text: %c%c%c\n", enc[0] % 26 + 'A', enc[1] % 26 + 'A', enc[2] % 26 + 'A');

    for (int i = 0; i < 3; i++)
        for (int j = 0; j < 3; j++)
            dec[i] += inverseKey[i][j] * enc[j] % 26;

    printf("Decrypted Cipher Text: %c%c%c\n", dec[0] % 26 + 'A', dec[1] % 26 + 'A', dec[2] % 26 + 'A');

    return 0;
}
```
## OUTPUT:
![{6E1E1844-36BB-42FA-A9EC-22C9C1620D45}](https://github.com/user-attachments/assets/679bffb3-f2fb-4835-baf6-afe016a79185)



## RESULT:
The program is executed successfully

--------------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:

To develop a simple C program to implement Vigenere Cipher.

## DESIGN STEPS:

### Step 1:

Design of Vigenere Cipher algorithnm 

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
#include <ctype.h>

#define MAX_LENGTH 100

int main() 
{
    char input[MAX_LENGTH];
    char key[MAX_LENGTH];
    char result[MAX_LENGTH];

    printf("Enter the text to encrypt: ");
    fgets(input, MAX_LENGTH, stdin);
    input[strcspn(input, "\n")] = '\0'; 

    printf("Enter the key: ");
    fgets(key, MAX_LENGTH, stdin);
    key[strcspn(key, "\n")] = '\0'; 

    int inputLength = strlen(input);
    int keyLength = strlen(key);

    for (int i = 0, j = 0; i < inputLength; ++i) 
    {
        char currentChar = input[i];

        if (isalpha(currentChar))
        {
            int shift = toupper(key[j % keyLength]) - 'A';
            int base = isupper(currentChar) ? 'A' : 'a';

            result[i] = ((currentChar - base + shift + 26) % 26) + base;
            ++j;
        }
        else
        {
            result[i] = currentChar;
        }
    }

    result[inputLength] = '\0';
    printf("Encrypted text: %s\n", result);

    for (int i = 0, j = 0; i < inputLength; ++i) 
    {
        char currentChar = result[i];

        if (isalpha(currentChar)) 
        {
            int shift = toupper(key[j % keyLength]) - 'A';
            int base = isupper(currentChar) ? 'A' : 'a';

            result[i] = ((currentChar - base - shift + 26) % 26) + base;
            ++j;
        }
    }

    result[inputLength] = '\0';
    printf("Decrypted text: %s\n", result);

    return 0;
}
```

## OUTPUT:
![{D16D69AD-4697-420B-AAA5-CBE61B01FF18}](https://github.com/user-attachments/assets/a8e53b04-2073-422c-9730-6654d561dd5d)


## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:

To develop a simple C program to implement Rail Fence Cipher.

## DESIGN STEPS:

### Step 1:

Design of Rail Fence Cipher algorithnm 

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

#define MAX 100

void railFenceEncrypt(char *plainText, char *cipherText, int key) {
    int len = strlen(plainText);
    int row, col, k = 0;
    char rail[key][len];


    for (row = 0; row < key; row++)
        for (col = 0; col < len; col++)
            rail[row][col] = '\n';

    int direction = -1;
    row = 0;

    // Fill the rail matrix
    for (col = 0; col < len; col++) {
        rail[row][col] = plainText[col];

        if (row == 0 || row == key - 1)
            direction *= -1;

        row += direction;
    }

    // Read the matrix row-wise to get the cipher text
    for (row = 0; row < key; row++) {
        for (col = 0; col < len; col++) {
            if (rail[row][col] != '\n')
                cipherText[k++] = rail[row][col];
        }
    }

    cipherText[k] = '\0';
}

void railFenceDecrypt(char *cipherText, char *plainText, int key) {
    int len = strlen(cipherText);
    int row, col, k = 0;
    char rail[key][len];

    
    for (row = 0; row < key; row++)
        for (col = 0; col < len; col++)
            rail[row][col] = '\n';

    int direction = -1;
    row = 0;

    // Mark the positions in the rail matrix
    for (col = 0; col < len; col++) {
        rail[row][col] = '*';

        if (row == 0 || row == key - 1)
            direction *= -1;

        row += direction;
    }

    // Fill the rail matrix with cipher text
    for (row = 0; row < key; row++) {
        for (col = 0; col < len; col++) {
            if (rail[row][col] == '*' && k < len)
                rail[row][col] = cipherText[k++];
        }
    }

    // Read the matrix in zigzag order to decrypt
    row = 0;
    direction = -1;
    k = 0;

    for (col = 0; col < len; col++) {
        plainText[k++] = rail[row][col];

        if (row == 0 || row == key - 1)
            direction *= -1;

        row += direction;
    }

    plainText[k] = '\0';
}

int main() {
    char plainText[MAX], cipherText[MAX];
    int key;

    printf("Enter the plain text: ");
    scanf("%s", plainText);

    printf("Enter the key (number of rails): ");
    scanf("%d", &key);

    railFenceEncrypt(plainText, cipherText, key);
    printf("Cipher Text after applying  rail fence: %s\n", cipherText);

    railFenceDecrypt(cipherText, plainText, key);
    printf("Text after Decrypted : %s\n", plainText);

    return 0;
}


```

## OUTPUT:

![image](https://github.com/user-attachments/assets/516d951d-255f-4b73-ab06-78447a5be6ac)


## RESULT:
The program is executed successfully

