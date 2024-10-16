# playfair_chiper

Nama : Tatia Deswita Anggraeni
Nim : 312210478
Kelas : Ti.22.a5


# def create_matrix(key):
    key = ''.join(sorted(set(key), key=key.index))  # remove duplicates
    key = key.replace('J', 'I')  # replace J with I
    alphabet = 'ABCDEFGHIKLMNOPQRSTUVWXYZ'
    matrix = key + ''.join(filter(lambda x: x not in key, alphabet))
    return [matrix[i:i + 5] for i in range(0, 25, 5)]

# def prepare_text(text):
    text = text.replace(' ', '').upper().replace('J', 'I')
    prepared = []
    i = 0
    while i < len(text):
        a = text[i]
        b = text[i + 1] if i + 1 < len(text) else 'X'
        if a == b:
            prepared.append(a + 'X')
            i += 1
        else:
            prepared.append(a + b)
            i += 2
    return prepared

# def encrypt(plaintext, key):
    matrix = create_matrix(key)
    pairs = prepare_text(plaintext)
    ciphertext = ''
    for a, b in pairs:
        row_a, col_a = divmod(matrix.index(a), 5)
        row_b, col_b = divmod(matrix.index(b), 5)
        if row_a == row_b:
            ciphertext += matrix[row_a][(col_a + 1) % 5]
            ciphertext += matrix[row_b][(col_b + 1) % 5]
        elif col_a == col_b:
            ciphertext += matrix[(row_a + 1) % 5][col_a]
            ciphertext += matrix[(row_b + 1) % 5][col_b]
        else:
            ciphertext += matrix[row_a][col_b]
            ciphertext += matrix[row_b][col_a]
    return ciphertext

# def decrypt(ciphertext, key):
    matrix = create_matrix(key)
    pairs = prepare_text(ciphertext)
    plaintext = ''
    for a, b in pairs:
        row_a, col_a = divmod(matrix.index(a), 5)
        row_b, col_b = divmod(matrix.index(b), 5)
        if row_a == row_b:
            plaintext += matrix[row_a][(col_a - 1) % 5]
            plaintext += matrix[row_b][(col_b - 1) % 5]
        elif col_a == col_b:
            plaintext += matrix[(row_a - 1) % 5][col_a]
            plaintext += matrix[(row_b - 1) % 5][col_b]
        else:
            plaintext += matrix[row_a][col_b]
            plaintext += matrix[row_b][col_a]
    return plaintext

# Contoh penggunaan
key = "TEKNIK INFORMATIKA"
plaintexts = [
    "GOOD BROOM SWEEP CLEAN",
    "REDWOOD NATIONAL STATE PARK",
    "JUNK FOOD AND HEALTH PROBLEMS"
]

for text in plaintexts:
    encrypted = encrypt(text, key)
    decrypted = decrypt(encrypted, key)
    print(f"Plaintext: {text}")
    print(f"Ciphertext: {encrypted}")
    print(f"Decrypted: {decrypted}")
    print()

    Hasil running

![Screenshot (55)](https://github.com/user-attachments/assets/ab111c2b-7f52-4aa2-9f2a-f00eb43110ab)
![Screenshot (56)](https://github.com/user-attachments/assets/b564f790-ac2f-41c7-9a7d-1ce9ab81e0f6)
![Screenshot (57)](https://github.com/user-attachments/assets/90214dd7-501a-4e29-9a93-4f0a59a59fbc)
![Screenshot (58)](https://github.com/user-attachments/assets/4d8a379d-3f9d-4918-9588-7b5f84d53eb0)
![Screenshot (59)](https://github.com/user-attachments/assets/22c333b7-85d4-4442-bc01-4cbe1345ef1d)
![Screenshot (60)](https://github.com/user-attachments/assets/c5fb6a62-4750-4e30-bb72-ab8e420ebac3)
