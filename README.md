
import tkinter as tk
from tkinter import messagebox

class حلويات:
    def __init__(self):
        self.products = {}

        self.window = tk.Tk()
        self.window.title("برنامج حلويات")

        self.notebook = tk.ttk.Notebook(self.window)
        self.notebook.pack(pady=10, expand=True)

        self.frame1 = tk.Frame(self.notebook)
        self.frame2 = tk.Frame(self.notebook)

        self.notebook.add(self.frame1, text="إضافة/تعديل/عرض")
        self.notebook.add(self.frame2, text="تقارير")

        # شاشة 1
        self.add_product_frame()
        self.edit_product_frame()
        self.display_product_frame()

        # شاشة 2
        self.reports_frame()

    def add_product_frame(self):
        frame = tk.Frame(self.frame1)
        frame.pack(pady=10)

        tk.Label(frame, text="اسم المنتج").pack()
        self.product_name = tk.Entry(frame)
        self.product_name.pack()

        tk.Label(frame, text="سعر المنتج").pack()
        self.product_price = tk.Entry(frame)
        self.product_price.pack()

        tk.Button(frame, text="إضافة منتج", command=self.add_product).pack()

    def edit_product_frame(self):
        frame = tk.Frame(self.frame1)
        frame.pack(pady=10)

        tk.Label(frame, text="اسم المنتج").pack()
        self.edit_product_name = tk.Entry(frame)
        self.edit_product_name.pack()

        tk.Label(frame, text="سعر المنتج الجديد").pack()
        self.edit_product_price = tk.Entry(frame)
        self.edit_product_price.pack()

        tk.Button(frame, text="تعديل منتج", command=self.edit_product).pack()

    def display_product_frame(self):
        frame = tk.Frame(self.frame1)
        frame.pack(pady=10)

        tk.Label(frame, text="اسم المنتج").pack()
        self.display_name = tk.Entry(frame)
        self.display_name.pack()

        tk.Button(frame, text="عرض منتج", command=self.display_product).pack()
        self.display_label = tk.Label(frame, text="")
        self.display_label.pack()

    def add_product(self):
        name = self.product_name.get()
        price = self.product_price.get()
        self.products[name] = price
        messagebox.showinfo("تم", "تم إضافة المنتج")

    def edit_product(self):
        name = self.edit_product_name.get()
        price = self.edit_product_price.get()
        if name in self.products:
            self.products[name] = price
            messagebox.showinfo("تم", "تم تعديل المنتج")
        else:
            messagebox.showerror("خطأ", "المنتج غير موجود")

    def display_product(self):
        name = self.display_name.get()
        if name in self.products:
            self.display_label.config(text=f"السعر: {self.products[name]}")
        else:
            messagebox.showerror("خطأ", "المنتج غير موجود")

    def reports_frame(self):
        frame = tk.Frame(self.frame2)
        frame.pack(pady=10)

        tk.Button(frame, text="تقرير المنتجات", command=self.report_products).pack()
        self.report_text = tk.Text(frame, height=10, width=40)
        self.report_text.pack()

        tk.Label(frame, text="ملاحظات").pack()
        self.notes = tk.Text(frame, height=5, width=40)
        self.notes.pack()

    def report_products(self):
        report = ""
        for name, price in self.products.items():
            report += f"{name}: {price}\n"
        self.report_text.delete(1.0, tk.END)
        self.report_text.insert(tk.END, report)

    def run(self):
        self.window.mainloop()

if __name__ == "__main__":
    app = حلويات()
    app.run()
