# Tkinter-text-accuracy-calculator.
Text widget where the user can enter text. It calculates the accuracy of the entered text compared to a target text by highlighting correct and incorrect words and printing the accuracy percentage when the space key is pressed.

```python
import tkinter as tk


def calculate_accuracy():
    input_text = input_text_widget.get("1.0", "end-1c")  # Get the entered text
    target_text = "The quick brown fox jumps over the lazy dog"

    input_words = input_text.split()
    target_words = target_text.split()

    for word_index, word in enumerate(input_words):
        if word_index >= len(target_words):
            break

        if word == target_words[word_index]:
            input_text_widget.tag_add("correct",
                                      f"1.{len(' '.join(input_words[:word_index]))}",
                                      f"1.{len(' '.join(input_words[:word_index])) + len(word)}")
        else:
            input_text_widget.tag_add("incorrect",
                                      f"1.{len(' '.join(input_words[:word_index]))}",
                                      f"1.{len(' '.join(input_words[:word_index])) + len(word)}")

    accuracy = sum(
        1 for i, j in zip(input_words, target_words) if i == j) / len(
        target_words) * 100
    print(f"Accuracy: {accuracy}%")


root = tk.Tk()

# Create a Text widget
input_text_widget = tk.Text(root, height=1, width=50)
input_text_widget.pack()

# Configure tags for formatting
input_text_widget.tag_configure("correct", foreground="black")
input_text_widget.tag_configure("incorrect", foreground="red")

# Bind the space key to trigger accuracy calculation
input_text_widget.bind("<space>", lambda event: calculate_accuracy())

root.mainloop()
```
