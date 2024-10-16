# playfair_chiper

Nama : Tatia Deswita Anggraeni

Nim : 312210478

Kelas : Ti.22.a5

'''
# Membuat tabel 5x5 Playfair Cipher
def create_table(key):
    alphabet = "ABCDEFGHIKLMNOPQRSTUVWXYZ"
    key = "".join(dict.fromkeys(key.upper().replace("J", "I")))  # Hilangkan duplikat, ganti J dengan I
    table = [c for c in key if c in alphabet]
    for c in alphabet:
        if c not in table:
            table.append(c)
    return [table[i:i + 5] for i in range(0, 25, 5)]

# Mendapatkan posisi dari huruf di tabel
def get_position(table, char):
    for row in range(5):
        for col in range(5):
            if table[row][col] == char:
                return row, col
    return None

# Memproses plaintext menjadi digram
def prepare_text(text):
    text = text.upper().replace("J", "I").replace(" ", "")
    prepared_text = []
    i = 0
    while i < len(text):
        if i + 1 < len(text) and text[i] == text[i + 1]:
            prepared_text.append(text[i] + 'X')
            i += 1
        else:
            prepared_text.append(text[i:i + 2])
            i += 2
    if len(prepared_text[-1]) == 1:
        prepared_text[-1] += 'X'
    return prepared_text

# Enkripsi menggunakan aturan Playfair Cipher
def encrypt_playfair(plaintext, table):
    digrams = prepare_text(plaintext)
    ciphertext = ""
    
    for digram in digrams:
        row1, col1 = get_position(table, digram[0])
        row2, col2 = get_position(table, digram[1])
        
        # Aturan enkripsi Playfair Cipher
        if row1 == row2:
            ciphertext += table[row1][(col1 + 1) % 5] + table[row2][(col2 + 1) % 5]
        elif col1 == col2:
            ciphertext += table[(row1 + 1) % 5][col1] + table[(row2 + 1) % 5][col2]
        else:
            ciphertext += table[row1][col2] + table[row2][col1]
    
    return ciphertext

# Kunci dan teks yang akan dienkripsi
key = "TEKNIK INFORMATIKA"
plaintexts = [
    "GOOD BROOM SWEEP CLEAN",
    "REDWOOD NATIONAL STATE PARK",
    "JUNK FOOD AND HEALTH PROBLEMS"
]

# Membuat tabel Playfair Cipher
table = create_table(key)
print("Tabel Playfair Cipher:")
for row in table:
    print(row)

# Enkripsi setiap teks
for plaintext in plaintexts:
    ciphertext = encrypt_playfair(plaintext, table)
    print(f"Plaintext: {plaintext}")
    print(f"Ciphertext: {ciphertext}")
    print()
'''

# Hasil output

![Screenshot (61)](https://github.com/user-attachments/assets/a6387986-c23d-48e5-879a-fa84b870f85f)

