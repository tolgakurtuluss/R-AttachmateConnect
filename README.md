## 🖥️ Attachmate Extra Terminal Connection with R
This script uses the RDCOMClient library to connect to an Attachmate Extra terminal session.

## 📋 Prerequisites
Before running the script, you need to have the following:

* Attachmate Extra installed on your machine.
* RDCOMClient library installed in R.

## 🚀 Running the Script
To connect to the Attachmate Extra terminal session, follow these steps:

* Launch Attachmate Extra as a COM object using COMCreate("EXTRA.System").
* Get the sessions collection using extra$sessions.
* Connect to the first available session using sessions$open().
* Wait for the session to connect using session$Connected().
* Get the screen object for the session using session$screen.
* Wait for the screen to be ready using screen$WaitForHostReady().
* Set the screen size to 80x24 using screen$Columns(80) and screen$Rows(24).
* Send some commands to the terminal using screen$SendKeys().
* Wait for the terminal to finish processing the commands using screen$WaitForHostSettle().
* Disconnect from the session using session$disconnect().

## 📖 Example

```R code
library(RDCOMClient)

# Launch Attachmate Extra as a COM object
extra <- COMCreate("EXTRA.System")

# Get the sessions collection
sessions <- extra$sessions

# Connect to the first available session
session <- sessions$open()

# Wait for the session to connect
while (session$Connected() == FALSE) {
  Sys.sleep(0.1)
}

# Get the screen object for the session
screen <- session$screen

# Wait for the screen to be ready
while (screen$WaitForHostReady() == FALSE) {
  Sys.sleep(0.1)
}

# Set the screen size to 80x24
screen$Columns(80)
screen$Rows(24)

# Send some commands to the terminal
screen$SendKeys("USERID")
screen$SendKeys("{Tab}")
screen$SendKeys("PASSWORD")
screen$SendKeys("{Enter}")

# Wait for the terminal to finish processing the commands
while (screen$WaitForHostSettle(1000) == FALSE) {
  Sys.sleep(0.1)
}

# Disconnect from the session
session$disconnect()
```
## 📝 License
This script is licensed under the MIT License.
