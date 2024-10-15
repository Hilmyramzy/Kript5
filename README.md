Nama : Hilmy Syaddad Ramzy

NIM 312210162

Kelas : TI22A1

Soal : 
Latihan :
Lakukan enkripsi Playfair Cihper pada plaintext:

GOOD BROOM SWEEP CLEAN
REDWOOD NATIONAL STATE PARK
JUNK FOOD AND HEALTH PROBLEMS

Dengan kunci “TEKNIK INFORMATIKA”

Kumpulkan : Capture hasil Enkrip dan Dekripnya, beserta Link Githubnya.
![image](https://github.com/user-attachments/assets/e22fcd0c-148f-4e39-9682-0daa51ce7f1b)








Langkah-langkah:

Siapkan Kunci: Misalkan kita menggunakan kunci "TEKNIK INFORMATIKA".


Membuat Tabel 5x5: Hilangkan huruf yang berulang dari kunci dan isi tabel dengan huruf alfabet yang tersisa, menggabungkan "I" dan "J" menjadi satu kotak.

T  E  K  N  I
F  O  R  M  A
B  C  D  G  H
L  P  Q  S  U
V  W  X  Y  Z


Bagi Plaintext menjadi Digraf (Pasangan Huruf): Misalkan plaintext yang akan dienkripsi adalah "GOOD BROOM". Kita pisahkan menjadi pasangan huruf (digraf):
GO OD BR OM

Aturan Enkripsi:

Jika dua huruf berada di baris yang sama, geser ke kanan (huruf paling kanan akan melingkar ke kiri).

Jika dua huruf berada di kolom yang sama, geser ke bawah (huruf paling bawah akan melingkar ke atas).

Jika huruf-hurufnya membentuk persegi panjang, gantikan dengan huruf-huruf di sudut yang berlawanan pada persegi.

Proses Enkripsi:

"GO": G berada di (3, 1), O berada di (2, 2) → hasil: C dan R

"OD": O berada di (2, 2), D berada di (3, 3) → hasil: R dan M

"BR": B berada di (3, 1), R berada di (2, 3) → hasil: D dan K

"OM": O berada di (2, 2), M berada di (2, 4) → hasil: R dan N

Jadi, hasil enkripsi dari "GOOD BROOM" dengan Playfair Cipher menggunakan kunci "TEKNIK INFORMATIKA" adalah:

"CR RM DK RN"

=============================================================================================================
enkripsi Playfair Cipher untuk plaintext "REDWOOD NATIONAL STATE PARK" menggunakan kunci "TEKNIK INFORMATIKA".

Langkah-langkah:

Siapkan Kunci dan Tabel 5x5: Kunci yang digunakan adalah "TEKNIK INFORMATIKA". Kita hilangkan huruf yang berulang dan buat tabel 5x5:
T  E  K  N  I
F  O  R  M  A
B  C  D  G  H
L  P  Q  S  U
V  W  X  Y  Z

Pisahkan Plaintext Menjadi Digraf: Text: "REDWOOD NATIONAL STATE PARK"

Kita hilangkan spasi dan pisahkan menjadi pasangan huruf (digraf):

RE DW OO DN AT IO NA LS TA TE PA RK

Karena ada dua huruf yang sama dalam satu pasangan (seperti "OO"), kita tambahkan "X" di antara mereka untuk memisahkan pasangan tersebut.

Jadi, digrafnya menjadi:

RE DW OX OD DN AT IO NA LS TA TE PA RK

Proses Enkripsi:

"RE": R berada di (2, 3), E berada di (1, 2) → hasil: K dan O

"DW": D berada di (3, 3), W berada di (5, 2) → hasil: C dan X

"OX": O berada di (2, 2), X berada di (5, 3) → hasil: R dan W

"OD": O berada di (2, 2), D berada di (3, 3) → hasil: R dan M

"DN": D berada di (3, 3), N berada di (1, 4) → hasil: G dan K

"AT": A berada di (2, 5), T berada di (1, 1) → hasil: I dan F

"IO": I berada di (1, 5), O berada di (2, 2) → hasil: A dan M

"NA": N berada di (1, 4), A berada di (2, 5) → hasil: I dan M

"LS": L berada di (4, 1), S berada di (4, 4) → hasil: P dan U

"TA": T berada di (1, 1), A berada di (2, 5) → hasil: I dan F

"TE": T berada di (1, 1), E berada di (1, 2) → hasil: E dan K

"PA": P berada di (4, 2), A berada di (2, 5) → hasil: U dan M

"RK": R berada di (2, 3), K berada di (1, 3) → hasil: D dan R

=====================================================================
Plaintext 3: "JUNK FOOD AND HEALTH PROBLEMS"

JU NK FO OD AN DH EA LT HP RO BL EM SX

Proses Enkripsi:

"JU" → I dan Z
"NK" → I dan N
"FO" → O dan R
"OD" → R dan M
"AN" → I dan F
"DH" → G dan H
"EA" → E dan M
"LT" → L dan T
"HP" → U dan C
"RO" → M dan F
"BL" → B dan L
"EM" → A dan G
"SX" → Y dan Q

Hasil Enkripsi:

IZ IN OR RM IF GH EM LT UC MF BL AG YQ

==========================================================================================================

def generate_key_matrix(key):
    key = key.upper().replace("J", "I")
    matrix = []
    seen = set()

    for char in key:
        if char not in seen and char.isalpha():
            seen.add(char)
            matrix.append(char)

    for char in "ABCDEFGHIKLMNOPQRSTUVWXYZ":
        if char not in seen:
            matrix.append(char)
            seen.add(char)

    return [matrix[i:i + 5] for i in range(0, 25, 5)]

def prepare_text(plaintext):
    # Mengabaikan spasi dan mengganti 'J' dengan 'I'
    plaintext = plaintext.upper().replace("J", "I").replace(" ", "")
    text = ""

    i = 0
    while i < len(plaintext):
        char1 = plaintext[i]
        if not char1.isalpha():
            i += 1
            continue

        if i + 1 < len(plaintext):
            char2 = plaintext[i + 1]
        else:
            char2 = "X"

        if char1 == char2:
            text += char1 + "X"
            i += 1
        else:
            text += char1 + char2
            i += 2

    if len(text) % 2 != 0:
        text += "X"

    return text

def find_position(matrix, char):
    for row in range(5):
        for col in range(5):
            if matrix[row][col] == char:
                return row, col
    return None

def encrypt_pair(matrix, char1, char2):
    pos1 = find_position(matrix, char1)
    pos2 = find_position(matrix, char2)

    if pos1 is None or pos2 is None:
        raise ValueError(f"Karakter '{char1}' atau '{char2}' tidak ditemukan dalam matriks")

    row1, col1 = pos1
    row2, col2 = pos2

    if row1 == row2:
        return matrix[row1][(col1 + 1) % 5] + matrix[row2][(col2 + 1) % 5]
    elif col1 == col2:
        return matrix[(row1 + 1) % 5][col1] + matrix[(row2 + 1) % 5][col2]
    else:
        return matrix[row1][col2] + matrix[row2][col1]

def encrypt_playfair(plaintext, key):
    matrix = generate_key_matrix(key)
    prepared_text = prepare_text(plaintext)
    ciphertext = ""

    for i in range(0, len(prepared_text), 2):
        char1 = prepared_text[i]
        char2 = prepared_text[i + 1]
        ciphertext += encrypt_pair(matrix, char1, char2)

    return ciphertext

# Input kunci dan plaintext
key = "TEKNIK INFORMATIKA"
plaintexts = [
    "GOOD BROOM SWEEP CLEAN",
    "REDWOOD NATIONAL STATE PARK",
    "JUNK FOOD AND HEALTH PROBLEMS"
]

# Hasil enkripsi
for i, plaintext in enumerate(plaintexts, 1):
    try:
        ciphertext = encrypt_playfair(plaintext, key)
        print(f"Plaintext {i}: {plaintext}")
        print(f"Ciphertext {i}: {ciphertext}\n")
    except ValueError as e:
        print(f"Error pada Plaintext {i}: {e}")



![Screenshot (389)](https://github.com/user-attachments/assets/de399640-4191-4667-983b-09b180b2478c)





Penjelasan Kode:

create_playfair_matrix: Membuat matriks Playfair 5x5 berdasarkan kunci yang diberikan, memastikan huruf tidak berulang dan menganggap I sebagai J.

prepare_text: Mempersiapkan teks untuk dienkripsi dengan menghilangkan spasi, memisahkan huruf berpasangan, dan menambahkan X jika diperlukan.

find_position: Menemukan posisi huruf dalam matriks.

encrypt_pair: Mengenkripsi sepasang huruf sesuai aturan Playfair Cipher.

encrypt_playfair: Fungsi utama yang memproses seluruh teks untuk dienkripsi.





