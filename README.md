
# Automated email sender with contact management

## Overview

This project automates the process of sending personalized emails to a list of contacts while ensuring no duplicate emails are sent to the same recipient. The script supports:
- **Reading a contact list** from an Excel file.
- **Creating email addresses** dynamically if not already provided.
- **Tracking sent emails** to avoid duplicates using a `reached.csv` file.
- **Sending personalized emails** with attachments.

## Features

1. **Dynamic Email Generation**:
   - If a contact does not have an email address, the script generates one based on their name and associated company domain.
   - Email domains are mapped using a predefined dictionary for company names.

2. **Duplicate Contact Tracking**:
   - The script maintains a `reached.csv` file, which tracks all previously contacted individuals. If a recipient is already in this file, they are skipped.

3. **Email Personalization**:
   - Each email includes a personalized body that addresses the recipient by name.

4. **Attachment Support**:
   - A specified file (e.g., resume) is attached to each email.

## Prerequisites

Before running the script, ensure you have the following:
1. **Python 3.8+** installed on your machine.
2. The following Python libraries:
   - `pandas` for data handling.
   - `smtplib` for sending emails.
   - `email.mime` for email composition.
3. An email account with SMTP access (e.g., Gmail).
   - **Note**: If using Gmail, you may need to enable "Less Secure Apps" or generate an app password for your account.

## File Structure

- **contacts.xlsx**: Input file containing contact details with the following columns:
  - `Name`: Full name of the contact (e.g., "John Smith").
  - `Email`: Email address of the contact (optional; will be generated if missing).
  - `Company`: Name of the contact's company.
  
- **reached.csv**: File to track already contacted individuals. Contains:
  - `Name`: Full name of the contact.
  - `Email`: Email address of the contact.
  - `Company`: Company name (optional).

- **Resume.pdf**: The file to be attached to each email.

## How It Works

1. **Load Data**:
   - Reads the contact list from `contacts.xlsx`.
   - Reads the list of already contacted individuals from `reached.csv` (if it exists).

2. **Generate Missing Emails**:
   - For contacts without an email, the script generates one using the format:
     ```
     first.last@companydomain.com
     ```
     - `first` and `last` are derived from the `Name` column.
     - `companydomain.com` is retrieved from the `companies` dictionary.

3. **Filter Duplicate Contacts**:
   - Skips sending an email if the recipient's name or email is already in `reached.csv`.

4. **Compose and Send Emails**:
   - Personalizes the email body with the recipient's name and company.
   - Sends the email with the specified attachment.

5. **Update the `reached.csv` File**:
   - After sending each email, the recipient's information is added to `reached.csv`.

## Setup and Usage

1. **Clone the Repository**:
   ```bash
   git clone <repository_url>
   cd <repository_directory>

