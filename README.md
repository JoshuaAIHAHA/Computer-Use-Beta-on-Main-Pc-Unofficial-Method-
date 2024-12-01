# Ubuntu Linux: How to Run Anthropic's Computer Use Beta on Your Main Display (Unofficial Method)

## WARNING! ⚠️

This guide describes an **UNSUPPORTED and POTENTIALLY RISKY** method for running Anthropic's Computer Use Beta on your main display and computer (tested with Ubuntu Linux). **Anthropic does not officially endorse this**, and proceeding could result in:

- **System instability**: Crashes, freezes, or unexpected behavior.
- **Data corruption**: Potential loss or damage to your files.
- **Security vulnerabilities**: Running the app with `sudo` grants elevated permissions (required to access the display), increasing risk if something goes wrong.
- **Conflicts with other programs**: Interference with existing software or system settings.

---

**SERIOUSLY, BACK UP YOUR DATA FIRST!**

If you encounter issues, you are responsible for troubleshooting and resolving them. This guide is provided "as-is" with no guarantees of success or safety.

If you need help though, feel free to ask!

Proceed with extreme caution and only if you are comfortable with the risks involved.

---

## Setup

1. **Clone the repository:**

   ```bash
   git clone https://github.com/anthropics/anthropic-quickstarts.git
   ```

2. **Navigate to the download directory:**

   ```bash
   cd anthropic-quickstarts/computer_use_demo
   ```

3. **Set up a virtual environment:**

   ```bash
   python3 -m venv .venv
   ```

4. **Activate the virtual environment:**

   ```bash
   source .venv/bin/activate
   ```

5. **Install the requirements:**

   ```bash
   pip install -r computer_use_demo/requirements.txt -r dev-requirements.txt
   ```

   > **Note:** The `requirements.txt` file is located in the `computer_use_demo` subdirectory, while `dev-requirements.txt` is in the root directory. Make sure to specify the correct paths if your setup differs.

6. **Modify `computer.py`:**

   - **Locate `computer.py` in the `tools` subfolder:**

     ```
     anthropic-quickstarts/computer_use_demo/computer_use_demo/tools/computer.py
     ```

   - **Edit the `__init__` method of the `ComputerTool` class. Change the `self._display_prefix` definition to:**

     ```python
     self._display_prefix = "DISPLAY=:0 "
     ```

     This forces `DISPLAY=:0` to redirect output to your main screen instead of the virtual one the demo expects.

7. **Modify `streamlit.py`:**

   - **Locate `streamlit.py` in the `computer_use_demo` directory:**

     ```
     anthropic-quickstarts/computer_use_demo/computer_use_demo/streamlit.py
     ```

   - **Add the following lines at the very beginning of the file:**

     ```python
     import sys
     import os
     sys.path.append(os.path.dirname(os.path.abspath(__file__)))
     ```

     This ensures that Python can correctly resolve the relative imports in the `streamlit.py` file.

8. **Set environment variables:**

   - **Set the necessary environment variables:**

     - `ANTHROPIC_API_KEY`: Your Anthropic API key.
     - `WIDTH` and `HEIGHT`: Your screen resolution (e.g., `WIDTH=1920`, `HEIGHT=1080` for 1080p).

     ```bash
     export ANTHROPIC_API_KEY=your_api_key_here
     export WIDTH=1920
     export HEIGHT=1080
     ```

---

**Use this at your own risk!**

---

## Running

1. **Navigate to the demo directory:**

   ```bash
   cd /home/yourusername/anthropic-quickstarts/computer_use_demo
   ```

2. **Activate the virtual environment:**

   ```bash
   source .venv/bin/activate
   ```

3. **Set screen resolution (may need adjustment):**

   ```bash
   export WIDTH=1920
   export HEIGHT=1080
   ```

4. **Set the display number (important for Xvfb):**

   ```bash
   export DISPLAY=:0
   ```

5. **Start the virtual display server:**

   ```bash
   Xvfb :0 -screen 0 1920x1080x24 &
   ```

   > **Note:** Adjust `1920x1080x24` to match your screen resolution and color depth.

6. **Run the Streamlit app with `sudo` to access the display:**

   ```bash
   sudo -E .venv/bin/python -m streamlit run computer_use_demo/streamlit.py
   ```

   The `-E` flag preserves the environment variables, which is necessary when using `sudo`.

---

You're done! Have fun and be safe!

---

**Note:** You may also change the system prompt, but this is user-based, so there is no one-size-fits-all prompt. You can create a custom prompt yourself or use AI to generate one, especially since the default prompt is based on Docker and a virtual PC.
