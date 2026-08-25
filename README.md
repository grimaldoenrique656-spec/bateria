import tkinter as tk
from tkinter import messagebox

def verificar_bateria():
    try:
        voltaje = float(entry_voltaje.get())
        porcentaje = -1

        # Asignar porcentaje según voltaje
        if voltaje >= 12.7:
            porcentaje = 100
        elif voltaje >= 12.2:
            porcentaje = 50
        elif voltaje >= 12.0:
            porcentaje = 20
        elif voltaje <= 10.5:
            porcentaje = 0

        # Mostrar resultados
        if porcentaje == -1:
            lbl_resultado.config(text="⚠️ Voltaje fuera de rango.")
            lbl_generador.config(text="")
        else:
            lbl_resultado.config(text=f"Nivel de batería: {porcentaje}%")
            if porcentaje <= 20:
                lbl_generador.config(text="🔋 La batería está baja. Se recomienda encender el generador.")
            else:
                lbl_generador.config(text="✅ La batería tiene suficiente carga.")
    except ValueError:
        messagebox.showerror("Error", "Ingrese un valor numérico válido.")

def encender_generador():
    lbl_generador.config(text="🚀 Generador encendido. Recargando batería...")

def no_encender_generador():
    lbl_generador.config(text="🛑 Generador apagado. La batería sigue con su nivel actual.")

# Crear ventana principal
ventana = tk.Tk()
ventana.title("Verificador de Batería")
ventana.geometry("450x250")

# Etiqueta y entrada de voltaje
lbl_voltaje = tk.Label(ventana, text="Ingrese voltaje de la batería (V):")
lbl_voltaje.pack(pady=5)

entry_voltaje = tk.Entry(ventana)
entry_voltaje.pack(pady=5)

# Botón para verificar
btn_verificar = tk.Button(ventana, text="Verificar", command=verificar_bateria)
btn_verificar.pack(pady=10)

# Botones para encender/no encender generador
frame_botones = tk.Frame(ventana)
frame_botones.pack(pady=10)

btn_encender = tk.Button(frame_botones, text="Encender Generador", command=encender_generador)
btn_encender.grid(row=0, column=0, padx=10)

btn_no_encender = tk.Button(frame_botones, text="No Encender Generador", command=no_encender_generador)
btn_no_encender.grid(row=0, column=1, padx=10)

# Etiquetas de resultados
lbl_resultado = tk.Label(ventana, text="", font=("Arial", 12))
lbl_resultado.pack(pady=5)

lbl_generador = tk.Label(ventana, text="", font=("Arial", 12))
lbl_generador.pack(pady=5)

# Ejecutar ventana
ventana.mainloop()

