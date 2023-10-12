# sistemlogin
#include <iostream>
#include <string>

using namespace std;

// Fungsi untuk mengenkripsi teks menggunakan Vigenere Cipher
string encryptVigenere(const string& plainText, const string& key) {
    string encryptedText = "";
    int keyLength = key.length();
    int textLength = plainText.length();

    for (int i = 0; i < textLength; i++) {
        char plainChar = plainText[i];
        if (isalpha(plainChar)) {
            char keyChar = key[i % keyLength];
            int shift = tolower(keyChar) - 'a';

            if (isupper(plainChar)) {
                char encryptedChar = ((plainChar - 'A' + shift) % 26) + 'A';
                encryptedText += encryptedChar;
            } else {
                char encryptedChar = ((plainChar - 'a' + shift) % 26) + 'a';
                encryptedText += encryptedChar;
            }
        } else {
            encryptedText += plainChar;
        }
    }

    return encryptedText;
}

// Fungsi untuk mendekripsi teks menggunakan Vigenere Cipher
string decryptVigenere(const string& encryptedText, const string& key) {
    string decryptedText = "";
    int keyLength = key.length();
    int textLength = encryptedText.length();

    for (int i = 0; i < textLength; i++) {
        char encryptedChar = encryptedText[i];
        if (isalpha(encryptedChar)) {
            char keyChar = key[i % keyLength];
            int shift = tolower(keyChar) - 'a';

            if (isupper(encryptedChar)) {
                char decryptedChar = ((encryptedChar - 'A' - shift + 26) % 26) + 'A';
                decryptedText += decryptedChar;
            } else {
                char decryptedChar = ((encryptedChar - 'a' - shift + 26) % 26) + 'a';
                decryptedText += decryptedChar;
            }
        } else {
            decryptedText += encryptedChar;
        }
    }

    return decryptedText;
}

int main() {
    string key = "secretkey";
    string storedPassword = encryptVigenere("Password123", key);

    string username, password;
    cout << "Username: ";
    cin >> username;
    cout << "Password: ";
    cin >> password;

    string decryptedPassword = decryptVigenere(storedPassword, key);

    if (password == decryptedPassword) {
        cout << "Login berhasil!" << endl;
    } else {
        cout << "Login gagal!" << endl;
    }

    return 0;
}
