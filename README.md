# PIN-Code-Validation-System-in-C-

The PIN Code Validation System is a console-based application in C designed to verify user-entered PIN codes against a predefined list of valid PIN codes. The system provides features for PIN code entry, validation, and error handling.

### Features

1. **PIN Code Entry**:
   - Users can enter a PIN code through the console.
   - The entered PIN code is masked for security.

2. **PIN Code Validation**:
   - The system checks the entered PIN code against a list of valid PIN codes.
   - Provides feedback on whether the PIN code is valid or invalid.

3. **Error Handling**:
   - Manages incorrect PIN entries gracefully.
   - Allows a limited number of attempts before locking the user out.

### Implementation

Here is the complete code for the PIN Code Validation System in C:

```c
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include <conio.h>

#define MAX_ATTEMPTS 3
#define PIN_LENGTH 4

// Predefined valid PIN codes
const char *validPins[] = {
    "1234",
    "5678",
    "4321",
    "8765"
};
const int numValidPins = sizeof(validPins) / sizeof(validPins[0]);

// Function prototypes
int validatePin(const char *pin);
void enterPin(char *pin);

int main() {
    char pin[PIN_LENGTH + 1];
    int attempts = 0;

    printf("PIN Code Validation System\n");

    while (attempts < MAX_ATTEMPTS) {
        printf("\nEnter your PIN: ");
        enterPin(pin);

        if (validatePin(pin)) {
            printf("\nPIN is valid.\n");
            return 0;
        } else {
            printf("\nInvalid PIN. Try again.\n");
            attempts++;
        }
    }

    printf("\nToo many invalid attempts. Access denied.\n");
    return 1;
}

// Function to validate the entered PIN
int validatePin(const char *pin) {
    for (int i = 0; i < numValidPins; i++) {
        if (strcmp(pin, validPins[i]) == 0) {
            return 1;
        }
    }
    return 0;
}

// Function to securely enter the PIN
void enterPin(char *pin) {
    int i = 0;
    char ch;

    while (i < PIN_LENGTH) {
        ch = getch(); // Get character without echoing it
        if (ch >= '0' && ch <= '9') {
            pin[i] = ch;
            printf("*"); // Print asterisk instead of the character
            i++;
        } else if (ch == '\b' && i > 0) { // Handle backspace
            printf("\b \b");
            i--;
        }
    }
    pin[i] = '\0'; // Null-terminate the string
}
```

### Explanation

1. **Predefined Valid PIN Codes**:
   - An array of strings (`validPins`) holds the valid PIN codes.
   - The number of valid PIN codes is determined using `sizeof`.

2. **Function Prototypes**:
   - `validatePin(const char *pin)`: Validates the entered PIN against the list of valid PINs.
   - `enterPin(char *pin)`: Handles secure PIN entry.

3. **Main Function**:
   - Initializes variables for the PIN and the number of attempts.
   - Uses a loop to allow the user to enter a PIN up to `MAX_ATTEMPTS` times.
   - Calls `enterPin` to get the user's PIN input.
   - Calls `validatePin` to check if the entered PIN is valid.
   - Provides feedback and exits the program based on the validation result.

4. **PIN Validation**:
   - The `validatePin` function compares the entered PIN with each valid PIN using `strcmp`.
   - Returns `1` if a match is found and `0` otherwise.

5. **Secure PIN Entry**:
   - The `enterPin` function uses `getch` to read characters without echoing them to the console.
   - Displays an asterisk (`*`) for each entered digit to mask the PIN.
   - Handles backspace to allow correction of input.

### Running the Program

1. **Compile the Program**:
   - Use a C compiler like `gcc` to compile the program:
     ```sh
     gcc pin_code_validation.c -o pin_code_validation
     ```

2. **Run the Program**:
   - Execute the compiled program:
     ```sh
     ./pin_code_validation
     ```

This implementation provides a simple yet effective PIN Code Validation System. It can be extended with additional features like reading valid PINs from a secure file, implementing more sophisticated security measures, or enhancing the user interface for better usability.
