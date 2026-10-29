\# Every New Project

 1\. Create project folder and cd into it  
**mkdir \~/Projects/myproject && cd \~/Projects/myproject**

 2\. Create the venv (name it .venv — the dot keeps it out of the way)  
**python3 \-m venv .venv**

 3\. Activate it  
**source .venv/bin/activate**

 4\. Upgrade pip inside the venv  
**python \-m pip install \--upgrade pip**

 5\. Install your dependencies (whatever you need)  
**pip install matplotlib numpy**    

 6\. (Optional) Save them for reproducibility  
**pip freeze \> requirements.txt**

 7\. Create .gitignore so you never commit the venv  
**echo ".venv/" \> .gitignore**

 8\. Open your script in Kate  
**kate myscript.py**   

\#\# When you come back to the project later (new terminal session):  
**cd \~/Projects/myproject**  
**source .venv/bin/activate**  
**python myscript.py**   

\#\# When you're done for the session:  
**deactivate**   

## w

## h

## a

## t

\# Quick sanity checks

| Symptom | Cause |
| :---- | :---- |
| No (.venv) in prompt | You forgot to activate |
| ModuleNotFoundError | Package not installed in *this* venv |
| externally-managed-environment | You're not in a venv (system pip) |

## \#\# Optional: consider uv

It's a single binary that replaces python3 \-m venv \+ pip and is dramatically faster. If you want to try it:

1\.  Install once  
**curl \-LsSf https\://astral.sh/uv/install.sh \| sh**

2\. Then per project(creates venv  ):  
**uv venv .venv**            
**uv pip install matplotlib**    installs into it (no activate needed)  
**uv run python myscript.py**    runs with the right env   

But the plain venv workflow above works perfectly fine and is what most people use. The key habit is: create → activate → install → run, every time, in the project folder.

## \#\# What You're Seeing

| Traceback (most recent call last):   File "/home/daniel/Downloads/SigNiodVenV/SigmoidPlot.py", line 2, in \<module\>     import matplotlib.pyplot as plt ModuleNotFoundError: No module named 'matplotlib'     |
| :---- |

That block is called a traceback. Python prints it whenever your script crashes. Read it bottom-up:

| Line | Meaning |
| :---- | :---- |
| Traceback (most recent call last): | "Something went wrong, here's the chain of events." |
| File "...", line 2, in \<module\> | Where it broke — your file, line 2, top-level code. |
| import matplotlib.pyplot as plt | What it was doing when it broke. |
| ModuleNotFoundError: No module named 'matplotlib' | The actual error — Python can't find that package in the current environment. |

## What To Do (the pattern)

Every time you see this:

1. Read the last line — it names the missing module (matplotlib, numpy, pandas, etc.)  
2. Make sure your venv is active — look for (.venv) in your prompt  
3. Install it:

| pip install matplotlib    |
| :---- |

1. Re-run the script.

That's it. The traceback is just Python's way of telling you *exactly* which import failed and *where*, so you know what to install.  
