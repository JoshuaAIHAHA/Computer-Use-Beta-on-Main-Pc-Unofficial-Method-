# Computer-Use-Beta-on-Main-Pc-Unofficial-Method-
How to Run Anthropic's Computer Use Beta on Your Main Display (Unofficial Method)  WARNING! ⚠️  This guide describes an UNSUPPORTED and POTENTIALLY RISKY method for running Anthropic's Computer Use Beta on your main display and computer (tested with Ubuntu Linux).  Anthropic does not officially endorse this, and proceeding could result in:


How to Run Anthropic's Computer Use Beta on Your Main Display (Unofficial Method)

WARNING! ⚠️

This guide describes an UNSUPPORTED and POTENTIALLY RISKY method for running Anthropic's Computer Use Beta on your main display and computer (tested with Ubuntu Linux).  Anthropic does not officially endorse this, and proceeding could result in:

- System instability: Crashes, freezes, or unexpected behavior.
- Data corruption: Potential loss or damage to your files.
- Security vulnerabilities: Running the app with sudo grants elevated permissions (required to access the display), increasing risk if something goes wrong.
- Conflicts with other programs: Interference with existing software or system settings.
----- SERIOUSLY, BACK UP YOUR DATA FIRST!

If you encounter issues, you are responsible for troubleshooting and resolving them. This guide is provided "as-is" with no guarantees of success or safety.

Proceed with extreme caution and only if you are comfortable with the risks involved.



Clone the repository:
   git clone [https://github.com/anthropics/anthropic-quickstarts.git](https://github.com/anthropics/anthropic-quickstarts.git)
   cd anthropic-quickstarts/computer_use_demo
Set up a virtual environment:

Bash
python3 -m venv .venv
source .venv/bin/activate


Install the requirements:

Bash
pip install -r computer_use_demo/requirements.txt -r dev-requirements.txt


(Note: The requirements.txt file is located in the computer_use_demo subdirectory, while dev-requirements.txt is in the root directory. Make sure to specify the correct paths if your setup differs.)

Modify computer.py:

In the __init__ method of the ComputerTool class, change the self._display_prefix definition to:

Python
self._display_prefix = "DISPLAY=:0 "


This forces DISPLAY=:0 redirects output to your main screen instead of the virtual one the demo expects.

(Optional) Disable scaling:

If you encounter issues with screen resolution or scaling, you might need to disable scaling by changing _scaling_enabled = True to _scaling_enabled = False within the ComputerTool class in computer.py.

Modify streamlit.py:

Add the following lines at the beginning of the file:

Python
import sys
import os
sys.path.append(os.path.dirname(os.path.abspath(__file__)))


This ensures that Python can correctly resolve the relative imports in the streamlit.py file.

Set environment variables:

Make sure to set the necessary environment variables:
ANTHROPIC_API_KEY: Your Anthropic API key.
WIDTH and HEIGHT: Your screen resolution (e.g., WIDTH=1920, HEIGHT=1080 for 1080p).


You may also change system prompt but this is user based so there is no one size fits all prompt but I can provide mine or you can use AI to make you one since the default prompt is based on docker and virutal pc.

Read the read me now for running!

or use this at your own risk !

(if your to lazy for the read me here is the setup to run it now!)

# Navigate to the demo directory (Yours is different than mine!)
cd /home/josh/anthropic-quickstarts/computer-use-demo 

# Activate the virtual environment
source .venv/bin/activate 

# Set screen resolution (may need adjustment)
export WIDTH=1920
export HEIGHT=1080

# Set the display number (important for Xvfb)
export display=0 

# Start the virtual display server
Xvfb :0 -screen 0 1366x768x24 &

# Run the Streamlit app with sudo to access the display
sudo -E .venv/bin/python -m streamlit run computer_use_demo/streamlit.py 
