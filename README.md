from kivy.app import App
from kivy.uix.button import Button
from kivy.uix.label import Label
from kivy.uix.boxlayout import BoxLayout
import cv2
import tkinter as tk
from tkinter import ttk

class CameraApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Camera Measurement App")

        self.cap = cv2.VideoCapture(0)

        self.label = ttk.Label(root, text="Measure objects using your camera")
        self.label.pack(pady=10)

        self.width_button = ttk.Button(root, text="Measure Width", command=self.measure_width)
        self.width_button.pack(pady=5)

        self.height_button = ttk.Button(root, text="Measure Height", command=self.measure_height)
        self.height_button.pack(pady=5)

        self.result_label = ttk.Label(root, text="")
        self.result_label.pack(pady=10)

        self.quit_button = ttk.Button(root, text="Quit", command=self.quit)
        self.quit_button.pack(pady=10)

    def measure_width(self):
        ret, frame = self.cap.read()
        cv2.imshow("Frame", frame)
        width = cv2.waitKey(0)
        print(f"Width: {width} pixels")
        self.show_result(f"Width: {width} pixels")

    def measure_height(self):
        ret, frame = self.cap.read()
        cv2.imshow("Frame", frame)
        height = cv2.waitKey(0)
        print(f"Height: {height} pixels")
        self.show_result(f"Height: {height} pixels")

    def show_result(self, result_text):
        self.result_label.config(text=result_text)

    def quit(self):
        self.cap.release()
        cv2.destroyAllWindows()
        self.root.destroy()

if __name__ == "__main__":
    root = tk.Tk()
    app = CameraApp(root)
    root.mainloop()

if __name__ == '__main__':
    CameraApp().run()
