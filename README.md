import math
#Store last 3 results
prev_results = [None, None, None]

def update_results(new_result):
    """ Update the last 3 results, keeping the most recent one at index 0 """
    prev_results.insert(0, new_result)
    if len(prev_results) > 3:
        prev_results.pop()

def get_number(prompt, use_prev=True):
    """ Get a number from user, allowing use of last 3 results """
    while True:
        num = input(prompt)
        if use_prev:
            if num.lower() == "prev1" and prev_results[0] is not None:
                return prev_results[0]
            elif num.lower() == "prev2" and prev_results[1] is not None:
                return prev_results[1]
            elif num.lower() == "prev3" and prev_results[2] is not None:
                return prev_results[2]
        try:
            return float(num)
        except ValueError:
            print("Invalid input. Enter a number or 'prev1', 'prev2', 'prev3' if available.")

def basic_operations():
    print("\nBasic Operations:")
    num1 = get_number("Enter first number (or 'prev1', 'prev2', 'prev3'): ")
    op = input("Enter operator (+, -, *, /): ")
    num2 = get_number("Enter second number: ")

    if op == '+':
        return num1 + num2
    elif op == '-':
        return num1 - num2
    elif op == '*':
        return num1 * num2
    elif op == '/':
        return num1 / num2 if num2 != 0 else "Undefined (division by zero)"
    else:
        return "Invalid operator"

def square_root():
    num = get_number("Enter number (or 'prev1', 'prev2', 'prev3'): ")
    return math.sqrt(num) if num >= 0 else "Undefined (negative square root)"

def power():
    base = get_number("Enter base number (or 'prev1', 'prev2', 'prev3'): ")
    exponent = get_number("Enter exponent: ")
    return math.pow(base, exponent)

def logarithm():
    num = get_number("Enter number (or 'prev1', 'prev2', 'prev3'): ")
    base = input("Enter base (leave empty for natural log): ")
    if base:
        return math.log(num, float(base)) if num > 0 else "Undefined (log of non-positive number)"
    return math.log(num) if num > 0 else "Undefined (log of non-positive number)"

def factorial():
    num = get_number("Enter number (or 'prev1', 'prev2', 'prev3'): ")
    return math.factorial(int(num)) if num >= 0 and num.is_integer() else "Undefined (factorial of non-integer or negative number)"

def trigonometric():
    print("Choose function: 1. sin  2. cos  3. tan")
    trig_choice = input("Enter choice: ")
    angle = get_number("Enter angle in degrees (or 'prev1', 'prev2', 'prev3'): ")
    radians = math.radians(angle)

    if trig_choice == "1":
        return math.sin(radians)
    elif trig_choice == "2":
        return math.cos(radians)
    elif trig_choice == "3":
        return "Undefined (tan 90° or 270°)" if angle % 180 == 90 else math.tan(radians)
    else:
        return "Invalid choice"

def unit_conversion():
    print("\nUnit Conversions:")
    print("1. Weight (kg <-> lb)")
    print("2. Length (m <-> ft)")
    print("3. Time (seconds <-> minutes)")
    print("4. Distance (km <-> miles)")

    choice = input("Enter choice: ")

    if choice == "1":
        value = get_number("Enter weight (or 'prev1', 'prev2', 'prev3'): ")
        unit = input("Enter unit (kg/lb): ").lower()
        return f"{value * 2.20462} lb" if unit == "kg" else f"{value / 2.20462} kg"

    elif choice == "2":
        value = get_number("Enter length (or 'prev1', 'prev2', 'prev3'): ")
        unit = input("Enter unit (m/ft): ").lower()
        return f"{value * 3.28084} ft" if unit == "m" else f"{value / 3.28084} m"

    elif choice == "3":
        value = get_number("Enter time (or 'prev1', 'prev2', 'prev3'): ")
        unit = input("Enter unit (s/min): ").lower()
        return f"{value / 60} min" if unit == "s" else f"{value * 60} s"

    elif choice == "4":
        value = get_number("Enter distance (or 'prev1', 'prev2', 'prev3'): ")
        unit = input("Enter unit (km/mi): ").lower()
        return f"{value * 0.621371} mi" if unit == "km" else f"{value / 0.621371} km"

    else:
        return "Invalid choice"

def view_last_results():
    """ Displays the last 3 results """
    print("\nLast 3 Results:")
    for i, result in enumerate(prev_results):
        if result is not None:
            print(f"{i+1}. {result}")
        else:
            print(f"{i+1}. No result yet.")

while True:
    print("\nAdvanced Calculator")
    print("1. Basic Operations")
    print("2. Square Root")
    print("3. Power (x^y)")
    print("4. Logarithm")
    print("5. Factorial")
    print("6. Trigonometric Functions")
    print("7. Unit Conversions")
    print("8. View Last 3 Results")
    print("9. Exit")

    choice = input("Enter your choice: ")

    if choice == "1":
        result = basic_operations()
    elif choice == "2":
        result = square_root()
    elif choice == "3":
        result = power()
    elif choice == "4":
        result = logarithm()
    elif choice == "5":
        result = factorial()
    elif choice == "6":
        result = trigonometric()
    elif choice == "7":
        result = unit_conversion()
    elif choice == "8":
        view_last_results()
        continue  # Go back to menu without storing a result
    elif choice == "9":
        print("Exiting calculator.")
        break
    else:
        print("Invalid choice, try again.")
        continue

    update_results(result)
    print(f"Result: {result}")
