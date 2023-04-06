import os
from collections import defaultdict
import tkinter as tk
from tkinter import filedialog

def find_files_to_delete(folder_path):
    size_to_files = defaultdict(list)

    for root, _, files in os.walk(folder_path):
        for file in files:
            file_path = os.path.join(root, file)
            file_size = os.path.getsize(file_path)
            size_to_files[file_size].append(file_path)

    files_to_delete = []
    for file_paths in size_to_files.values():
        if len(file_paths) > 1:
            files_to_delete.extend(file_paths[:-1])

    return files_to_delete

def browse_folder():
    folder_path = filedialog.askdirectory()
    folder_path_entry.delete(0, tk.END)
    folder_path_entry.insert(0, folder_path)

def find_files():
    folder_path = folder_path_entry.get()
    files_list.delete(0, tk.END)
    
    files_to_delete = find_files_to_delete(folder_path)

    for file in files_to_delete:
        files_list.insert(tk.END, file)

    delete_files_button.config(state=tk.NORMAL)
    num_files_label.config(text=f'Number of files to delete: {len(files_to_delete)}')

def delete_files():
    for i in range(files_list.size()):
        file_path = files_list.get(i)
        os.remove(file_path)

    find_files()

app = tk.Tk()
app.title('Duplicate Files Remover')

folder_path_label = tk.Label(app, text='Folder Path:')
folder_path_label.grid(row=0, column=0, padx=5, pady=5, sticky=tk.W)

folder_path_entry = tk.Entry(app, width=50)
folder_path_entry.grid(row=0, column=1, padx=5, pady=5)

browse_button = tk.Button(app, text='Browse', command=browse_folder)
browse_button.grid(row=0, column=2, padx=5, pady=5)

find_files_button = tk.Button(app, text='Find Files', command=find_files)
find_files_button.grid(row=1, column=0, padx=5, pady=5, columnspan=3)

scrollbar = tk.Scrollbar(app)
scrollbar.grid(row=2, column=2, rowspan=2, padx=5, pady=5, sticky=tk.N+tk.S)

files_list = tk.Listbox(app, width=80, height=20, yscrollcommand=scrollbar.set)
files_list.grid(row=2, column=0, padx=5, pady=5, columnspan=2, rowspan=2)

scrollbar.config(command=files_list.yview)

delete_files_button = tk.Button(app, text='Delete Files', command=delete_files, state=tk.DISABLED)
delete_files_button.grid(row=4, column=0, padx=5, pady=5)

num_files_label = tk.Label(app, text='Number of files to delete: 0')
num_files_label.grid(row=4, column=1, padx=5, pady=5, sticky=tk.W)

app.mainloop()
