This guide will walk you through the process of installing MongoDB on your macOS machine. We'll cover two primary methods: using Homebrew (recommended) and manual installation.

# Installing MongoDB on macOS

MongoDB is a popular open-source NoSQL database. This guide will help you install it on your macOS machine. We'll cover the recommended method using Homebrew and an alternative manual installation.

## Table of Contents

1.  [Prerequisites](https://www.google.com/search?q=%23prerequisites)
2.  [Method 1: Using Homebrew (Recommended)](https://www.google.com/search?q=%23method-1-using-homebrew-recommended)
      * [Step 1: Install Homebrew (if you haven't already)](https://www.google.com/search?q=%23step-1-install-homebrew-if-you-havent-already)
      * [Step 2: Tap the MongoDB Homebrew Tap](https://www.google.com/search?q=%23step-2-tap-the-mongodb-homebrew-tap)
      * [Step 3: Install MongoDB Community Edition](https://www.google.com/search?q=%23step-3-install-mongodb-community-edition)
      * [Step 4: Start MongoDB](https://www.google.com/search?q=%23step-4-start-mongodb)
      * [Step 5: Verify Installation](https://www.google.com/search?q=%23step-5-verify-installation)
      * [Step 6: Stop MongoDB](https://www.google.com/search?q=%23step-6-stop-mongodb)
      * [Step 7: Configure MongoDB to Launch at Login (Optional)](https://www.google.com/search?q=%23step-7-configure-mongodb-to-launch-at-login-optional)
3.  [Method 2: Manual Installation](https://www.google.com/search?q=%23method-2-manual-installation)
      * [Step 1: Download MongoDB Community Edition](https://www.google.com/search?q=%23step-1-download-mongodb-community-edition)
      * [Step 2: Extract the Tarball](https://www.google.com/search?q=%23step-2-extract-the-tarball)
      * [Step 3: Create the Data Directory](https://www.google.com/search?q=%23step-3-create-the-data-directory)
      * [Step 4: Add MongoDB to your PATH (Optional but Recommended)](https://www.google.com/search?q=%23step-4-add-mongodb-to-your-path-optional-but-recommended)
      * [Step 5: Start MongoDB](https://www.google.com/search?q=%23step-5-start-mongodb-1)
      * [Step 6: Verify Installation](https://www.google.com/search?q=%23step-6-verify-installation-1)
4.  [Connecting to MongoDB](https://www.google.com/search?q=%23connecting-to-mongodb)
5.  [Troubleshooting](https://www.google.com/search?q=%23troubleshooting)

## Prerequisites

Before you begin, ensure you have:

  * A macOS machine.
  * Administrator privileges to install software.
  * An active internet connection.

## Method 1: Using Homebrew (Recommended)

Homebrew simplifies the installation of software on macOS. It's the easiest and most recommended way to install MongoDB.

### Step 1: Install Homebrew (if you haven't already)

Open your **Terminal** application (you can find it in `Applications/Utilities` or by searching with Spotlight `Cmd + Space` and typing "Terminal").

Paste the following command and press Enter:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Follow the on-screen instructions, which may include entering your user password.

### Step 2: Tap the MongoDB Homebrew Tap

MongoDB maintains its own Homebrew "tap" (a repository of formulas) for community edition. You need to add this tap to your Homebrew installation.

In your Terminal, run:

```bash
brew tap mongodb/brew
```

### Step 3: Install MongoDB Community Edition

Now you can install MongoDB Community Edition using Homebrew.

```bash
brew install mongodb-community@7.0
```

  * **Note:** The `@7.0` specifies the version. You can change this to a different major version if needed (e.g., `@6.0`). Always check the official MongoDB documentation for the latest recommended stable version.

This command will download and install MongoDB, along with its dependencies. This might take a few minutes.

### Step 4: Start MongoDB

After the installation is complete, you can start the MongoDB server.

```bash
brew services start mongodb-community@7.0
```

Homebrew will start `mongod` (the MongoDB daemon) and configure it to run as a background service.

### Step 5: Verify Installation

To verify that MongoDB is running, you can check the service status:

```bash
brew services list
```

You should see `mongodb-community@7.0` listed with a `started` status.

You can also connect to the MongoDB shell:

```bash
mongosh
```

If everything is working correctly, you will see the MongoDB shell prompt, for example:

```
Current Mongosh Log ID:        648937e0045d6a2f64f4f2c3
Connecting to:                 mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+2.0.2
Using MongoDB:                 7.0.8
Using Mongosh:                 2.0.2

For usage instructions, see: https://docs.mongodb.com/mongodb-shell/

test>
```

To exit the MongoDB shell, type `exit` and press Enter.

### Step 6: Stop MongoDB

If you need to stop the MongoDB server, use:

```bash
brew services stop mongodb-community@7.0
```

### Step 7: Configure MongoDB to Launch at Login (Optional)

By default, `brew services start` will configure MongoDB to launch automatically when your Mac starts up. If you disabled this or want to explicitly ensure it, you can use the `brew services` command.

If you already started it using `brew services start`, it's already configured to launch at login.

## Method 2: Manual Installation

This method involves downloading the MongoDB binaries directly and setting them up manually. This gives you more control but requires more manual configuration.

### Step 1: Download MongoDB Community Edition

1.  Open your web browser and go to the official MongoDB Download Center:
    [https://www.mongodb.com/try/download/community](https://www.mongodb.com/try/download/community)

2.  Select the following options:

      * **Version:** Choose the desired stable version (e.g., `7.0.x`).
      * **Platform:** Select `macOS`.
      * **Package:** Choose `tgz`.

3.  Click the "Download" button. The `.tgz` file will be downloaded to your `Downloads` folder.

### Step 2: Extract the Tarball

Open your **Terminal**. Navigate to your `Downloads` directory:

```bash
cd ~/Downloads
```

Extract the downloaded tarball. Replace `mongodb-macos-x86_64-7.0.8.tgz` with the actual filename you downloaded:

```bash
tar -zxvf mongodb-macos-x86_64-7.0.8.tgz
```

This will create a directory (e.g., `mongodb-macos-x86_64-7.0.8`) containing the MongoDB binaries.

Move the extracted directory to a more permanent location, such as `/usr/local/mongodb` or `/opt/mongodb`. We'll use `/usr/local` for this example.

```bash
sudo mv mongodb-macos-x86_64-7.0.8 /usr/local/mongodb
```

You might be prompted for your administrator password.

### Step 3: Create the Data Directory

MongoDB requires a data directory where it stores its data files. By default, this is `/data/db`. You need to create this directory and ensure proper permissions.

```bash
sudo mkdir -p /data/db
```

Now, set the permissions for the data directory so that your user can read and write to it. Replace `YOUR_USERNAME` with your actual macOS username.

```bash
sudo chown -R `id -un` /data/db
```

Alternatively, you can create a data directory within your user's home directory to avoid `sudo` for `chown`:

```bash
mkdir -p ~/data/db
```

If you choose this, remember to specify this path when starting `mongod` (e.g., `mongod --dbpath ~/data/db`).

### Step 4: Add MongoDB to your PATH (Optional but Recommended)

Adding the MongoDB `bin` directory to your system's `PATH` makes it easier to run `mongod` and `mongosh` from any directory in your Terminal without typing the full path.

1.  Open your shell profile file. This is typically `.bash_profile`, `.zshrc`, or `.profile` in your home directory, depending on your shell. For modern macOS, it's usually `.zshrc`.

    ```bash
    nano ~/.zshrc   # If you use Zsh
    # or
    nano ~/.bash_profile # If you use Bash
    ```

2.  Add the following line to the end of the file. If you moved MongoDB to a different path in Step 2, adjust `/usr/local/mongodb` accordingly.

    ```bash
    export PATH=/usr/local/mongodb/bin:$PATH
    ```

3.  Save the file and exit the editor:

      * For `nano`: Press `Ctrl + O`, then `Enter` to save, then `Ctrl + X` to exit.

4.  Apply the changes to your current terminal session:

    ```bash
    source ~/.zshrc  # Or source ~/.bash_profile
    ```

### Step 5: Start MongoDB

Now you can start the MongoDB server (`mongod`).

If you created `/data/db` and set permissions:

```bash
mongod
```

If you created `~/data/db`:

```bash
mongod --dbpath ~/data/db
```

The `mongod` process will start, and you'll see a lot of output in your terminal indicating that it's running and listening for connections on port `27017`. **Keep this Terminal window open** as `mongod` runs in the foreground. To run it in the background, you can use `mongod --fork --logpath /path/to/logfile.log`.

### Step 6: Verify Installation

Open a **new** Terminal window.

Connect to the MongoDB shell:

```bash
mongosh
```

If successful, you will see the MongoDB shell prompt.

To exit the MongoDB shell, type `exit` and press Enter.

To stop the `mongod` process (if running in the foreground), go back to the Terminal window where `mongod` is running and press `Ctrl + C`.

## Connecting to MongoDB

Once MongoDB is running, you can connect to it using the `mongosh` (MongoDB Shell).

```bash
mongosh
```

This will connect to the default MongoDB instance running on `localhost:27017`.

From the shell, you can start interacting with your database. For example:

  * Show all databases: `show dbs`
  * Switch to a database (creates it if it doesn't exist): `use mydatabase`
  * Insert a document into a collection: `db.mycollection.insertOne({ name: "John Doe", age: 30 })`
  * Find documents: `db.mycollection.find()`

## Troubleshooting

  * **Permissions issues for `/data/db`**: If you get errors related to permissions when starting `mongod`, ensure you've run ` sudo chown -R  `id -un`  /data/db ` correctly or choose a different data directory that your user has full write access to.
  * **`mongod` not found (Manual Installation)**: If you can't run `mongod` directly, ensure you've added the MongoDB `bin` directory to your `PATH` and sourced your shell profile file. Alternatively, navigate to `/usr/local/mongodb/bin` (or wherever you installed it) and run `./mongod`.
  * **Port in use**: If MongoDB fails to start because the default port (27017) is already in use, you can specify a different port using the `--port` option when starting `mongod` (e.g., `mongod --port 27018`).
  * **Checking logs**: MongoDB writes logs that can be helpful for troubleshooting. By default, Homebrew logs are managed by `brew services`. For manual installations, `mongod` will output logs to the terminal, or you can specify a log file with `--logpath`.

**You can also refer to the below youtube link for Video on MongoDB installation.**

[How to Install MongoDB on Mac](https://youtu.be/8gUQL2zlpvI?si=ALpEjs4R-90VoXEk)
