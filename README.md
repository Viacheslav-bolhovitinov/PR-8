#include <stdio.h>
#include <string.h>

#define MAX_LEN 14

unsigned long long factorial(int n) {
    unsigned long long result = 1;
    for (int i = 2; i <= n; i++) {
        result *= i;
    }
    return result;
}

int main() {
    char word[MAX_LEN + 1];
    printf("Введіть слово (до 14 букв): ");
    scanf("%s", word);

    int len = strlen(word);
    if (len > MAX_LEN) {
        printf("Слово перевищує допустиму довжину.\n");
        return 1;
    }

    int counts[26] = {0};
    for (int i = 0; i < len; i++) {
        counts[word[i] - 'A']++;
    }

    unsigned long long total_anagrams = factorial(len);
    for (int i = 0; i < 26; i++) {
        if (counts[i] > 1) {
            total_anagrams /= factorial(counts[i]);
        }
    }

    printf("Кількість можливих анаграм: %llu\n", total_anagrams);

    return 0;
}
