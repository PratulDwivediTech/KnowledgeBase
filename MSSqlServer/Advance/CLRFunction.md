# CLR Functions
- A CLR (Common Language Runtime) function in Microsoft SQL Server is a type of user-defined function that is written using a .NET language like C# or VB.NET, rather than T-SQL (Transact-SQL). SQL Server integrates with the .NET Framework, allowing you to run managed code directly within the SQL Server environment.
## Key Points about MS SQL CLR Functions:
- ### Purpose:
    CLR functions are typically used for complex calculations, operations that are not easily implemented in T-SQL, or when you need to leverage the full capabilities of the .NET Framework within SQL Server.
- ### Creating CLR Functions:
  - A CLR function is written in a .NET language, compiled into an assembly (DLL), and then registered with SQL Server.
  - After registering the assembly, you can create functions, procedures, triggers, or types within SQL Server that reference the methods within the assembly.
- ### Steps to Implement a CLR Function:
  - Step 1: Create a .NET Class Library project in Visual Studio.
  - Step 2: Write the function code in C# or VB.NET.
  - Step 3: Compile the code into a DLL.
  - Step 4: Register the assembly in SQL Server using the CREATE ASSEMBLY statement.
  - Step 5: Create the CLR function using the CREATE FUNCTION statement and reference the method from the registered assembly.
- ### Example
    - #### Simple Function
      ```csharp
        using System;
        using Microsoft.SqlServer.Server;
        
        public class SqlClrFunctions
        {
            [SqlFunction]
            public static int AddNumbers(int a, int b)
            {
                return a + b;
            }
        }
      ```
# Advance Functions:
Here are few advance function which may help you
## 1. EncryptText Function

### **Description:**
The `EncryptText` function encrypts a given string using the Rijndael encryption algorithm.

### **Use Case:**
This function is used when you need to securely encrypt sensitive data before storing it in a database or transmitting it over a network.

### **Input Parameters:**
- **value (string):** The text that needs to be encrypted.

### **Output:**
- **Encrypted text (SqlString):** The encrypted version of the input text.

### **Example:**
```sql
SELECT dbo.EncryptText('MySecretPassword')
```

---

## 2. DecryptText Function

### **Description:**
The `DecryptText` function decrypts a previously encrypted string using the Rijndael decryption algorithm.

### **Use Case:**
This function is used when you need to retrieve the original text from an encrypted string stored in a database.

### **Input Parameters:**
- **value (string):** The encrypted text that needs to be decrypted.

### **Output:**
- **Decrypted text (SqlString):** The original text after decryption.

### **Example:**
```sql
SELECT dbo.DecryptText('EncryptedText')
```

---

## 3. GetPlainText Function

### **Description:**
The `GetPlainText` function removes HTML tags and special characters from a given string.

### **Use Case:**
This function is useful when you need to sanitize text input by removing HTML tags and special characters.

### **Input Parameters:**
- **value (string):** The text from which HTML tags and special characters need to be removed.

### **Output:**
- **Plain text (SqlString):** The cleaned text with HTML tags and special characters removed.

### **Example:**
```sql
SELECT dbo.GetPlainText('<p>Hello World!</p>&nbsp;')
```

---

## 4. StringToBase64 Function

### **Description:**
The `StringToBase64` function converts a given string to its Base64 encoded representation.

### **Use Case:**
This function is used to encode binary data into a Base64 string for storage or transmission.

### **Input Parameters:**
- **value (string):** The text that needs to be converted to Base64.

### **Output:**
- **Base64 encoded text (SqlString):** The Base64 encoded version of the input text.

### **Example:**
```sql
SELECT dbo.StringToBase64('Hello World!')
```

---

## 5. GetHttpData Function

### **Description:**
The `GetHttpData` function retrieves the HTML content from a specified URL.

### **Use Case:**
This function is used to fetch the content of a web page for processing or storage.

### **Input Parameters:**
- **url (string):** The URL of the web page to retrieve.

### **Output:**
- **HTML content (SqlString):** The content of the web page as a string.

### **Example:**
```sql
SELECT dbo.GetHttpData('https://www.example.com')
```

---

## 6. GetHttpDataHeaders Function

### **Description:**
The `GetHttpDataHeaders` function retrieves the HTML content from a specified URL with custom headers.

### **Use Case:**
This function is used to fetch web page content while passing specific headers, such as authorization tokens or custom user-agents.

### **Input Parameters:**
- **url (string):** The URL of the web page to retrieve.
- **header (string):** The custom headers to include in the request.

### **Output:**
- **HTML content (SqlString):** The content of the web page as a string.

### **Example:**
```sql
SELECT dbo.GetHttpDataHeaders('https://www.example.com', 'Authorization: Bearer token;User-Agent: MyAgent')
```

---

## 7. PostHttpData Function

### **Description:**
The `PostHttpData` function sends a POST request to a specified URL with JSON data and custom headers.

### **Use Case:**
This function is used to send data to a web server via a POST request, such as submitting form data or triggering an API.

### **Input Parameters:**
- **url (string):** The URL of the web server to send the data to.
- **header (string):** The custom headers to include in the request.
- **data (string):** The JSON data to send in the POST request.

### **Output:**
- **Response (SqlString):** The response from the server.

### **Example:**
```sql
SELECT dbo.PostHttpData('https://www.example.com/api', 'Authorization: Bearer token', '{"key":"value"}')
```

---

## 8. PostHttpFormData Function

### **Description:**
The `PostHttpFormData` function sends a POST request to a specified URL with form data and custom headers.

### **Use Case:**
This function is used to submit form data to a web server via a POST request.

### **Input Parameters:**
- **url (string):** The URL of the web server to send the data to.
- **header (string):** The custom headers to include in the request.
- **data (string):** The form data to send in the POST request.

### **Output:**
- **Response (SqlString):** The response from the server.

### **Example:**
```sql
SELECT dbo.PostHttpFormData('https://www.example.com/form', 'Authorization: Bearer token', 'field1=value1&field2=value2')
```

---

## 9. SendMail Function

### **Description:**
The `SendMail` function sends an email using the specified SMTP server.

### **Use Case:**
This function is used to send emails from a SQL Server environment, such as sending notifications or reports.

### **Input Parameters:**
- **EMailHost (string):** The SMTP server to use for sending the email.
- **FromName (string):** The display name of the sender.
- **FromEmailId (string):** The email address of the sender.
- **LoginPassword (string):** The password for the sender's email account.
- **Port (int):** The port number to use for the SMTP server.
- **IsSSL (bool):** Whether to use SSL for the SMTP connection.
- **EmailTo (string):** The recipient's email address.
- **EmailCC (string):** The CC recipient's email address.
- **EmailBCC (string):** The BCC recipient's email address.
- **ReplyTo (string):** The Reply-To email address.
- **EmailSubject (string):** The subject of the email.
- **EmailBody (string):** The body of the email.
- **AttachmentBytes (string):** The attachment data in hexadecimal format.
- **LogId (int):** The log ID for tracking email status.

### **Output:**
- **Status (SqlString):** The status of the email send operation.

### **Example:**
```sql
SELECT dbo.SendMail('smtp.example.com', 'Sender Name', 'sender@example.com', 'password', 587, 1, 'recipient@example.com', '', '', '', 'Subject', 'Body', '', 1)
```

---

## 10. UspSendMail Procedure

### **Description:**
The `UspSendMail` procedure sends an email using the specified SMTP server, similar to the `SendMail` function, but as a stored procedure.

### **Use Case:**
This procedure is used to send emails with the option to return an output parameter indicating the status of the operation.

### **Input Parameters:**
- **EMailHost (string):** The SMTP server to use for sending the email.
- **FromName (string):** The display name of the sender.
- **FromEmailId (string):** The email address of the sender.
- **Password (string):** The password for the sender's email account.
- **Port (int):** The port number to use for the SMTP server.
- **IsSSL (bool):** Whether to use SSL for the SMTP connection.
- **EmailTo (string):** The recipient's email address.
- **EmailCC (string):** The CC recipient's email address.
- **EmailBCC (string):** The BCC recipient's email address.
- **ReplyTo (string):** The Reply-To email address.
- **EmailSubject (string):** The subject of the email.
- **EmailBody (string):** The body of the email.
- **AttachmentBytes (string):** The attachment data in hexadecimal format.
- **FileName (string):** The name of the attachment file.
- **LogId (int):** The log ID for tracking email status.
- **ReturnValue (out string):** The output parameter indicating the status of the email send operation.

### **Output:**
- **ReturnValue (string):** The status of the email send operation.

### **Example:**
```sql
DECLARE @ReturnValue NVARCHAR(MAX);
EXEC dbo.UspSendMail 'smtp.example.com', 'Sender Name', 'sender@example.com', 'password', 587, 1, 'recipient@example.com', '', '', '', 'Subject', 'Body', '', 'attachment.pdf', 1, @ReturnValue OUT;
PRINT @ReturnValue;
```



