# Setting up a Nillion project in PyCharm

## Comprehensive Guide: Setting Up a Nillion Project in PyCharm with Python 3.12

### 1. Set up WSL in PyCharm

- Ensure WSL is installed on your Windows machine
- In PyCharm, go to File > Settings > Project > Python Interpreter
- Click the gear icon, select "Add", and choose "WSL"
- Select your Ubuntu distribution

### 2. Open WSL terminal in PyCharm

- Go to View > Tool Windows > Terminal
- Ensure the terminal is using WSL (it should show the Ubuntu prompt)

### 3. Install Python 3.12 and necessary packages in WSL

```bash
sudo add-apt-repository ppa:deadsnakes/ppa
sudo apt update
sudo apt install python3.12 python3.12-venv python3.12-dev
```

### 4. Create and activate a virtual environment using Python 3.12

```bash
python3.12 -m venv nillion_env
source nillion_env/bin/activate
```

### 5. Install Nillion SDK

```bash
curl https://nilup.nilogy.xyz/install.sh | bash
nilup install latest
nilup use latest
nilup init
```

Verify the installation:

```bash
nillion -V
```

### 6. Install Nillion Python client

```bash
pip install py_nillion_client nada_dsl
```

### 7. Set up project structure

- Create a new directory for your project
- Create a `.env` file for environment variables (NILLION_HOST, NILLION_API_KEY)
- Create a `.gitignore` file to exclude sensitive and unnecessary files

### 8. Configure PyCharm to use WSL interpreter with Python 3.12

- Go to File > Settings > Project > Python Interpreter
- Select the Python 3.12 interpreter from your WSL virtual environment

### 9. Set up External Tools in PyCharm for Nillion commands

- Go to File > Settings > Tools > External Tools
- Add new tools for nillion, nada, nada-run, etc., using WSL paths

### 10. Fork and clone the Nillion Python Starter repo

```bash
git clone https://github.com/YOUR_USERNAME/nillion-python-starter.git
cd nillion-python-starter
```

### 11. Install project requirements

```bash
pip install -r requirements.txt
```

### 12. Write your first Nada program

- Navigate to the quickstart directory:

```bash
cd quickstart
```

- Initialize a new Nada project:

```bash
nada init nada_quickstart_programs
```

- Create a new file `secret_addition.py` in `quickstart/nada_quickstart_programs/src/`
- Copy the following code into `secret_addition.py`:

```python
from nada_dsl import *

def nada_main():
    party1 = Party(name="Party1")
    my_int1 = SecretInteger(Input(name="my_int1", party=party1))
    my_int2 = SecretInteger(Input(name="my_int2", party=party1))
    new_int = my_int1 + my_int2
    return [Output(new_int, "my_output", party1)]
```

### 13. Compile, run, and test your program

- Add your program to `nada-project.toml`:

```toml
[[programs]]
path = "src/secret_addition.py"
name = "secret_addition"
prime_size = 128
```

- Build the program:

```bash
nada build
```

- Generate a test:

```bash
nada generate-test --test-name secret_addition_test secret_addition
```

- Run the program:

```bash
nada run secret_addition_test
```

- Test the program (after adjusting the test file):

```bash
nada test secret_addition_test
```

### 14. Connect to the devnet and run your program

- Start the local Nillion devnet:

```bash
nillion-devnet
```

- Create a new file `secret_addition.py` in `quickstart/client_code/`
- Implement the Python client code to interact with the devnet (refer to the full code in the documentation)
- Run the script:

```bash
cd client_code
python3 secret_addition.py
```

### 15. Additional Setup for Production Use

- Create a `.env` file in your project root for environment variables:
  - NILLION_HOST
  - NILLION_API_KEY
- Update your `.gitignore` file to exclude sensitive information

Remember to keep the devnet running in the background while you're working on your project. This setup allows you to develop, test, and run Nillion programs within your PyCharm environment using Python 3.12 and WSL.

If you encounter any issues or need more detailed explanations for specific steps, please don't hesitate to ask for further assistance.
