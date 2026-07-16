As usual we start with functional and non-functional requirements.

![[namastedev.com_learn_namaste-frontend-system-design_hld-email-client.png]]

- SMTP (Simple mail transfer protocol) is the protocol generally used to send mails from one client to another client. Most email rules are defined by SMTP.
- POP (Post office protocol) - Mainly for older systems and incoming emails. It deletes the mail after being read. Client is a single client. After reading the mail, it gets deleted.
- IMAP (Internet message Access Protocol) - Does not delete the mail after reading the email. Useful when we want to retrieve mails from multiple sources.

![[namastedev.com_learn_namaste-frontend-system-design_hld-email-client 1.png]]

Differences between POP and IMAP.

![[namastedev.com_learn_namaste-frontend-system-design_hld-email-client 2.png]]


Architecture and flow 

![[namastedev.com_learn_namaste-frontend-system-design_hld-email-client 3.png]]

# Email Sending and Receiving Flow

## Components

- **MUA (Mail User Agent)** – The email client used by the user (Outlook, Gmail Web, Thunderbird, Apple Mail, etc.).
- **Mail Server** – Stores users' mailboxes and handles sending/receiving emails.
- **MTA (Mail Transfer Agent)** – Software on a mail server responsible for transferring emails between mail servers using SMTP.

---

## Email Sending Flow

1. User composes an email in an email client (MUA).
2. The client sends the email to its provider's web/application server using **HTTP/HTTPS** (if using webmail like Gmail or Outlook Web).
   - Desktop clients may directly use **SMTP** instead.
3. The provider's server submits the email to its **Mail Server (MTA)**.
4. The sender's Mail Server looks up the recipient domain's **MX (Mail Exchange) record** using DNS.
5. The sender's Mail Server sends the email to the recipient's Mail Server using **SMTP**.
6. The recipient's Mail Server stores the email in the recipient's mailbox.

---

## Email Receiving Flow

### Using Webmail (gmail.com, outlook.com)

1. The user opens the webmail application.
2. The browser communicates with the provider's web server using **HTTP/HTTPS**.
3. The web server retrieves the email from its backend mailbox storage.
4. The email is displayed in the browser.

> **Note:** Gmail Web does **not** use IMAP internally. The browser only communicates using HTTP/HTTPS.

---

### Using Desktop/Mobile Email Clients

1. The email client connects directly to the Mail Server.
2. It retrieves emails using:
   - **IMAP** (recommended)
   - **POP3** (older protocol)

---

## Protocols

### HTTP/HTTPS
- Used between the **web browser/app** and the **email provider's web server**.
- Used only for webmail interfaces.

### SMTP (Simple Mail Transfer Protocol)
- Used to **send emails**.
- Client → Mail Server
- Mail Server → Mail Server

### IMAP (Internet Message Access Protocol)
- Used to **retrieve and synchronize** emails.
- Emails remain on the server.
- Supports folders, multiple devices, read/unread status, etc.

### POP3 (Post Office Protocol v3)
- Used to **download** emails.
- Typically removes emails from the server after download.
- Best suited for a single device.

---

## Complete Flow

```
Sender (Outlook Web)
        │
     HTTP/HTTPS
        │
        ▼
Outlook Web Server
        │
       SMTP
        ▼
Outlook Mail Server (MTA)
        │
       SMTP
        ▼
Gmail Mail Server (MTA)
        │
   Stores Email
        │
        ├──────────────► Gmail Web
        │                  │
        │              HTTP/HTTPS
        │                  ▼
        │             Gmail Browser
        │
        └──────────────► Outlook/Thunderbird
                           │
                       IMAP / POP3
                           ▼
                     Desktop Client
```

---

## Key Points

- **SMTP = Sending emails**
- **IMAP/POP3 = Retrieving emails**
- **HTTP/HTTPS = Accessing webmail (Gmail, Outlook Web, Yahoo Mail, etc.)**
- **Mail Server ↔ Mail Server communication is always SMTP.**
- **Browsers never use IMAP or POP3 directly.**
- **Desktop email clients use IMAP/POP3 to fetch emails from mail servers.**