import tkinter as tk
from tkinter import messagebox
import random

# --- 1. Логика программы (Функция-обработчик) ---
def generate_number():
    """
    Эта функция вызывается при нажатии кнопки.
    Она получает данные, проверяет их, генерирует число и выводит результат.
    """
    # Получаем текст из полей ввода
    min_text = entry_min.get()
    max_text = entry_max.get()

    try:
        # 1. Преобразуем ввод в целые числа
        min_value = int(min_text)
        max_value = int(max_text)

        # 2. Проверка логики: минимум не должен быть больше максимума
        if min_value > max_value:
            # Меняем значения местами и информируем пользователя
            min_value, max_value = max_value, min_value
            messagebox.showinfo("Исправлено", "Минимум был больше максимума. Значения поменяны местами.")
        
        # 3. Генерация случайного числа в диапазоне [min_value, max_value]
        random_number = random.randint(min_value, max_value)
        
        # 4. Обновление интерфейса с результатом
        result_label.config(text=f"Случайное число: {random_number}", fg="green")

    except ValueError:
        # Этот блок выполняется, если int() не смог преобразовать текст в число
        result_label.config(text="Ошибка: введите целые числа", fg="red")


# --- 2. Создание графического интерфейса ---
window = tk.Tk()
window.title("Генератор случайных чисел")
window.geometry("400x250")
window.resizable(False, False)
window.configure(bg="#f0f0f0") # Светло-серый фон для красоты

# --- Блок ввода данных (Фрейм) ---
frame_input = tk.Frame(window, bg="#f0f0f0")
frame_input.pack(pady=20)

# Метка и поле для "Минимум"
tk.Label(frame_input, text="Минимум:", bg="#f0f0f0", font=("Arial", 12)).grid(row=0, column=0, padx=10)
entry_min = tk.Entry(frame_input, width=15, font=("Arial", 12))
entry_min.grid(row=0, column=1, padx=10)
entry_min.insert(0, "1") # Значение по умолчанию

# Метка и поле для "Максимум"
tk.Label(frame_input, text="Максимум:", bg="#f0f0f0", font=("Arial", 12)).grid(row=1, column=0, pady=10)
entry_max = tk.Entry(frame_input, width=15, font=("Arial", 12))
entry_max.grid(row=1, column=1, pady=10)
entry_max.insert(0, "100") # Значение по умолчанию

# --- Кнопка запуска ---
btn_generate = tk.Button(
    window,
    text="Сгенерировать",
    command=generate_number,
    bg="#4CAF50", fg="white",
    font=("Arial", 12),
    width=20,
    height=2
)
btn_generate.pack(pady=25)

# --- Поле вывода результата ---
result_label = tk.Label(
    window,
    text="Результат появится здесь",
    font=("Arial", 14, "bold"),
    bg="#f0f0f0",
    fg="black"
)
result_label.pack(pady=15)


# --- 3. Запуск приложения ---
window.mainloop()
