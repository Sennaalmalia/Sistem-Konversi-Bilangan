// 162024019 - Senna Almalia
// Sistem Konversi Bilangan
// 15 November 2025

#include <stdio.h>
#include <string.h>

// Dari biner ke desimal
long long binerKeDesimal(long long angkaBiner) {
    long long angkaDesimal = 0, pangkat = 1;
    while (angkaBiner > 0) {
        int digit = angkaBiner % 10;
        angkaDesimal += digit * pangkat;
        pangkat *= 2;
        angkaBiner /= 10;
    }
    return angkaDesimal;
}

// Dari oktal ke desimal
long long oktalKeDesimal(long long angkaOktal) {
    long long angkaDesimal = 0, pangkat = 1;
    while (angkaOktal > 0) {
        int digit = angkaOktal % 10;
        angkaDesimal += digit * pangkat;
        pangkat *= 8;
        angkaOktal /= 10;
    }
    return angkaDesimal;
}

// Dari heksa ke desimal
long long heksaKeDesimal(char angkaHeksa[]) {
    long long angkaDesimal = 0, pangkat = 1;
    int n = strlen(angkaHeksa);

    for (int i = n - 1; i >= 0; i--) {
        char c = angkaHeksa[i];
        int nilai;
        if (c >= '0' && c <= '9') nilai = c - '0';
        else if (c >= 'A' && c <= 'F') nilai = c - 'A' + 10;
        else if (c >= 'a' && c <= 'f') nilai = c - 'a' + 10;
        else nilai = 0;

        angkaDesimal += nilai * pangkat;
        pangkat *= 16;
    }
    return angkaDesimal;
}

void desimalKeBiner(long long angkaDesimal, char hasil[]) {
    if (angkaDesimal == 0) {
        strcpy(hasil, "0");
        return;
    }

    char temp[100];
    int indeks = 0;

    while (angkaDesimal > 0) {
        temp[indeks++] = (angkaDesimal % 2) + '0';
        angkaDesimal /= 2;
    }

    for (int i = 0; i < indeks; i++)
        hasil[i] = temp[indeks - 1 - i];
    hasil[indeks] = '\0';
}

void desimalKeOktal(long long angkaDesimal, char hasil[]) {
    if (angkaDesimal == 0) {
        strcpy(hasil, "0");
        return;
    }

    char temp[100];
    int indeks = 0;

    while (angkaDesimal > 0) {
        temp[indeks++] = (angkaDesimal % 8) + '0';
        angkaDesimal /= 8;
    }

    for (int i = 0; i < indeks; i++)
        hasil[i] = temp[indeks - 1 - i];
    hasil[indeks] = '\0';
}

void desimalKeHeksa(long long angkaDesimal, char hasil[]) {
    if (angkaDesimal == 0) {
        strcpy(hasil, "0");
        return;
    }

    char temp[100];
    int indeks = 0;

    while (angkaDesimal > 0) {
        int sisa = angkaDesimal % 16;
        if (sisa < 10) temp[indeks] = sisa + '0';
        else temp[indeks] = (sisa - 10) + 'A';
        indeks++;
        angkaDesimal /= 16;
    }

    for (int i = 0; i < indeks; i++)
        hasil[i] = temp[indeks - 1 - i];
    hasil[indeks] = '\0';
}

int main() {
    int menuPilihan;

    printf("============================================\n");
    printf("     PROGRAM KONVERSI BILANGAN SEDERHANA   \n");
    printf("============================================\n\n");

    do {
        printf("============================================\n");
        printf("         MENU PILIHAN\n");
        printf("============================================\n");
        printf(" 1. Biner ke Semua\n");
        printf(" 2. Desimal ke Semua\n");
        printf(" 3. Oktal ke Semua\n");
        printf(" 4. Heksa ke Semua\n");
        printf(" 0. Keluar\n");
        printf("============================================\n");
        printf("Pilih: ");
        scanf("%d", &menuPilihan);

        if (menuPilihan == 1) {
            long long angkaBiner;
            printf("\nMasukkan angka biner: ");
            scanf("%lld", &angkaBiner);

            long long angkaDesimal = binerKeDesimal(angkaBiner);
            char hasilBiner[100], hasilOktal[100], hasilHeksa[100];
            desimalKeBiner(angkaDesimal, hasilBiner);
            desimalKeOktal(angkaDesimal, hasilOktal);
            desimalKeHeksa(angkaDesimal, hasilHeksa);

            printf("\n=== HASIL KONVERSI ===\n");
            printf("Biner   : %lld\n", angkaBiner);
            printf("Desimal : %lld\n", angkaDesimal);
            printf("Oktal   : %s\n", hasilOktal);
            printf("Heksa   : %s\n", hasilHeksa);
        }

        else if (menuPilihan == 2) {
            long long angkaDesimal;
            printf("\nMasukkan angka desimal: ");
            scanf("%lld", &angkaDesimal);

            char hasilBiner[100], hasilOktal[100], hasilHeksa[100];
            desimalKeBiner(angkaDesimal, hasilBiner);
            desimalKeOktal(angkaDesimal, hasilOktal);
            desimalKeHeksa(angkaDesimal, hasilHeksa);

            printf("\n=== HASIL KONVERSI ===\n");
            printf("Biner   : %s\n", hasilBiner);
            printf("Desimal : %lld\n", angkaDesimal);
            printf("Oktal   : %s\n", hasilOktal);
            printf("Heksa   : %s\n", hasilHeksa);
        }

        else if (menuPilihan == 3) {
            long long angkaOktal;
            printf("\nMasukkan angka oktal: ");
            scanf("%lld", &angkaOktal);

            long long angkaDesimal = oktalKeDesimal(angkaOktal);
            char hasilBiner[100], hasilOktal[100], hasilHeksa[100];
            desimalKeBiner(angkaDesimal, hasilBiner);
            desimalKeOktal(angkaDesimal, hasilOktal);
            desimalKeHeksa(angkaDesimal, hasilHeksa);

            printf("\n=== HASIL KONVERSI ===\n");
            printf("Oktal   : %lld\n", angkaOktal);
            printf("Desimal : %lld\n", angkaDesimal);
            printf("Biner   : %s\n", hasilBiner);
            printf("Heksa   : %s\n", hasilHeksa);
        }

        else if (menuPilihan == 4) {
            char angkaHeksa[100];
            printf("\nMasukkan angka heksa: ");
            scanf("%s", angkaHeksa);

            long long angkaDesimal = heksaKeDesimal(angkaHeksa);
            char hasilBiner[100], hasilOktal[100];
            desimalKeBiner(angkaDesimal, hasilBiner);
            desimalKeOktal(angkaDesimal, hasilOktal);

            printf("\n=== HASIL KONVERSI ===\n");
            printf("Heksa   : %s\n", angkaHeksa);
            printf("Desimal : %lld\n", angkaDesimal);
            printf("Biner   : %s\n", hasilBiner);
            printf("Oktal   : %s\n", hasilOktal);
        }

        else if (menuPilihan == 0) {
            printf("\nTerima kasih!\n");
        }

        else {
            printf("\nPilihan tidak valid!\n");
        }

    } while (menuPilihan != 0);

    return 0;
}
# Sistem-Konversi-Bilangan
