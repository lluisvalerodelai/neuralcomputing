# Running the Jupyter Notebook on the LIACS Duranium Server

This guide will walk you through the steps to run the Jupyter Notebook for this assignment on the LIACS duranium server and access it from your local machine.

When you ssh into places, you will need to use your university login details (your password).

## 1. Connect to the Server and Prepare Your Environment

First, you'll need to connect to the server, create a directory for your files, and set up the environment.

1.  **SSH into the LIACS server:**
    Open a terminal and use the following command, replacing `sXXXXXXX` with your student number.

    ```bash
    ssh sXXXXXXX@ssh.liacs.nl
    ```

2.  **Connect to the Duranium server:**
    Once logged in, connect to the `duranium` server.

    ```bash
    ssh duranium
    ```

3.  **Create your data directory:**
    Navigate to the `/data` directory and create a folder for your student number. You need this because you have a space limitation within your ~ home directory, but not in the /data directory.

    ```bash
    cd /data
    mkdir sXXXXXXX
    cd sXXXXXXX
    ```

4.  **Copy project files:**
    Copy the assignment files into this new directory with scp or whatever (`/data/sXXXXXXX`).

5.  **Install `uv`:** You can use `uv sync` to install the requirements from the `project.toml` in the GitHub repo.

    *   **Using pip:**
        ```bash
        pip install uv
        ```
    *   **Using curl:**
        ```bash
        curl -LsSf https://astral.sh/uv/install.sh | sh
        ```

6.  **Configure `uv` cache:**
    To avoid exceeding your storage quota, set the `uv` cache directory to your data folder.

    ```bash
    export UV_CACHE_DIR="/data/sXXXXXXX/.uv_cache"
    ```

## 2. Run the Jupyter Notebook

Now you can start the Jupyter Notebook server.

1.  **Start the notebook:**
    Run the following command. It will start the server without opening a browser on the server itself.

    ```bash
    uv run jupyter notebook --no-browser --port=8890
    ```

2.  **Copy the access URL:**
    After a few moments, you will see output that includes a URL with a token. Copy this URL; you will need it to access the notebook. It will look something like this:

    ```
    http://localhost:8890/tree?token=<your-unique-token>
    ```

## 3. Access the Notebook from Your Browser

To view and interact with the notebook, you need to forward the server's port to your local machine.

1.  **Open a NEW terminal:**
    Do not close the first terminal where the notebook is running. Open a **second** terminal on your own computer.

2.  **Set up SSH port forwarding:**
    Run the following command to create an SSH tunnel. This will forward port `8890` from the server to your local machine.

    ```bash
    ssh -J sXXXXXXX@ssh.liacs.nl -L 8890:localhost:8890 sXXXXXXX@duranium.liacs.nl
    ```

3.  **Open the notebook in your browser:**
    Paste the URL you copied earlier into your web browser (the one with the tree and the token). You should now have access to the Jupyter Notebook interface.

