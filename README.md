import tkinter as tk
from datetime import datetime

class Cliente:
    def __init__(self, nombre, apellido, fecha_nacimiento, domicilio):
        self.nombre = nombre
        self.apellido = apellido
        self.fecha_nacimiento = fecha_nacimiento
        self.domicilio = domicilio

    def __str__(self):
        return (f"Cliente: {self.nombre} {self.apellido}\n"
                f"Fecha de Nacimiento: {self.fecha_nacimiento}\n"
                f"Domicilio: {self.domicilio}")
class Movimiento:
    def __init__(self, descripcion, tipo, monto, saldo):
        self.fecha = datetime.now().strftime("%Y-%m-%d %H:%M:%S")
        self.descripcion = descripcion
        self.tipo = tipo  
        self.monto = monto
        self.saldo = saldo

    def __str__(self):
        return (f"{self.fecha} | {self.descripcion} | {self.tipo} | "
                f"${self.monto} | Saldo: ${self.saldo}")

class Cuenta:
    def __init__(self, numero_cuenta):
        self.numero_cuenta = numero_cuenta
        self.saldo = 1000  
        self.movimientos = []

    def agregar_movimiento(self, descripcion, tipo, monto):
        if tipo == 'abono':
            self.saldo += monto
        else:
            self.saldo -= monto
        movimiento = Movimiento(descripcion, tipo, monto, self.saldo)
        self.movimientos.append(movimiento)

    def obtener_estado(self):
        texto = f"Cuenta: {self.numero_cuenta}\nSaldo inicial: 1000\n\nMovimientos:\n"
        for mov in self.movimientos:
            texto += str(mov) + "\n"
        texto += f"\nSaldo final: ${self.saldo}"
        return texto

def generar_estado_cuenta():
    cliente = Cliente(
        entrynombre.get(),
        entryapellidopat.get(),
        entryapellidomat.get(),
        entryfecha.get(),
        entrydomicilio.get(),
        entrynum_cuenta.get()
    )
    cuenta = Cuenta(entrynum_cuenta.get())

    lista_movimientos = [
        ('Depósito inicial', 'abono', 1500),
        ('Compra supermercado', 'cargo', 500),
        ('Pago de servicios', 'cargo', 200),
    ]

    for desc, tipo, monto in lista_movimientos:
        cuenta.agregar_movimiento(desc, tipo, monto)

    texto = str(cliente) + "\n\n" + cuenta.obtener_estado()

    buttonresultado.delete("1.0", tk.END)
    buttonresultado.insert(tk.END, texto)

ventana = tk.Tk()
ventana.title("ESTADO DE CUENTA")
ventana.geometry("700x600")

tk.Label(ventana, text="Nombre").grid(row=0, column=0)
entrynombre = tk.Entry(ventana)
entrynombre.grid(row=0, column=1)

tk.Label(ventana, text="Apellido Paterno").grid(row=1, column=0)
entryapellidopat = tk.Entry(ventana)
entryapellidopat.grid(row=1, column=1)

tk.Label(ventana, text="Apellido Materno").grid(row=2, column=0)
entryapellidomat = tk.Entry(ventana)
entryapellidomat.grid(row=2, column=1)

tk.Label(ventana, text="Fecha de Nacimiento").grid(row=3, column=0)
entryfecha = tk.Entry(ventana)
entryfecha.grid(row=3, column=1)

tk.Label(ventana, text="Domicilio").grid(row=4, column=0)
entrydomicilio = tk.Entry(ventana)
entrydomicilio.grid(row=4, column=1)

tk.Label(ventana, text="Número de Cuenta").grid(row=5, column=0)
entrynum_cuenta = tk.Entry(ventana)
entrynum_cuenta.grid(row=5, column=1)

tk.Button(ventana, text="Generar Estado de Cuenta", command=generar_estado_cuenta).grid(row=7, column=0, columnspan=2, pady=10)

buttonresultado = tk.Text(ventana, height=15, width=70)
buttonresultado.grid(row=6, column=0, columnspan=2)

ventana.mainloop()
