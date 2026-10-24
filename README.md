# spark-installation-WSL
This is a complete, tested method for installing Apache Spark on Windows using WSL (Ubuntu). It has been tested and works successfully! ✅  Simply follow the `README.md` file step by step and **copy and paste the commands provided**. That's all you need to do! 🚀

## My Experience

I personally installed and tested this setup on my own laptop, which has **8 GB of RAM and a 512 GB SSD**, and it works well!

Before finding this method, I watched many YouTube tutorials and spent a lot of time trying different approaches. Unfortunately, I wasted time and valuable disk space on methods that didn't work as expected. It took me several days to understand the installation process and figure out the right steps.

Finally, I successfully installed Apache Spark and PySpark on my Windows laptop using WSL2 (Ubuntu). I created this guide to help others avoid the same difficulties and save time.

**You can try this method on your own laptop!** Just follow the steps in the `README.md` file in the given order and copy and paste the commands carefully.

### Need Help?

If you face any problems during installation or have suggestions to improve this guide, feel free to contact me:

📧 **Email:** [sample101918@gmail.com](mailto:sample101918@gmail.com)

I'll be happy to help you as much as I can. I hope this guide saves you time and makes your Spark installation journey easier!


# Apache Spark and PySpark Installation Guide for Beginners

### A Complete Step-by-Step Guide for Windows 10/11

---

## 📌 1. Introduction

This guide explains how to install and configure **Python, Java, Apache Spark, and PySpark** on a Windows computer using WSL Ubuntu and Visual Studio Code.

This tutorial is written for beginners. You do not need prior experience with Linux or Apache Spark.

By following this guide, you will learn how to:

* Install Ubuntu on Windows using WSL.
* Install Python and Java.
* Download and configure Apache Spark.
* Create a Python virtual environment.
* Install PySpark.
* Configure environment variables.
* Configure the Spark History Server.
* Connect Ubuntu to Visual Studio Code.
* Write and execute your first PySpark program.

### Technologies Used

| Technology           | Purpose                              |
| :------------------- | :----------------------------------- |
| Windows 10/11        | Main operating system                |
| WSL 2                | Runs Linux on Windows                |
| Ubuntu               | Linux development environment        |
| Python               | Programming language                 |
| Java 17              | Runs the Spark engine                |
| Apache Spark         | Data processing engine               |
| PySpark              | Allows us to use Spark with Python   |
| VS Code              | Code editor                          |
| Spark History Server | Displays recorded Spark applications |

### How Everything Works

```text
+------------------------------------------------+
|                  WINDOWS                       |
|                                                |
|  +------------------------------------------+  |
|  |                VS CODE                   |  |
|  |                                          |  |
|  |  +------------------------------------+  |  |
|  |  |           WSL 2 - UBUNTU           |  |  |
|  |  |                                    |  |  |
|  |  |  Python                            |  |  |
|  |  |    |                               |  |  |
|  |  |    v                               |  |  |
|  |  |  PySpark                           |  |  |
|  |  |    |                               |  |  |
|  |  |    v                               |  |  |
|  |  |  Apache Spark                      |  |  |
|  |  |    |                               |  |  |
|  |  |    v                               |  |  |
|  |  |  Java 17                           |  |  |
|  |  |                                    |  |  |
|  |  +------------------------------------+  |  |
|  +------------------------------------------+  |
+------------------------------------------------+
```

---

# STEP 1: Install WSL and Ubuntu

## 1.1 What is WSL?

WSL stands for Windows Subsystem for Linux.

It allows you to run a Linux environment inside Windows without installing a separate operating system.

We will use Ubuntu as our Linux environment.

## 1.2 Check Whether WSL Is Already Installed

Open **PowerShell as Administrator**.

Run:

```powershell
wsl --status
```

To see your installed Linux distributions, run:

```powershell
wsl --list --verbose
```

If Ubuntu is already installed and its version is `2`, you can continue to Step 2.

## 1.3 Install WSL and Ubuntu

If WSL is not installed, run this command in PowerShell as Administrator:

```powershell
wsl --install -d Ubuntu
```

Restart your computer if Windows requests it.

Ubuntu may open automatically. If it does not, open Ubuntu from the Windows Start menu.

During the first launch, Ubuntu asks you to create:

1. A Linux username.
2. A Linux password.

Choose a username and password.

**Important:** When entering your Linux password, the terminal may not display any characters. This is normal. Type your password and press Enter.

## 1.4 Verify Ubuntu

Open the Ubuntu terminal and run:

```bash
whoami
```

This displays your Linux username.

Next, run:

```bash
echo $HOME
```

The output should look similar to:

```text
/home/your_username
```

Your actual username may be different.

### Expected Result

Ubuntu is installed and ready to use.

---

# STEP 2: Update Ubuntu

Before installing software, update Ubuntu's package information.

Run:

```bash
sudo apt update
```

Enter your Ubuntu password if requested.

### What does this command do?

It updates the list of available software packages.

It does not upgrade every installed package.

To install available package updates as well, you can optionally run:

```bash
sudo apt upgrade
```

For this tutorial, updating the package list is sufficient to continue.

---

# STEP 3: Install Python

## 3.1 What Is Python?

Python is a programming language.

We will use Python to write programs that process data using Apache Spark.

## 3.2 Install Python and Required Tools

In Ubuntu, run:

```bash
sudo apt install -y python3 python3-pip python3-venv
```

### What are these packages?

| Package        | Purpose                                  |
| :------------- | :--------------------------------------- |
| `python3`      | Installs Python                          |
| `python3-pip`  | Installs the Python package manager      |
| `python3-venv` | Allows us to create virtual environments |

## 3.3 Check the Python Version

Run:

```bash
python3 --version
```

Example output:

```text
Python 3.12.3
```

Your Python version may be different.

## 3.4 Find the Python Installation

Run:

```bash
which python3
```

Example output:

```text
/usr/bin/python3
```

This is the location of Ubuntu's system Python interpreter.

### Expected Result

Python is installed and ready to use.

---

# STEP 4: Install Java 17

## 4.1 Why Do We Need Java?

Apache Spark uses the Java Virtual Machine (JVM) to execute its engine.

Even though we write our Spark programs in Python, Java is needed for the Spark runtime.

## 4.2 Install OpenJDK 17

Run:

```bash
sudo apt install -y openjdk-17-jdk
```

Wait for the installation to finish.

## 4.3 Verify Java

Run:

```bash
java -version
```

The output should identify Java 17.

For example:

```text
openjdk version "17..."
```

The exact version information may differ.

## 4.4 Find the Java Executable

Run:

```bash
which java
```

Typical output:

```text
/usr/bin/java
```

## 4.5 Find the Java Installation Directory

Run:

```bash
ls -d /usr/lib/jvm/java-17-openjdk-amd64
```

On a standard 64-bit Ubuntu installation on an x86-64 computer, the expected directory is:

```text
/usr/lib/jvm/java-17-openjdk-amd64
```

If this command reports that the directory does not exist, check the actual installation directories:

```bash
ls /usr/lib/jvm
```

Use the appropriate Java 17 directory for your system in the next step.

### Expected Result

Java 17 is installed.

---

# STEP 5: Configure JAVA_HOME

## 5.1 What Is JAVA_HOME?

`JAVA_HOME` is an environment variable that tells software where Java is installed.

Instead of repeatedly typing the Java installation path, we can store it in this variable.

## 5.2 Open the Ubuntu Configuration File

Run:

```bash
nano ~/.bashrc
```

The `.bashrc` file contains commands and settings that are loaded when Bash starts an interactive shell.

Scroll to the bottom of the file.

Add this line for the standard 64-bit Ubuntu Java 17 installation:

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
```

If your Java installation is in a different directory, use that directory instead.

## 5.3 Save the File

Inside Nano:

1. Press `Ctrl + O`.
2. Press Enter to save.
3. Press `Ctrl + X` to exit.

## 5.4 Apply the Configuration

Run:

```bash
source ~/.bashrc
```

## 5.5 Verify JAVA_HOME

Run:

```bash
echo $JAVA_HOME
```

Expected output on the standard installation:

```text
/usr/lib/jvm/java-17-openjdk-amd64
```

### Expected Result

The `JAVA_HOME` environment variable is configured.

---

# STEP 6: Download Apache Spark

## 6.1 What Is Apache Spark?

Apache Spark is a data processing engine used for tasks such as:

* Batch data processing.
* Data transformations.
* ETL pipelines.
* DataFrame operations.
* Spark SQL.
* Structured Streaming.

We will use Spark version **3.5.5** throughout this tutorial to keep the installation steps consistent.

## 6.2 Open Your Home Directory

Run:

```bash
cd ~
```

The `~` symbol represents your Linux home directory.

Check your current directory:

```bash
pwd
```

The output should look like:

```text
/home/your_username
```

## 6.3 Download Spark

Run:

```bash
wget https://archive.apache.org/dist/spark/spark-3.5.5/spark-3.5.5-bin-hadoop3.tgz
```

This downloads the Apache Spark archive.

The file is several hundred megabytes, so the download may take some time.

## 6.4 Verify the Download

Run:

```bash
ls -lh spark-3.5.5-bin-hadoop3.tgz
```

You should see the downloaded archive.

### What Does the Filename Mean?

```text
spark-3.5.5-bin-hadoop3.tgz
     |     |   |       |
     |     |   |       +-- Compressed archive
     |     |   +---------- Built for Hadoop 3
     |     +-------------- Version 3.5.5
     +-------------------- Apache Spark
```

### Expected Result

The Spark archive is downloaded into your home directory.

---

# STEP 7: Extract Apache Spark

## 7.1 Why Do We Extract the Archive?

The downloaded file is compressed.

We must extract it to access the Spark programs, libraries, and configuration files.

## 7.2 Extract Spark

Make sure you are in your home directory:

```bash
cd ~
```

Run:

```bash
tar -xzf spark-3.5.5-bin-hadoop3.tgz -C ~
```

Wait for the extraction to finish.

## 7.3 Verify the Installation

Run:

```bash
ls ~/spark-3.5.5-bin-hadoop3
```

You should see directories such as:

```text
bin
conf
jars
python
sbin
```

Other files and directories may also be present.

## 7.4 Understand the Important Directories

| Directory | Purpose                                             |
| :-------- | :-------------------------------------------------- |
| `bin`     | Contains Spark execution commands                   |
| `conf`    | Contains Spark configuration files                  |
| `jars`    | Contains Spark's Java libraries                     |
| `python`  | Contains Python-related Spark files                 |
| `sbin`    | Contains scripts for starting and stopping services |

Your Spark installation directory is:

```text
~/spark-3.5.5-bin-hadoop3
```

The full path will look like:

```text
/home/your_username/spark-3.5.5-bin-hadoop3
```

### Expected Result

Apache Spark has been extracted.

---

# STEP 8: Configure SPARK_HOME and PATH

## 8.1 What Is SPARK_HOME?

`SPARK_HOME` tells applications where Apache Spark is installed.

For this tutorial, its value will be:

```text
$HOME/spark-3.5.5-bin-hadoop3
```

## 8.2 What Is PATH?

`PATH` is an environment variable containing directories in which Linux searches for executable commands.

Adding Spark's `bin` directory to PATH allows you to run commands such as `spark-submit` without typing the full installation path.

## 8.3 Open .bashrc

Run:

```bash
nano ~/.bashrc
```

At the bottom, add:

```bash
export SPARK_HOME=$HOME/spark-3.5.5-bin-hadoop3
```

Then add:

```bash
export PATH=$JAVA_HOME/bin:$SPARK_HOME/bin:$PATH
```

Make sure the `JAVA_HOME` line from Step 5 is also present.

Your three environment-variable lines should look like this:

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
export SPARK_HOME=$HOME/spark-3.5.5-bin-hadoop3
export PATH=$JAVA_HOME/bin:$SPARK_HOME/bin:$PATH
```

If your Java installation directory is different, use the correct directory for `JAVA_HOME`.

**Important:** Add these lines only once. Do not repeatedly add duplicate entries.

## 8.4 Save and Reload

Save the file:

1. Press `Ctrl + O`.
2. Press Enter.
3. Press `Ctrl + X`.

Reload the configuration:

```bash
source ~/.bashrc
```

## 8.5 Verify SPARK_HOME

Run:

```bash
echo $SPARK_HOME
```

The output should look like:

```text
/home/your_username/spark-3.5.5-bin-hadoop3
```

## 8.6 Verify the Spark Command

Run:

```bash
which spark-submit
```

Expected output:

```text
/home/your_username/spark-3.5.5-bin-hadoop3/bin/spark-submit
```

The username and home-directory path will vary.

## 8.7 Verify the Spark Version

Run:

```bash
spark-submit --version
```

The output should identify:

```text
version 3.5.5
```

### Expected Result

`JAVA_HOME`, `SPARK_HOME`, and PATH are configured.

---

# STEP 9: Create a Python Virtual Environment

## 9.1 What Is a Virtual Environment?

A Python virtual environment provides an isolated location for the Python packages used by a project.

For example, we can install PySpark in a virtual environment without mixing it with Ubuntu's system Python packages.

We will name the environment:

```text
spark-env
```

## 9.2 Create the Environment

Run this command from your home directory:

```bash
cd ~
```

Create the environment:

```bash
python3 -m venv ~/spark-env
```

This creates the directory:

```text
/home/your_username/spark-env
```

## 9.3 Activate the Environment

Run:

```bash
source ~/spark-env/bin/activate
```

Your terminal prompt should now start with:

```text
(spark-env)
```

For example:

```text
(spark-env) username@computer:~$
```

The exact prompt will vary.

## 9.4 What Does Activation Do?

When you activate the environment, commands such as `python` and `pip` use the environment's executables.

You can check the Python executable with:

```bash
which python
```

Expected output:

```text
/home/your_username/spark-env/bin/python
```

### Expected Result

The virtual environment is created and activated.

---

# STEP 10: Install PySpark

## 10.1 What Is PySpark?

PySpark is the Python API for Apache Spark.

It allows us to write Spark applications using Python instead of writing the entire application in Java or Scala.

## 10.2 Make Sure the Virtual Environment Is Active

Your terminal prompt should contain:

```text
(spark-env)
```

If it does not, run:

```bash
source ~/spark-env/bin/activate
```

## 10.3 Install PySpark 3.5.5

Run:

```bash
python -m pip install pyspark==3.5.5
```

Wait for the installation to complete.

## 10.4 Verify the Installation

Run:

```bash
python -c "import pyspark; print(pyspark.__version__)"
```

Expected output:

```text
3.5.5
```

## 10.5 Understand the Components

```text
Python
  |
  |-- Programming language
  |
  v
PySpark
  |
  |-- Python interface to Apache Spark
  |
  v
Apache Spark
  |
  |-- Executes data processing tasks
```

### Expected Result

PySpark is installed in the virtual environment.

---

# STEP 11: Create the Spark Event-Log Directory

## 11.1 What Is an Event Log?

Spark can record information about an application's execution.

These records can later be viewed using the Spark History Server.

We will store these records in a directory named:

```text
SparkHistLogs
```

## 11.2 Create the Directory

Run:

```bash
mkdir -p ~/SparkHistLogs
```

The `-p` option creates the directory if it does not exist and does not report an error if it already exists.

## 11.3 Verify the Directory

Run:

```bash
ls -ld ~/SparkHistLogs
```

The directory should be listed.

### Expected Result

The event-log directory is ready.

---

# STEP 12: Configure the Spark History Server

## 12.1 What Is the Spark History Server?

The Spark History Server provides a web interface for reviewing Spark applications whose event logs have been recorded.

It is useful when an application has already finished and its normal application UI is no longer available.

## 12.2 Open the Spark Configuration File

Run:

```bash
nano ~/spark-3.5.5-bin-hadoop3/conf/spark-defaults.conf
```

This file stores default Spark configuration properties.

## 12.3 Add the Event-Logging Settings

Add these three lines:

```properties
spark.eventLog.enabled true
spark.eventLog.dir file:///home/your_username/SparkHistLogs
spark.history.fs.logDirectory file:///home/your_username/SparkHistLogs
```

**Important:** Replace `your_username` with your actual Linux username.

For example, if your Linux username is `aforashwin`, use:

```properties
spark.eventLog.enabled true
spark.eventLog.dir file:///home/aforashwin/SparkHistLogs
spark.history.fs.logDirectory file:///home/aforashwin/SparkHistLogs
```

Do not add duplicate versions of these properties if they already exist. Update the existing values instead.

## 12.4 Understand Each Setting

### Enable event logging

```properties
spark.eventLog.enabled true
```

Enables recording of Spark application events.

### Choose where Spark saves event logs

```properties
spark.eventLog.dir file:///home/your_username/SparkHistLogs
```

Specifies the directory in which Spark writes the event logs.

### Choose where the History Server reads event logs

```properties
spark.history.fs.logDirectory file:///home/your_username/SparkHistLogs
```

Specifies the directory the History Server reads.

The three slashes after `file:` are intentional.

## 12.5 Save the File

1. Press `Ctrl + O`.
2. Press Enter.
3. Press `Ctrl + X`.

### Expected Result

Spark is configured to record application event logs in your local directory.

---

# STEP 13: Start the Spark History Server

## 13.1 Start the Service

Run:

```bash
$SPARK_HOME/sbin/start-history-server.sh
```

This starts the History Server using your Spark installation.

## 13.2 Verify That It Is Running

Run:

```bash
jps
```

The output should contain a process named:

```text
HistoryServer
```

The process ID will vary.

If the command `jps` is unavailable, install the JDK package if you have not already done so and check again.

## 13.3 Open the History Server

Open your Windows browser and visit:

http://localhost:18080

The page should display the Spark History Server interface if the service started successfully.

### Why Port 18080?

Port `18080` is the default web interface port for the Spark History Server.

### What If No Applications Appear?

This can happen if no Spark application has generated event logs yet.

Run a Spark application with event logging enabled, allow it to finish, and refresh the History Server page.

## 13.4 Stop the History Server

When you no longer need it, run:

```bash
$SPARK_HOME/sbin/stop-history-server.sh
```

You can start it again later using the start command.

### Expected Result

The Spark History Server is configured and can be started when needed.

---

# STEP 14: Install Visual Studio Code

## 14.1 What Is VS Code?

Visual Studio Code is a code editor that allows you to create and edit Python programs.

We will use its WSL integration to edit and run files inside Ubuntu.

## 14.2 Install VS Code

If you do not already have VS Code, download it from the official website:

https://code.visualstudio.com/

Install it on Windows.

## 14.3 Install the Required VS Code Extensions

Open VS Code and select the Extensions icon.

Install:

1. **WSL** by Microsoft.
2. **Python** by Microsoft.

The Python extension helps VS Code identify Python interpreters and run Python programs.

The WSL extension allows VS Code to connect to your Ubuntu environment.

## 14.4 Connect VS Code to Ubuntu

Open Ubuntu and run:

```bash
code .
```

If prompted, allow VS Code to install its WSL server components.

VS Code should open in the Ubuntu environment.

You can verify the connection by checking that the bottom-left corner indicates WSL or Ubuntu.

### Expected Result

VS Code is connected to Ubuntu.

---

# STEP 15: Create Your First Spark Project

## 15.1 Create a Project Directory

Open the Ubuntu terminal.

Run:

```bash
mkdir -p ~/spark-projects
```

Move into the directory:

```bash
cd ~/spark-projects
```

## 15.2 Open the Project in VS Code

Run:

```bash
code .
```

This opens the current directory in VS Code.

## 15.3 Create a Python File

In VS Code:

1. Open the Explorer panel.
2. Click **New File**.
3. Name the file `spark_test.py`.

Your project should now look like this:

```text
spark-projects/
|
+-- spark_test.py
```

## 15.4 Write Your First PySpark Program

Copy this code into `spark_test.py`:

```python
from pyspark.sql import SparkSession

# Create a Spark session
spark = (
    SparkSession.builder
    .appName("MyFirstSparkApp")
    .master("local[*]")
    .getOrCreate()
)

# Create sample data
data = [
    (1, "Alice", 50000),
    (2, "Bob", 60000),
    (3, "Charlie", 70000)
]

# Define the column names
columns = ["id", "name", "salary"]

# Create a Spark DataFrame
df = spark.createDataFrame(data, columns)

# Display the data
df.show()

# Count the records
print("Total records:", df.count())

# Stop the Spark session
spark.stop()
```

Save the file by pressing:

`Ctrl + S`

### Understand the Code

| Code                   | Meaning                                              |
| :--------------------- | :--------------------------------------------------- |
| `SparkSession.builder` | Creates or obtains a Spark session                   |
| `.appName()`           | Sets the application name                            |
| `.master("local[*]")`  | Runs Spark locally using available logical CPU cores |
| `createDataFrame()`    | Creates a Spark DataFrame                            |
| `df.show()`            | Displays the data                                    |
| `df.count()`           | Counts the records                                   |
| `spark.stop()`         | Stops the Spark session                              |

**Note:** `local[*]` runs Spark on your local computer. It does not create a remote cluster.

---

# STEP 16: Select the Python Interpreter in VS Code

## 16.1 Why Is This Necessary?

VS Code may use the system Python instead of the virtual environment where PySpark is installed.

If it uses the wrong interpreter, you may see this error:

```text
ModuleNotFoundError: No module named 'pyspark'
```

We must select the Python interpreter inside `spark-env`.

## 16.2 Select the Interpreter

In VS Code:

1. Press `Ctrl + Shift + P`.
2. Search for `Python: Select Interpreter`.
3. Choose the option to enter an interpreter path if necessary.
4. Select or enter the following path:

```text
/home/your_username/spark-env/bin/python
```

Replace `your_username` with your Linux username.

For example:

```text
/home/ashwin_balaji/spark-env/bin/python
```

5. Confirm the selection.

### Expected Result

VS Code uses the Python interpreter that has PySpark installed.

---

# STEP 17: Run Your First PySpark Program

Now we will execute the program.

## 17.1 Open the VS Code Terminal

In VS Code, select:

**Terminal → New Terminal**

Make sure the terminal is connected to Ubuntu.

## 17.2 Navigate to Your Project

Run:

```bash
cd ~/spark-projects
```

## 17.3 Activate the Virtual Environment

Run:

```bash
source ~/spark-env/bin/activate
```

Your terminal prompt should start with:

```text
(spark-env)
```

## 17.4 Verify PySpark

Run:

```bash
python -c "import pyspark; print(pyspark.__version__)"
```

Expected output:

```text
3.5.5
```

## 17.5 Run the Program

Run:

```bash
python spark_test.py
```

Wait for Spark to initialize and execute the program.

## 17.6 Expected Output

You should see output similar to:

```text
+---+-------+------+
| id|   name|salary|
+---+-------+------+
|  1|  Alice| 50000|
|  2|    Bob| 60000|
|  3|Charlie| 70000|
+---+-------+------+

Total records: 3
```

The exact spacing and additional Spark messages may vary.

### Expected Result

Congratulations! You have successfully run your first PySpark application.

---

# STEP 18: Understand the Spark Web Interfaces

Spark provides two useful web interfaces.

## 18.1 Spark Application UI

Address:

http://localhost:4040

This interface provides details about a running Spark application.

You can inspect:

* Jobs.
* Stages.
* Tasks.
* SQL execution.
* Storage information.
* Environment settings.

**Important:** This interface normally exists only while the application is running. If the application finishes quickly, the page may no longer be available.

## 18.2 Spark History Server

Address:

http://localhost:18080

This interface displays recorded applications.

It can show information about completed applications when their event logs are available.

### Difference Between the Two

| Feature                                 | Spark Application UI                      | Spark History Server               |
| :-------------------------------------- | :---------------------------------------- | :--------------------------------- |
| Default port                            | `4040`                                    | `18080`                            |
| Purpose                                 | Inspect a running application             | Inspect recorded applications      |
| Requires event logs                     | Not in the same way as the History Server | Yes                                |
| Available after an application finishes | Normally no                               | Yes, if its event log is available |

---

# STEP 19: Common Problems and Solutions

## Problem 1: `ModuleNotFoundError: No module named 'pyspark'`

### Cause

The virtual environment is not active, or VS Code is using the wrong Python interpreter.

### Solution

Run:

```bash
source ~/spark-env/bin/activate
```

Then verify:

```bash
python -c "import pyspark; print(pyspark.__version__)"
```

If PySpark is not installed in this environment, install it:

```bash
python -m pip install pyspark==3.5.5
```

Also verify that VS Code uses:

```text
/home/your_username/spark-env/bin/python
```

---

## Problem 2: `JAVA_HOME is not set`

### Cause

The Java environment variable is missing or incorrect.

### Solution

Check:

```bash
echo $JAVA_HOME
```

If it is empty, confirm the Java installation directory:

```bash
ls /usr/lib/jvm
```

Open the configuration file:

```bash
nano ~/.bashrc
```

Add the correct Java 17 directory. For a standard 64-bit Ubuntu installation:

```bash
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
```

Reload the configuration:

```bash
source ~/.bashrc
```

Check again:

```bash
echo $JAVA_HOME
```

---

## Problem 3: `spark-submit: command not found`

### Cause

The Spark `bin` directory is missing from PATH, or the terminal has not loaded the configuration.

### Solution

Run:

```bash
source ~/.bashrc
```

Check:

```bash
echo $SPARK_HOME
```

Then:

```bash
which spark-submit
```

If Spark is installed in a different directory, correct `SPARK_HOME` in `.bashrc`.

---

## Problem 4: History Server Shows No Applications

### Cause

No event logs have been generated, or the History Server is looking in the wrong directory.

### Solution

Verify the event-log directory:

```bash
ls -ld ~/SparkHistLogs
```

Check the settings:

```bash
cat ~/spark-3.5.5-bin-hadoop3/conf/spark-defaults.conf
```

Confirm that the settings point to the same event-log directory.

Run a Spark application and allow it to finish. Refresh the History Server page afterward.

---

## Problem 5: Port 4040 Does Not Open

### Cause

The Spark application may have finished, or port `4040` may already be in use.

### Solution

Run your Spark program again:

```bash
python spark_test.py
```

While the application is running, open:

http://localhost:4040

For a program that finishes too quickly, you may need a longer-running test application to inspect the UI.

---

# STEP 20: Daily Commands to Remember

These are the main commands you will use during development.

### 1. Activate the Python environment

```bash
source ~/spark-env/bin/activate
```

### 2. Open the project directory

```bash
cd ~/spark-projects
```

### 3. Run the Spark program

```bash
python spark_test.py
```

### 4. Check the Spark version

```bash
spark-submit --version
```

### 5. Start the History Server

```bash
$SPARK_HOME/sbin/start-history-server.sh
```

### 6. Stop the History Server

```bash
$SPARK_HOME/sbin/stop-history-server.sh
```

### 7. Check the Java and Spark environment variables

```bash
echo $JAVA_HOME
echo $SPARK_HOME
```

### 8. Check the History Server process

```bash
jps
```

---

# STEP 21: Final Directory Structure

After completing the tutorial, your home directory should contain the following important directories:

```text
/home/your_username/
|
+-- spark-3.5.5-bin-hadoop3/
|   |
|   +-- bin/
|   +-- conf/
|   |   |
|   |   +-- spark-defaults.conf
|   |
|   +-- jars/
|   +-- python/
|   +-- sbin/
|
+-- spark-env/
|   |
|   +-- bin/
|       |
|       +-- activate
|       +-- python
|
+-- spark-projects/
|   |
|   +-- spark_test.py
|
+-- SparkHistLogs/
|
+-- .bashrc
```

The exact files and directories may differ slightly.

### What Does Each Directory Do?

| Directory or File          | Purpose                                              |
| :------------------------- | :--------------------------------------------------- |
| `spark-3.5.5-bin-hadoop3/` | Contains Apache Spark                                |
| `spark-env/`               | Contains the Python virtual environment              |
| `spark-projects/`          | Stores your Python programs                          |
| `SparkHistLogs/`           | Stores Spark event logs                              |
| `.bashrc`                  | Stores shell configuration and environment variables |

---

# STEP 22: Installation Checklist

Use this checklist to verify that every step is complete.

* [ ] WSL 2 installed.
* [ ] Ubuntu installed and working.
* [ ] Python installed.
* [ ] Java 17 installed.
* [ ] `JAVA_HOME` configured.
* [ ] Apache Spark 3.5.5 downloaded.
* [ ] Apache Spark extracted.
* [ ] `SPARK_HOME` configured.
* [ ] Spark added to PATH.
* [ ] Python virtual environment created.
* [ ] PySpark 3.5.5 installed.
* [ ] Spark event-log directory created.
* [ ] Spark History Server configured.
* [ ] VS Code installed.
* [ ] WSL and Python extensions installed in VS Code.
* [ ] Correct Python interpreter selected.
* [ ] First PySpark program created.
* [ ] First PySpark program executed successfully.
* [ ] Spark History Server verified.

---

# CONCLUSION

You have now learned how to install and configure a local Apache Spark development environment on Windows using WSL Ubuntu.

Your environment includes:

```text
Python
  +
Java 17
  +
Apache Spark 3.5.5
  +
PySpark 3.5.5
  +
VS Code
  +
Spark History Server
```

You can now start learning:

* PySpark DataFrames.
* Spark SQL.
* Transformations and actions.
* Joins and aggregations.
* Reading and writing CSV, JSON, and Parquet files.
* ETL pipelines.
* Batch processing.
* Structured Streaming.

**Next step:** Practise reading a CSV file into a Spark DataFrame, transforming the data, and writing the results to Parquet.

---

**Author:** aforashwin

**Purpose:** Beginner-friendly Apache Spark and PySpark installation tutorial.

**Environment:** Windows + WSL Ubuntu + VS Code

