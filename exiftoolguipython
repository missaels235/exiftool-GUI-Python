import tkinter as tk
from tkinter import filedialog
import subprocess

class ExifToolGUI:
    def __init__(self, root):
        self.root = root
        self.root.title("ExifTool GUI v1")

        # Matriz de botones
        buttons_frame = tk.Frame(root)
        buttons_frame.pack(pady=10)

        # Botón para seleccionar archivos
        self.select_button = tk.Button(buttons_frame, text="Seleccionar Archivos", command=self.select_files)
        self.select_button.pack(side=tk.LEFT, padx=5, pady=10)

        # Botón para ejecutar ExifTool
        self.run_button = tk.Button(buttons_frame, text="Ejecutar ExifTool", command=self.run_exiftool)
        self.run_button.pack(side=tk.LEFT, padx=5, pady=10)

        # Botón para limpiar la consola
        self.clear_button = tk.Button(buttons_frame, text="Limpiar Consola", command=self.clear_console)
        self.clear_button.pack(side=tk.LEFT, padx=5, pady=10)

        # Botón para mostrar créditos
        self.credits_button = tk.Button(buttons_frame, text="Créditos", command=self.show_credits)
        self.credits_button.pack(side=tk.LEFT, padx=5, pady=10)

        # Consola para mostrar la salida de ExifTool
        self.console = tk.Text(root, height=10, width=50)
        self.console.pack(pady=10)

        # Lista de archivos seleccionados
        self.selected_files = []

        # Vincular evento de cambio de tamaño de la ventana principal
        self.root.bind("<Configure>", self.adjust_console_size)

    def select_files(self):
        # Abre el cuadro de diálogo para seleccionar archivos
        self.selected_files = filedialog.askopenfilenames(title="Seleccionar archivos", filetypes=[("Archivos", "*.*")])

        # Muestra los archivos seleccionados en la consola
        self.console.insert(tk.END, "Archivos seleccionados:\n")
        for file_path in self.selected_files:
            self.console.insert(tk.END, f"{file_path}\n")

    def run_exiftool(self):
        if not self.selected_files:
            self.console.insert(tk.END, "No se han seleccionado archivos.\n")
            return

        # Ejecuta ExifTool en la terminal
        command = ["exiftool"] + list(self.selected_files)
        try:
            output = subprocess.check_output(command, stderr=subprocess.STDOUT, text=True)
            self.console.insert(tk.END, "\nSalida de ExifTool:\n")
            self.console.insert(tk.END, output)
            # Ajusta la vista al final del texto
            self.console.see(tk.END)
        except subprocess.CalledProcessError as e:
            self.console.insert(tk.END, f"\nError al ejecutar ExifTool: {e.output}\n")

    def clear_console(self):
        # Borra el contenido de la consola
        self.console.delete("1.0", tk.END)

    def show_credits(self):
        # Muestra los créditos en la consola en cursiva
        self.console.insert(tk.END, "\nCréditos:\n")
        self.console.insert(tk.END, "by Missael S")

    def adjust_console_size(self, event):
        # Ajusta el tamaño de la consola en función del tamaño de la ventana principal
        console_width = self.root.winfo_width() - 20  # Ajuste para el relleno
        console_height = self.root.winfo_height() - 150  # Ajuste para otros elementos
        self.console.config(width=console_width, height=console_height)

if __name__ == "__main__":
    root = tk.Tk()
    app = ExifToolGUI(root)
    root.mainloop()
