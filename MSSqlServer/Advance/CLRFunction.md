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
## 1. Function: EncryptText
This function encrypts a given string using key and return encrypted string   
### Use Case:
- Scenario: Securely storing sensitive information such as passwords in the database.
- Purpose: Encrypt a plain text string using encryption before storing it.
### Usage: 
```sql

SELECT dbo.EncryptText('SensitiveData') ;

```sql
