---
layout: default
---

    /* Temperature Conversion Program
     * Author: Lucas Flanagan - 02/12/2021
     */

    #include "myhead.h"
    #include <stdio.h>
    #include <stdlib.h>
    #include <string.h>

    #define BANNER "|-----------Temperature Conversion-----------|\n"
    #define USAGE ("[USAGE]: ./(executable) (DegreesF or DegreesC)\n[USAGE]: Example: ./converter 10F        -- this returns the Celsius equivalent of 10 degrees Fahrenheit\n                  ./converter 55C        -- this returns the Fahrenheit equivalent of 55 degrees Celsius\n")
    #define ERROR (1)
    #define SUCCESS (0)
    #define TRUE (1)
    #define FALSE (0)

    /* The 'main' function does the following tasks.
     * It checks whether the correct number of command line arguments have been supplied. If an incorrect number of arguments are present, it calls the function 'print_usage' and returns 0.
     * If the number of command line arguments is correct, it calls the function 'validate_and_parse_input' and passes a string argument as a parameter.
     * It allocates storage for the temperature, scale, and result variables on the function's stack frame.
     * If the returned value of 'validate_and_parse_input' is equal to 'ERROR', it calls the function 'print_usage' and returns 0.
     * Otherwise, it passes the temperature and scale values to the function 'print_output' and returns the value 0.*/
    int main(int argc, char * argv[]) {
        printf(BANNER);
        if (argc != 2) {
            print_usage();
      return 0;
        }
        double temperature;
        char scale;
        int result = validate_and_parse_input(argv[1], &temperature, &scale);
        if (result == ERROR) {
      print_usage();
            return 0;	
        }
        if (scale == 'F') {
            print_output(fahrenheit_to_celsius(temperature), temperature, scale);
      return SUCCESS;
        } else if (scale == 'C') {
            print_output(temperature, celsius_to_fahrenheit(temperature), scale);
      return SUCCESS;
        } else {
            return ERROR;
        }
    }

    /* The function 'is_digit' checks whether the input character c is a decimal digit from 0 through 9.
     * It returns 1 if the value is one of these decimal digits, and 0 if it is not.  */
    int is_digit(char c) {
        if (c >= '0' && c <= '9') {
            return TRUE;
        }
        return FALSE;
    }

    /* The function 'is_floating_point_number' checks whether the input string is a valid floating point number. 
     * If the input string is valid, it returns 1. If it is invalid, the function returns 0.*/
    int is_floating_point_number(char * input) {
        int running = 1;
        int index = 1;
        int is_first_index_number = is_digit(input[0]);
        int decimal_count = 0;
        if (input[0] != '+' && input[0] != '-' && is_first_index_number == 0) {
            /* invalid */
      return FALSE;
        }
        while (running == 1) {
            if (is_digit(input[index]) == 0) {
          if (strlen(input) == 1 && is_first_index_number == 1) {
              return TRUE;
          }
          if (input[index] != '.') {
        /* invalid */
              return FALSE;
          }
          if (input[index] == '.') {
              ++decimal_count;
        if (decimal_count > 1) {
            /* more than one decimal is present */
            return FALSE;
        }
          }
      }
      if (input[index + 1] == '\0' || input[index + 1] == '\n') {
          running = 0;
      }
      ++index;
        }
        return TRUE;
    }

    /* The function 'is_integer' checks whether the input string is a valid integer. 
     * If the input string is valid, it returns 1. 
     * If it is invalid, the function returns 0. 
     * Valid integers may or may not begin with '+' or '-' symbols.*/
    int is_integer(char * input) {
        int running = TRUE;
        int index = 1;
        int is_first_index_number = is_digit(input[0]);
        if (input[0] != '+' && input[0] != '-' && is_first_index_number == 0) {
            /* invalid */
      return FALSE;
        }
        while (running == TRUE) {
            if (is_digit(input[index]) == FALSE) {
          /* invalid */
          return FALSE;
      }
      if (input[index + 1] == '\0' || input[index + 1] == '\n') {
          running = FALSE;
      }
      ++index;
        }
        return TRUE;
    }

    /* The function 'validate_and_parse_input' does the following.
     * It checks whether the last character in the string is one of the two allowable characters, 'C' or 'F'. 
     * It returns 0 if the value is allowable, and 1 if it is not. 
     * If allowable, the character value will be stored in the memory address associated with the scale parameter.
     * It replaces the last character of the input with a null character '\0'.
     * It checks whether the shortened input string represents a valid floating point number. 
     * If it does, the value is converted to a double and stored in the memory location associated with the temperature parameter. 
     * If the shortened input does not represent a valid floating point number, it is tested for validity as an integer. 
     * If it represents a valid integer, it will be converted to type integer and subsequently stored in the memory address associated with the temperature parameter.
     * It returns 0 if the function executes without error. */
    int validate_and_parse_input(char * input, double * temperature, char * scale) {
        char last = input[strlen(input) - 1];
        if (last == 'C') {
            *scale = input[strlen(input) - 1];
        } else if (last == 'F') {
            *scale = input[strlen(input) - 1];
        } else {
            /* invalid */
      return ERROR;
        }
        input[strlen(input) - 1] = '\0';
        if (is_floating_point_number(input) == TRUE && is_integer(input) == FALSE) {
            double new_float = strtod(input, NULL);
      * temperature = new_float; /* CHECK IF THIS STORES ON MAIN STACK PROPERLY */
      return SUCCESS;
        } else if (is_integer(input) == TRUE) {
            int new_integer = atoi(input);
      double new_double = (double) new_integer;
      * temperature = new_double;
      return SUCCESS;
        } else {
            return ERROR;
        }

    }

    /* The function 'celsius_to_fahrenheit' converts a temperature from Celsius to Fahrenheit.*/
    double celsius_to_fahrenheit(double celsius) {
        double fahrenheit = ((9.0 * celsius) / 5.0) + 32;
        return fahrenheit;
    }

    /* The function 'fahrenheit_to_celsius' converts a temperature from Fahrenheit to Celsius.*/
    double fahrenheit_to_celsius(double fahrenheit) {
        double celsius = (((fahrenheit - 32) * 5) / 9);
        return celsius;
    }

    /* The function 'print_usage' prints a message to the user containing instructions on how to use the program if they enter erroneous input. */
    void print_usage() {
        printf(USAGE);
        exit(EXIT_FAILURE);
    }

    /* The function 'print_output' prints information to the screen about the conversion.
     * If the scale is the character 'C', it prints the inputted value in Celsius first and the converted value in Fahrenheit second.
     * If the scale is the character 'F', it prints the inputted value in Fahrenheit first and the converted value in Celsius second.
     * If the scale is some other value, it prints an error for the developer.*/
    void print_output(double celsius, double fahrenheit, char scale) {
        if (scale == 'C') {
            printf("Celsius: %.2f = Fahrenheit: %.2f \n", celsius, fahrenheit);
        } else if (scale == 'F') {
            printf("Fahrenheit: %.2f = Celsius: %.2f \n", fahrenheit, celsius);
        } else {
            printf("[***] Internal Error. Invalid 'scale' at function print_output()\n");
        }
    }

