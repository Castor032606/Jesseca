import tkinter as tk
from tkinter import scrolledtext

class ChatbotGUI:
    def __init__(self):
        self.window = tk.Tk()
        self.window.title("Chatbot")
        self.window.geometry("500x700")
        self.window.config(bg="#1e1e2f") 

        
        self.chat_area = scrolledtext.ScrolledText(self.window, wrap=tk.WORD, font=("Arial", 10))
        self.chat_area.config(state='disabled', bg="#2c2c3e", fg="white", insertbackground="white")
        self.chat_area.place(x=10, y=10, width=380, height=400)

        
        self.entry = tk.Entry(self.window, font=("Arial", 12), bg="#3a3a4f", fg="white", insertbackground="white")
        self.entry.place(x=10, y=420, width=300, height=50)

        
        self.send_button = tk.Button(self.window, text="Send", bg="#4CAF50", fg="white",
                                     font=("Arial", 12, "bold"), command=self.send_message)
        self.send_button.place(x=320, y=420, width=100, height=50)

        
        self.window.bind('<Return>', lambda event: self.send_message())

        self.bot_reply("Hi there! I'm your basic chatbot. Type 'quit' to exit.")

    def bot_reply(self, message):
        self.chat_area.config(state='normal')
        self.chat_area.insert(tk.END, "Chatbot: " + message + "\n")
        self.chat_area.config(state='disabled')
        self.chat_area.yview(tk.END)  

    def user_message(self, message):
        self.chat_area.config(state='normal')
        self.chat_area.insert(tk.END, "You: " + message + "\n")
        self.chat_area.config(state='disabled')
        self.chat_area.yview(tk.END)

    def send_message(self):
        user_input = self.entry.get().lower().strip()
        self.entry.delete(0, tk.END)

        if user_input == "":
            return

        self.user_message(user_input)

        
        if user_input == "quit":
            self.bot_reply("Goodbye! Have a great day!")
            self.window.after(1000, self.window.destroy)

        elif any(word in user_input for word in ["hi", "hello", "hey"]):
            self.bot_reply("Hello! Nice to talk to you!")

        elif any(word in user_input for word in ["how are you", "how r u"]):
            self.bot_reply("I'm doing well, thanks! How about you?")

        elif "name" in user_input:
            self.bot_reply("I'm your friendly basic chatbot!")

        elif any(word in user_input for word in ["bye", "goodbye"]):
            self.bot_reply("See you later! Take care!")

        else:
            self.bot_reply("Sorry, I don't understand that yet.")

    def run(self):
        self.window.mainloop()


if __name__ == "__main__":
    app = ChatbotGUI()
    app.run()
