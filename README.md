#include <stdio.h>

int main() {
    int n, r, i, j, deadlock = 1;
    printf("Enter the number of chefs: ");
    scanf("%d", &n);
    printf("Enter the maximum number of ingredients each chef can claim: ");
    scanf("%d", &r);

    int ingredients[n][r];
    for (i = 0; i < n; i++) {
        printf("Enter the ingredients claimed by chef %d (separated by spaces): ", i+1);
        for (j = 0; j < r; j++) {
            scanf("%d", &ingredients[i][j]);
        }
    }

    int unique_ingredients = r;
    for (i = 0; i < n; i++) {
        int count = 0;
        for (j = 0; j < r; j++) {
            if (ingredients[i][j] != 0) {
                count++;
            }
        }
        if (count < unique_ingredients) {
            unique_ingredients = count;
        }
    }

    int total_ingredients = unique_ingredients * n;
    printf("\nTotal number of ingredients in the kitchen: %d\n", total_ingredients);

    // Check for deadlock
    for (i = 0; i < n; i++) {
        for (j = i+1; j < n; j++) {
            int k;
            for (k = 0; k < r; k++) {
                if (ingredients[i][k] != 0 && ingredients[i][k] == ingredients[j][k]) {
                    printf("Deadlock detected! Chefs %d and %d require the same ingredient: %d\n", i+1, j+1, ingredients[i][k]);
                    deadlock = 0;
                    break;
                }
            }
            if (!deadlock) {
                break;
            }
        }
        if (!deadlock) {
            break;
        }
    }

    if (deadlock) {
        printf("No deadlock detected.\n");
    }

    return 0;
}
