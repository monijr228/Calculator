import tkinter as tk

def click(event):
    current = str(entry.get())
    entry.delete(0, tk.END)
    entry.insert(0, current + str(event.widget["text"]))

def clear():
    entry.delete(0, tk.END)

def delete_last():
    current = entry.get()
    entry.delete(0, tk.END)
    entry.insert(0, current[:-1])

def calculate():
    try:
        result = eval(entry.get())
        entry.delete(0, tk.END)
        entry.insert(0, str(result))
    except Exception:
        entry.delete(0, tk.END)
        entry.insert(0, "Error")

# Create main window
root = tk.Tk()
root.title("Simple Calculator")
root.geometry("300x420")

# Entry field
entry = tk.Entry(root, font=("Arial", 20), borderwidth=2, relief="groove", justify='right')
entry.pack(fill=tk.BOTH, ipadx=8, ipady=15, pady=10, padx=10)

# Button layout (including Delete)
buttons = [
    ['7', '8', '9', '/'],
    ['4', '5', '6', '*'],
    ['1', '2', '3', '-'],
    ['0', '.', '=', '+'],
    ['C', 'DEL']
]

# Create buttons
for row in buttons:
    frame = tk.Frame(root)
    frame.pack(expand=True, fill="both")
    for char in row:
        btn = tk.Button(frame, text=char, font=("Time New Roman", 18), height=2, width=5)
        btn.pack(side=tk.LEFT, expand=True, fill="both")

        if char == '=':
            btn.config(command=calculate)
        elif char == 'C':
            btn.config(command=clear)
        elif char == 'DEL':
            btn.config(command=delete_last)
        else:
            btn.bind("<Button-1>", click)

root.mainloop()
