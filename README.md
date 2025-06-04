# Python-GUI-ATM
ATM Class (Backend Logic):
How to Run This Code:

Save the code as a Python file (e.g., atm_gui.py).
Open a terminal or command prompt.
Navigate to the directory where you saved the file.
Run the command: python atm_gui.py
Key Features and Explanations:

ATM Class (Backend Logic):

Separates the core ATM functionalities (account management, transactions) from the GUI.
accounts dictionary: Simple in-memory storage for accounts. In a real application, this would interact with a database.
validate_pin, get_balance, withdraw, deposit, get_transaction_history, logout: These methods encapsulate the business logic.
pin_attempts: Basic security to lock out after too many incorrect PINs.
ATM_GUI Class (Tkinter GUI):

__init__(self, master):
Sets up the main window (master).
Initializes self.atm_backend to access the ATM logic.
self.current_input: A tk.StringVar to display the numbers entered on the keypad.
self.screen_message: A tk.StringVar to display dynamic messages to the user on the main screen.
self.current_state: A crucial part of a state machine to manage the ATM's flow (e.g., "ACCOUNT_ENTRY", "PIN_ENTRY", "MAIN_MENU", "WITHDRAW_AMOUNT"). This helps in processing ENTER differently based on context.
setup_ui(self):
Organizes the GUI using tk.Frame widgets for better structure.
Screen Area: Uses tk.Label for messages and input display. wraplength helps the text wrap within the label.
Side Action Buttons: tk.Button widgets are created dynamically. command=lambda is used to pass arguments to the handler function. Initially, these are disabled until login.
Keypad Area: Buttons for 0-9, CLEAR, ENTER, and CANCEL are created using tk.Button and arranged with grid.
append_input(self, digit): Appends digits to current_input. Crucially, it masks the PIN entry with * while storing the actual digits in self.actual_pin_input.
clear_input(self): Resets the input field.
process_input(self): This is the heart of the interaction. It uses self.current_state to determine what to do when "ENTER" is pressed:
If ACCOUNT_ENTRY, it prompts for PIN.
If PIN_ENTRY, it attempts to validate the PIN.
If WITHDRAW_AMOUNT or DEPOSIT_AMOUNT, it processes the transaction.
display_main_menu(self): Shows the options available after successful login.
handle_side_action(self, action): Called when a side button is pressed, initiating actions like balance inquiry, withdrawal, or deposit.
confirm_cancel(self): Uses messagebox.askyesno for the "Confirm if you want to cancel" dialog from your image.
reset_atm(self): Logs out the user and returns the ATM to its initial state.
enable_action_buttons() and disable_action_buttons(): Control the state of the side buttons based on login status.
Further Enhancements (Beyond this initial code):

Database Integration: Replace the self.accounts dictionary with a connection to an SQLite database (built-in, good for local apps) or a more robust one like PostgreSQL.
Security:
Hash PINs (never store plain text PINs!).
Implement more sophisticated lockout mechanisms.
Secure storage of account data.
Error Handling: More robust try-except blocks.
Transaction Limits: Daily withdrawal limits, etc.
User Experience (UX):
Animation for "cash dispensing."
Sound effects.
Better visual feedback for errors/success.
Object-Oriented Design: Create separate Account and Transaction classes to manage data more cleanly.
More Advanced GUI: Use ttk (Themed Tkinter) for a more modern look.
