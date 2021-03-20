def text_input():
    return input('- Text: ')


def print_text():
    print("".join(text))


formatters = ["plain", "bold", "italic", "link", "inline-code", "header", "ordered-list", "unordered-list",
              "line-break"]

text = []

file = open('output.md', 'w')

while True:
    command = input('- Choose a formatter: ')
    if command == "!help":
        print(f'''Available formatters: {" ".join(formatters)}\n'''
              '''Special commands: !help !done''')

    elif command == "plain":

        text.append(f"{text_input()}")
        print_text()

    elif command == "bold":
        text.append(f"**{text_input()}**")
        print_text()

    elif command == "italic":
        text.append(f"*{text_input()}*")
        print_text()

    elif command == "link":
        label = input('- Label')
        link = input('- URL: ')
        text.append(f"[{label}]({link})")
        print_text()

    elif command == "inline-code":
        text.append(f"`{text_input()}`")
        print_text()

    elif command == "header":
        header_level = int(input("- Level: "))
        if 1 <= header_level <= 6:
            text.append(header_level * "#" + f" {text_input()}\n")
        text.append("")
        print_text()

    elif command == "ordered-list":
        while True:
            rows_num = int(input("- Number of rows: "))
            if rows_num <=0:
                print("The number of rows should be greater than zero")
            else:
                for i in range(1, rows_num + 1):
                    print(f"Row #{i}", end="")
                    text.append(f"{i}. {text_input()}\n")
                break
        print_text()

    elif command == "unordered-list":
        while True:
            rows_num = int(input("- Number of rows: "))
            if rows_num <= 0:
                print("The number of rows should be greater than zero")
            else:
                for i in range(1, rows_num + 1):
                    print(f"Row #{i}", end="")
                    text.append(f"* {text_input()}\n")
                break
        print_text()

    elif command == "line-break":
        text.append('\n')
        print_text()

    elif command == "!done":
        # file = open('result.md', 'w')
        file.writelines(text)
        file.close()
        break
    elif command == "new-line":
        text.append('\n')
        print_text()
    else:
        print('''
        Unknown formatting type or command. Please try again
        ''')

