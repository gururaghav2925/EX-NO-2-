## EX. NO:2 IMPLEMENTATION OF PLAYFAIR CIPHER

 

## AIM:
 
To write a Python program to implement the Playfair Substitution technique.

## DESCRIPTION:

The Playfair cipher starts with creating a key table. The key table is a 5×5 grid of letters that will act as the key for encrypting your plaintext. Each of the 25 letters must be unique and one letter of the alphabet is omitted from the table (as there are 25 spots and 26 letters in the alphabet).

To encrypt a message, one would break the message into digrams (groups of 2 letters) such that, for example, "HelloWorld" becomes "HE LL OW OR LD", and map them out on the key table. The two letters of the diagram are considered as the opposite corners of a rectangle in the key table. Note the relative position of the corners of this rectangle. Then apply the following 4 rules, in order, to each pair of letters in the plaintext:
1.	If both letters are the same (or only one letter is left), add an "X" after the first letter
2.	If the letters appear on the same row of your table, replace them with the letters to their immediate right respectively
3.	If the letters appear on the same column of your table, replace them with the letters immediately below respectively
4.	If the letters are not on the same row or column, replace them with the letters on the same row respectively but at the other pair of corners of the rectangle defined by the original pair.
## EXAMPLE:
![image](https://github.com/Hemamanigandan/EX-NO-2-/assets/149653568/e6858d4f-b122-42ba-acdb-db18ec2e9675)

 

## ALGORITHM:

STEP-1: Read the plain text from the user.
STEP-2: Read the keyword from the user.
STEP-3: Arrange the keyword without duplicates in a 5*5 matrix in the row order and fill the remaining cells with missed out letters in alphabetical order. Note that ‘i’ and ‘j’ takes the same cell.
STEP-4: Group the plain text in pairs and match the corresponding corner letters by forming a rectangular grid.
STEP-5: Display the obtained cipher text.




## Program:

```py
def generate_matrix(key):
    key = key.upper().replace("J", "I")
    matrix = []
    used = set()
    for ch in key:
        if ch not in used and ch.isalpha():
            used.add(ch)
            matrix.append(ch)
    for ch in "ABCDEFGHIKLMNOPQRSTUVWXYZ":
        if ch not in used:
            used.add(ch)
    return [matrix[i:i+5] for i in range(0, 25, 5)]
def find_position(matrix, ch):
    for row in range(5):
        for col in range(5):
            if matrix[row][col] == ch:
                return row, col
    return None
def preprocess_text(text):
    text = text.upper().replace("J", "I")
    prepared = ""
    i = 0
    while i < len(text):
        ch1 = text[i]
        if not ch1.isalpha():
            i += 1
            continue
        if i+1 < len(text):
            ch2 = text[i+1]
            if ch1 == ch2:
                prepared += ch1 + "X"
                i += 1
            else:
                prepared += ch1 + ch2
                i += 2
        else:
            prepared += ch1 + "X"
            i += 1
    return prepared
def encrypt(text, matrix):
    cipher = ""
    for i in range(0, len(text), 2):
        ch1, ch2 = text[i], text[i+1]
        r1, c1 = find_position(matrix, ch1)
        r2, c2 = find_position(matrix, ch2)
        if r1 == r2:  
            cipher += matrix[r1][(c1+1) % 5] + matrix[r2][(c2+1) % 5]
        elif c1 == c2:  
            cipher += matrix[(r1+1) % 5][c1] + matrix[(r2+1) % 5][c2]
        else:  
            cipher += matrix[r1][c2] + matrix[r2][c1]
    return cipher
def decrypt(cipher, matrix):
    plain = ""
    for i in range(0, len(cipher), 2):
        ch1, ch2 = cipher[i], cipher[i+1]
        r1, c1 = find_position(matrix, ch1)
        r2, c2 = find_position(matrix, ch2)

        if r1 == r2: 
            plain += matrix[r1][(c1-1) % 5] + matrix[r2][(c2-1) % 5]
        elif c1 == c2:  
            plain += matrix[(r1-1) % 5][c1] + matrix[(r2-1) % 5][c2]
        else:  
            plain += matrix[r1][c2] + matrix[r2][c1]
    return plain
key = input("Enter the key: ")
matrix = generate_matrix(key)
print("\nPlayfair Matrix:")
for row in matrix:
    print(" ".join(row))
plain = input("\nEnter the plain text: ")
prepared_text = preprocess_text(plain)
cipher = encrypt(prepared_text, matrix)
decrypted = decrypt(cipher, matrix)
print("\nPrepared Text:", prepared_text)
print("Encrypted Text:", cipher)
print("Decrypted Text:", decrypted)



```





## Output:

<img width="1919" height="1019" alt="Screenshot 2025-08-30 094346" src="https://github.com/user-attachments/assets/a45e2e86-bb9d-41c9-a7ff-8806b6a987d9" />

<img width="1919" height="1020" alt="image" src="https://github.com/user-attachments/assets/5b90ae2a-a975-432e-8697-65978ba655ae" />


## Result:
Thus the Python program to implement the Playfair Substitution technique was  completed and successfully executed.
