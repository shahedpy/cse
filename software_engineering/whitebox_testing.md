# White Box Testing (Path Testing)

## Practice Example 1

```c
#include <stdio.h>
int main() {
    char string[80];
    int index;
    printf("Enter the string for checking its characters: ");
    scanf("%s", string);

    for (index = 0; string[index] != '\0'; ++index) {
        if (string[index] >= '0' && string[index] <= '9')
            printf("%c is a digit\n", string[index]);
        else if ((string[index] >= 'A' && string[index] <= 'Z') | (string[index] >= 'a' && string[index] <= 'z'))
            printf("%c is an alphabet\n", string[index]);
        else
            printf("%c is a special character\n", string[index]);
    }
    return 0;
}
```

- a) Draw the Control Flow Graph for the program.
- b) Calculate the cyclomatic complexity of the program.
- c) List all independent paths.
- d) Design test cases from independent paths.

## Practice Example 2

```c
main() {
    char chr;
    printf("Enter the special character\n");
    scanf("%c", &chr);

    if ((chr != 48) && (chr != 49) && (chr != 50) && (chr != 51) && (chr != 52) &&
        (chr != 53) && (chr != 54) && (chr != 55) && (chr != 56) && (chr != 57)) {
        switch(chr) {
            case '*': printf("It is a special character"); break;
            case '#': printf("It is a special character"); break;
            case '@': printf("It is a special character"); break;
            case '!': printf("It is a special character"); break;
            case '%': printf("It is a special character"); break;
            default: printf("You have not entered a special character"); break;
        }
    } else {
        printf("You have not entered a character");
    }
}
```

- a) Draw the Control Flow Graph for the program.
- b) Calculate the cyclomatic complexity of the program.
- c) List all independent paths.
- d) Design test cases from independent paths.

## Practice Example 3

```c
#include <stdio.h>
int main() {
    int num;
    printf("Enter a number: ");
    scanf("%d", &num);

    if (num > 0) {
        if (num % 2 == 0)
            printf("%d is a positive even number\n", num);
        else
            printf("%d is a positive odd number\n", num);
    } else if (num < 0) {
        if (num % 2 == 0)
            printf("%d is a negative even number\n", num);
        else
            printf("%d is a negative odd number\n", num);
    } else {
        printf("The number is zero\n");
    }
    return 0;
}
```

- a) Draw the Control Flow Graph for the program.
- b) Calculate the cyclomatic complexity of the program.
- c) List all independent paths.
- d) Design test cases from independent paths.

## Practice Example 4

```c
#include <stdio.h>
int main() {
    char op;
    float a, b;

    printf("Enter operator (+, -, *, /): ");
    scanf(" %c", &op);

    printf("Enter two numbers: ");
    scanf("%f %f", &a, &b);

    switch (op) {
        case '+': printf("Result: %.2f\n", a + b); break;
        case '-': printf("Result: %.2f\n", a - b); break;
        case '*': printf("Result: %.2f\n", a * b); break;
        case '/':
            if (b != 0)
                printf("Result: %.2f\n", a / b);
            else
                printf("Division by zero not allowed!\n");
            break;
        default:
            printf("Invalid operator\n");
    }
    return 0;
}
```

- a) Draw the Control Flow Graph for the program.
- b) Calculate the cyclomatic complexity of the program.
- c) List all independent paths.
- d) Design test cases from independent paths.

