---
title: "SqlClient 스트리밍 지원 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c449365b-470b-4edb-9d61-8353149f5531
caps.latest.revision: 14
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 14
---
# SqlClient 스트리밍 지원
[!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]와 응용 프로그램 간의 스트리밍 지원\([!INCLUDE[net_v45](../../../../includes/net-v45-md.md)]의 새로운 기능\)을 통해 서버 측의 구조화되지 않은 데이터\(문서, 이미지 및 미디어 파일\)가 지원됩니다.  [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 데이터베이스는 BLOB\(Binary Large Object\)를 저장할 수 있지만 BLOB를 검색할 때 많은 메모리가 사용될 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]로의 스트리밍과 그 반대로의 스트리밍이 지원되면 데이터를 메모리에 완전하게 로드하지 않고 데이터를 스트리밍함으로써 메모리 오버플로 예외가 보다 적게 발생하는 응용 프로그램을 간단하게 작성할 수 있습니다.  
  
 또한 스트리밍 지원을 통해 중간 계층 응용 프로그램의 확장성이 높아질 수 있습니다. 특히 대형 BLOB를 전송, 검색 및 조작하기 위해 비즈니스 개체를 SQL Azure에 연결하는 시나리오에서는 더욱 그렇습니다.  
  
> [!WARNING]
>  응용 프로그램에서 `Context Connection` 연결 문자열 키워드도 사용하는 경우에는 비동기 호출이 지원되지 않습니다.  
>   
>  스트리밍을 지원하기 위해 추가된 멤버는 쿼리에서 데이터를 검색하고 쿼리 및 저장 프로시저에 매개 변수를 전달하는 데 사용됩니다.  스트리밍 기능은 기본 OLTP 및 데이터 마이그레이션 시나리오를 처리하며 온\-프레미스 및 오프\-프레미스 데이터 마이그레이션 환경에 적용할 수 있습니다.  
  
## [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]에서의 스트리밍 지원  
 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]에서의 스트리밍 지원은 <xref:System.Data.Common.DbDataReader> 및 <xref:System.Data.SqlClient.SqlDataReader> 클래스에 새로운 기능을 도입함으로써 <xref:System.IO.Stream>, <xref:System.Xml.XmlReader> 및 <xref:System.IO.TextReader> 개체를 가져오고 이러한 개체에 반응할 수 있습니다.  이러한 클래스는 쿼리에서 데이터를 검색하는 데 사용됩니다.  따라서 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]에서의 스트리밍 지원은 OLTP 시나리오를 처리하며 온\-프레미스 및 오프\-프레미스 환경에 적용됩니다.  
  
 <xref:System.Data.SqlClient.SqlDataReader>에서의 스트리밍 지원을 활성화하기 위해 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]에 추가된 메서드는 다음과 같습니다.  
  
1.  <xref:System.Data.SqlClient.SqlDataReader.IsDBNullAsync%2A>  
  
2.  <xref:System.Data.SqlClient.SqlDataReader.GetFieldValue%2A?displayProperty=fullName>  
  
3.  <xref:System.Data.SqlClient.SqlDataReader.GetFieldValueAsync%2A>  
  
4.  <xref:System.Data.SqlClient.SqlDataReader.GetStream%2A>  
  
5.  <xref:System.Data.SqlClient.SqlDataReader.GetTextReader%2A>  
  
6.  <xref:System.Data.SqlClient.SqlDataReader.GetXmlReader%2A>  
  
 <xref:System.Data.Common.DbDataReader>에서의 스트리밍 지원을 활성화하기 위해 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]에 추가된 메서드는 다음과 같습니다.  
  
1.  <xref:System.Data.Common.DbDataReader.GetFieldValue%2A>  
  
2.  <xref:System.Data.Common.DbDataReader.GetStream%2A>  
  
3.  <xref:System.Data.Common.DbDataReader.GetTextReader%2A>  
  
## [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]로의 스트리밍 지원  
 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]로의 스트리밍 지원은 <xref:System.Data.SqlClient.SqlParameter> 클래스에 새로운 기능을 도입함으로써 <xref:System.Xml.XmlReader>, <xref:System.IO.Stream> 및 <xref:System.IO.TextReader> 개체를 받아들이고 이러한 개체에 반응할 수 있습니다.  <xref:System.Data.SqlClient.SqlParameter>는 쿼리 및 저장 프로시저에 매개 변수를 전달하는 데 사용됩니다.  
  
 <xref:System.Data.SqlClient.SqlCommand> 개체를 삭제하거나 <xref:System.Data.SqlClient.SqlCommand.Cancel%2A>을 호출할 때는 모든 스트리밍 작업이 취소되어야 합니다.  응용 프로그램에서 <xref:System.Threading.CancellationToken>을 전송하면 취소되지 않을 수 있습니다.  
  
 다음 <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> 형식에서는 <xref:System.Data.SqlClient.SqlParameter.Value%2A>의 <xref:System.IO.Stream>를 받아들입니다.  
  
-   **Binary**  
  
-   **VarBinary**  
  
 다음 <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> 형식에서는 <xref:System.Data.SqlClient.SqlParameter.Value%2A>의 <xref:System.IO.TextReader>를 받아들입니다.  
  
-   **Char**  
  
-   **NChar**  
  
-   **NVarChar**  
  
-   **Xml**  
  
 **Xml** <xref:System.Data.SqlClient.SqlParameter.SqlDbType%2A> 형식에서는 <xref:System.Data.SqlClient.SqlParameter.Value%2A>의 <xref:System.Xml.XmlReader>를 받아들입니다.  
  
 <xref:System.Data.SqlClient.SqlParameter.SqlValue%2A>는 <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader> 및 <xref:System.IO.Stream> 형식의 값만 받아들일 수 있습니다.  
  
 <xref:System.Xml.XmlReader>, <xref:System.IO.TextReader> 및 <xref:System.IO.Stream> 개체는 <xref:System.Data.SqlClient.SqlParameter.Size%2A>에 정의된 값까지 전송됩니다.  
  
## 샘플 \- [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]에서의 스트리밍  
 다음 [!INCLUDE[tsql](../../../../includes/tsql-md.md)]에 따라 샘플 데이터베이스를 작성할 수 있습니다.  
  
```  
CREATE DATABASE [Demo]  
GO  
USE [Demo]  
GO  
CREATE TABLE [Streams] (  
[id] INT PRIMARY KEY IDENTITY(1, 1),  
[textdata] NVARCHAR(MAX),  
[bindata] VARBINARY(MAX),  
[xmldata] XML)  
GO  
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'This is a test', 0x48656C6C6F, N'<test>value</test>')  
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'Hello, World!', 0x54657374696E67, N'<test>value2</test>')  
INSERT INTO [Streams] (textdata, bindata, xmldata) VALUES (N'Another row', 0x666F6F626172, N'<fff>bbb</fff><fff>bbc</fff>')  
GO  
```  
  
 이 샘플에서는 다음 작업의 수행 방법을 보여 줍니다.  
  
-   큰 파일을 검색하는 비동기적 방법을 제공하여 사용자 인터페이스 스레드의 차단을 방지합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]를 통해 [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)]에서 큰 텍스트 파일을 전송합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]를 통해 [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)]에서 큰 XML 파일을 전송합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]에서 데이터를 검색합니다.  
  
-   메모리를 지나치게 소모하지 않으면서 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 데이터베이스 간에 큰 파일\(BLOB\)을 전송합니다.  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.IO;  
using System.Threading.Tasks;  
using System.Xml;  
  
namespace StreamingFromServer {  
   class Program {  
      // Replace the connection string if needed, for instance to connect to SQL Express: @"Server=(local)\SQLEXPRESS;Database=Demo;Integrated Security=true"  
      private const string connectionString = @"Server=(localdb)\V11.0;Database=Demo";  
  
      static void Main(string[] args) {  
         CopyBinaryValueToFile().Wait();  
         PrintTextValues().Wait();  
         PrintXmlValues().Wait();  
         PrintXmlValuesViaNVarChar().Wait();  
  
         Console.WriteLine("Done");  
      }  
  
      // Application retrieving a large BLOB from SQL Server in .NET 4.5 using the new asynchronous capability  
      private static async Task CopyBinaryValueToFile() {  
         string filePath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.MyDocuments), "binarydata.bin");  
  
         using (SqlConnection connection = new SqlConnection(connectionString)) {  
            await connection.OpenAsync();  
            using (SqlCommand command = new SqlCommand("SELECT [bindata] FROM [Streams] WHERE [id]=@id", connection)) {  
               command.Parameters.AddWithValue("id", 1);  
  
               // The reader needs to be executed with the SequentialAccess behavior to enable network streaming  
               // Otherwise ReadAsync will buffer the entire BLOB into memory which can cause scalability issues or even OutOfMemoryExceptions  
               using (SqlDataReader reader = await command.ExecuteReaderAsync(CommandBehavior.SequentialAccess)) {  
                  if (await reader.ReadAsync()) {  
                     if (!(await reader.IsDBNullAsync(0))) {  
                        using (FileStream file = new FileStream(filePath, FileMode.Create, FileAccess.Write)) {  
                           using (Stream data = reader.GetStream(0)) {  
  
                              // Asynchronously copy the stream from the server to the file we just created  
                              await data.CopyToAsync(file);  
                           }  
                        }  
                     }  
                  }  
               }  
            }  
         }  
      }  
  
      // Application transferring a large Text File from SQL Server in .NET 4.5  
      private static async Task PrintTextValues() {  
         using (SqlConnection connection = new SqlConnection(connectionString)) {  
            await connection.OpenAsync();  
            using (SqlCommand command = new SqlCommand("SELECT [id], [textdata] FROM [Streams]", connection)) {  
  
               // The reader needs to be executed with the SequentialAccess behavior to enable network streaming  
               // Otherwise ReadAsync will buffer the entire text document into memory which can cause scalability issues or even OutOfMemoryExceptions  
               using (SqlDataReader reader = await command.ExecuteReaderAsync(CommandBehavior.SequentialAccess)) {  
                  while (await reader.ReadAsync()) {  
                     Console.Write("{0}: ", reader.GetInt32(0));  
  
                     if (await reader.IsDBNullAsync(1)) {  
                        Console.Write("(NULL)");  
                     }  
                     else {  
                        char[] buffer = new char[4096];  
                        int charsRead = 0;  
                        using (TextReader data = reader.GetTextReader(1)) {  
                           do {  
                              // Grab each chunk of text and write it to the console  
                              // If you are writing to a TextWriter you should use WriteAsync or WriteLineAsync  
                              charsRead = await data.ReadAsync(buffer, 0, buffer.Length);  
                              Console.Write(buffer, 0, charsRead);  
                           } while (charsRead > 0);  
                        }  
                     }  
  
                     Console.WriteLine();  
                  }  
               }  
            }  
         }  
      }  
  
      // Application transferring a large Xml Document from SQL Server in .NET 4.5  
      private static async Task PrintXmlValues() {  
         using (SqlConnection connection = new SqlConnection(connectionString)) {  
            await connection.OpenAsync();  
            using (SqlCommand command = new SqlCommand("SELECT [id], [xmldata] FROM [Streams]", connection)) {  
  
               // The reader needs to be executed with the SequentialAccess behavior to enable network streaming  
               // Otherwise ReadAsync will buffer the entire Xml Document into memory which can cause scalability issues or even OutOfMemoryExceptions  
               using (SqlDataReader reader = await command.ExecuteReaderAsync(CommandBehavior.SequentialAccess)) {  
                  while (await reader.ReadAsync()) {  
                     Console.WriteLine("{0}: ", reader.GetInt32(0));  
  
                     if (await reader.IsDBNullAsync(1)) {  
                        Console.WriteLine("\t(NULL)");  
                     }  
                     else {  
                        using (XmlReader xmlReader = reader.GetXmlReader(1)) {  
                           int depth = 1;  
                           // NOTE: The XmlReader returned by GetXmlReader does NOT support async operations  
                           // See the example below (PrintXmlValuesViaNVarChar) for how to get an XmlReader with asynchronous capabilities  
                           while (xmlReader.Read()) {  
                              switch (xmlReader.NodeType) {  
                                 case XmlNodeType.Element:  
                                    Console.WriteLine("{0}<{1}>", new string('\t', depth), xmlReader.Name);  
                                    depth++;  
                                    break;  
                                 case XmlNodeType.Text:  
                                    Console.WriteLine("{0}{1}", new string('\t', depth), xmlReader.Value);  
                                    break;  
                                 case XmlNodeType.EndElement:  
                                    depth--;  
                                    Console.WriteLine("{0}</{1}>", new string('\t', depth), xmlReader.Name);  
                                    break;  
                              }  
                           }  
                        }  
                     }  
                  }  
               }  
            }  
         }  
      }  
  
      // Application transferring a large Xml Document from SQL Server in .NET 4.5  
      // This goes via NVarChar and TextReader to enable asynchronous reading  
      private static async Task PrintXmlValuesViaNVarChar() {  
         XmlReaderSettings xmlSettings = new XmlReaderSettings() {  
            // Async must be explicitly enabled in the XmlReaderSettings otherwise the XmlReader will throw exceptions when async methods are called  
            Async = true,  
            // Since we will immediately wrap the TextReader we are creating in an XmlReader, we will permit the XmlReader to take care of closing\disposing it  
            CloseInput = true,  
            // If the Xml you are reading is not a valid document (as per http://msdn.microsoft.com/library/6bts1x50.aspx) you will need to set the conformance level to Fragment  
            ConformanceLevel = ConformanceLevel.Fragment  
         };  
  
         using (SqlConnection connection = new SqlConnection(connectionString)) {  
            await connection.OpenAsync();  
  
            // Cast the XML into NVarChar to enable GetTextReader - trying to use GetTextReader on an XML type will throw an exception  
            using (SqlCommand command = new SqlCommand("SELECT [id], CAST([xmldata] AS NVARCHAR(MAX)) FROM [Streams]", connection)) {  
  
               // The reader needs to be executed with the SequentialAccess behavior to enable network streaming  
               // Otherwise ReadAsync will buffer the entire Xml Document into memory which can cause scalability issues or even OutOfMemoryExceptions  
               using (SqlDataReader reader = await command.ExecuteReaderAsync(CommandBehavior.SequentialAccess)) {  
                  while (await reader.ReadAsync()) {  
                     Console.WriteLine("{0}:", reader.GetInt32(0));  
  
                     if (await reader.IsDBNullAsync(1)) {  
                        Console.WriteLine("\t(NULL)");  
                     }  
                     else {  
                        // Grab the row as a TextReader, then create an XmlReader on top of it  
                        // We are not keeping a reference to the TextReader since the XmlReader is created with the "CloseInput" setting (so it will close the TextReader when needed)  
                        using (XmlReader xmlReader = XmlReader.Create(reader.GetTextReader(1), xmlSettings)) {  
                           int depth = 1;  
                           // The XmlReader above now supports asynchronous operations, so we can use ReadAsync here  
                           while (await xmlReader.ReadAsync()) {  
                              switch (xmlReader.NodeType) {  
                                 case XmlNodeType.Element:  
                                    Console.WriteLine("{0}<{1}>", new string('\t', depth), xmlReader.Name);  
                                    depth++;  
                                    break;  
                                 case XmlNodeType.Text:  
                                    // Depending on what your data looks like, you should either use Value or GetValueAsync  
                                    // Value has less overhead (since it doesn't create a Task), but it may also block if additional data is required  
                                    Console.WriteLine("{0}{1}", new string('\t', depth), await xmlReader.GetValueAsync());  
                                    break;  
                                 case XmlNodeType.EndElement:  
                                    depth--;  
                                    Console.WriteLine("{0}</{1}>", new string('\t', depth), xmlReader.Name);  
                                    break;  
                              }  
                           }  
                        }  
                     }  
                  }  
               }  
            }  
         }  
      }  
   }  
}  
  
```  
  
## 샘플 \- [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]로의 스트리밍  
 다음 [!INCLUDE[tsql](../../../../includes/tsql-md.md)]에 따라 샘플 데이터베이스를 작성할 수 있습니다.  
  
```  
CREATE DATABASE [Demo2]  
GO  
USE [Demo2]  
GO  
CREATE TABLE [BinaryStreams] (  
[id] INT PRIMARY KEY IDENTITY(1, 1),  
[bindata] VARBINARY(MAX))  
GO  
CREATE TABLE [TextStreams] (  
[id] INT PRIMARY KEY IDENTITY(1, 1),  
[textdata] NVARCHAR(MAX))  
GO  
CREATE TABLE [BinaryStreamsCopy] (  
[id] INT PRIMARY KEY IDENTITY(1, 1),  
[bindata] VARBINARY(MAX))  
GO  
```  
  
 이 샘플에서는 다음 작업의 수행 방법을 보여 줍니다.  
  
-   [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]를 통해 [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)]로 큰 BLOB를 전송합니다.  
  
-   [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]를 통해 [!INCLUDE[net_v45](../../../../includes/net-v45-md.md)]로 큰 텍스트 파일을 전송합니다.  
  
-   새로운 비동기 기능을 사용하여 큰 BLOB를 전송합니다.  
  
-   새로운 비동기 기능과 await 키워드를 사용하여 큰 BLOB를 전송합니다.  
  
-   큰 BLOB의 전송을 취소합니다.  
  
-   새로운 비동기 기능을 사용하여 하나의 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 간에 스트리밍합니다.  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.IO;  
using System.Threading;  
using System.Threading.Tasks;  
  
namespace StreamingToServer {  
   class Program {  
      // Replace the connection string if needed, for instance to connect to SQL Express: @"Server=(local)\SQLEXPRESS;Database=Demo2;Integrated Security=true"  
      private const string connectionString = @"Server=(localdb)\V11.0;Database=Demo2";  
  
      static void Main(string[] args) {  
         CreateDemoFiles();  
  
         StreamBLOBToServer().Wait();  
         StreamTextToServer().Wait();  
  
         // Create a CancellationTokenSource that will be cancelled after 100ms  
         // Typically this token source will be cancelled by a user request (e.g. a Cancel button)  
         CancellationTokenSource tokenSource = new CancellationTokenSource();  
         tokenSource.CancelAfter(100);  
         try {  
            CancelBLOBStream(tokenSource.Token).Wait();  
         }  
         catch (AggregateException ex) {  
            // Cancelling an async operation will throw an exception  
            // Since we are using the Task's Wait method, this exception will be wrapped in an AggregateException  
            // If you were using the 'await' keyword, the compiler would take care of unwrapping the AggregateException  
            // Depending on when the cancellation occurs, you can either get an error from SQL Server or from .Net  
            if ((ex.InnerException is SqlException) || (ex.InnerException is TaskCanceledException)) {  
               // This is an expected exception  
               Console.WriteLine("Got expected exception: {0}", ex.InnerException.Message);  
            }  
            else {  
               // Did not expect this exception - re-throw it  
               throw;  
            }  
         }  
  
         Console.WriteLine("Done");  
      }  
  
      // This is used to generate the files which are used by the other sample methods  
      private static void CreateDemoFiles() {  
         Random rand = new Random();  
         byte[] data = new byte[1024];  
         rand.NextBytes(data);  
  
         using (FileStream file = File.Open("binarydata.bin", FileMode.Create)) {  
            file.Write(data, 0, data.Length);  
         }  
  
         using (StreamWriter writer = new StreamWriter(File.Open("textdata.txt", FileMode.Create))) {  
            writer.Write(Convert.ToBase64String(data));  
         }  
      }  
  
      // Application transferring a large BLOB to SQL Server in .Net 4.5  
      private static async Task StreamBLOBToServer() {  
         using (SqlConnection conn = new SqlConnection(connectionString)) {  
            await conn.OpenAsync();  
            using (SqlCommand cmd = new SqlCommand("INSERT INTO [BinaryStreams] (bindata) VALUES (@bindata)", conn)) {  
               using (FileStream file = File.Open("binarydata.bin", FileMode.Open)) {  
  
                  // Add a parameter which uses the FileStream we just opened  
                  // Size is set to -1 to indicate "MAX"  
                  cmd.Parameters.Add("@bindata", SqlDbType.Binary, -1).Value = file;  
  
                  // Send the data to the server asynchronously  
                  await cmd.ExecuteNonQueryAsync();  
               }  
            }  
         }  
      }  
  
      // Application transferring a large Text File to SQL Server in .Net 4.5  
      private static async Task StreamTextToServer() {  
         using (SqlConnection conn = new SqlConnection(connectionString)) {  
            await conn.OpenAsync();  
            using (SqlCommand cmd = new SqlCommand("INSERT INTO [TextStreams] (textdata) VALUES (@textdata)", conn)) {  
               using (StreamReader file = File.OpenText("textdata.txt")) {  
  
                  // Add a parameter which uses the StreamReader we just opened  
                  // Size is set to -1 to indicate "MAX"  
                  cmd.Parameters.Add("@textdata", SqlDbType.NVarChar, -1).Value = file;  
  
                  // Send the data to the server asynchronously  
                  await cmd.ExecuteNonQueryAsync();  
               }  
            }  
         }  
      }  
  
      // Cancelling the transfer of a large BLOB  
      private static async Task CancelBLOBStream(CancellationToken cancellationToken) {  
         using (SqlConnection conn = new SqlConnection(connectionString)) {  
            // We can cancel not only sending the data to the server, but also opening the connection  
            await conn.OpenAsync(cancellationToken);  
  
            // Artifically delay the command by 100ms  
            using (SqlCommand cmd = new SqlCommand("WAITFOR DELAY '00:00:00:100';INSERT INTO [BinaryStreams] (bindata) VALUES (@bindata)", conn)) {  
               using (FileStream file = File.Open("binarydata.bin", FileMode.Open)) {  
  
                  // Add a parameter which uses the FileStream we just opened  
                  // Size is set to -1 to indicate "MAX"  
                  cmd.Parameters.Add("@bindata", SqlDbType.Binary, -1).Value = file;  
  
                  // Send the data to the server asynchronously  
                  // Pass the cancellation token such that the command will be cancelled if needed  
                  await cmd.ExecuteNonQueryAsync(cancellationToken);  
               }  
            }  
         }  
      }  
   }  
}  
  
```  
  
## 샘플 \- 한 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]에서 다른 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]로의 스트리밍  
 이 샘플에서는 [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] 간에 큰 BLOB를 비동기적으로 스트리밍하는 방법을 보여 줍니다.  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
using System.IO;  
using System.Threading;  
using System.Threading.Tasks;  
  
namespace StreamingFromServerToAnother {  
   class Program {  
      // Replace the connection string if needed, for instance to connect to SQL Express: @"Server=(local)\SQLEXPRESS;Database=Demo2;Integrated Security=true"  
      private const string connectionString = @"Server=(localdb)\V11.0;Database=Demo2";  
  
      static void Main(string[] args) {  
         // For this example, we don't want to cancel  
         // So we can pass in a "blank" cancellation token  
         E2EStream(CancellationToken.None).Wait();  
  
         Console.WriteLine("Done");  
      }  
  
      // Streaming from one SQL Server to Another One using the new Async.NET  
      private static async Task E2EStream(CancellationToken cancellationToken) {  
         using (SqlConnection readConn = new SqlConnection(connectionString)) {  
            using (SqlConnection writeConn = new SqlConnection(connectionString)) {  
  
               // Note that we are using the same cancellation token for calls to both connections\commands  
               // Also we can start both the connection opening asynchronously, and then wait for both to complete  
               Task openReadConn = readConn.OpenAsync(cancellationToken);  
               Task openWriteConn = writeConn.OpenAsync(cancellationToken);  
               await Task.WhenAll(openReadConn, openWriteConn);  
  
               using (SqlCommand readCmd = new SqlCommand("SELECT [bindata] FROM [BinaryStreams]", readConn)) {  
                  using (SqlCommand writeCmd = new SqlCommand("INSERT INTO [BinaryStreamsCopy] (bindata) VALUES (@bindata)", writeConn)) {  
  
                     // Add an empty parameter to the write command which will be used for the streams we are copying  
                     // Size is set to -1 to indicate "MAX"  
                     SqlParameter streamParameter = writeCmd.Parameters.Add("@bindata", SqlDbType.Binary, -1);  
  
                     // The reader needs to be executed with the SequentialAccess behavior to enable network streaming  
                     // Otherwise ReadAsync will buffer the entire BLOB into memory which can cause scalability issues or even OutOfMemoryExceptions  
                     using (SqlDataReader reader = await readCmd.ExecuteReaderAsync(CommandBehavior.SequentialAccess, cancellationToken)) {  
                        while (await reader.ReadAsync(cancellationToken)) {  
                           // Grab a stream to the binary data in the source database  
                           using (Stream dataStream = reader.GetStream(0)) {  
  
                              // Set the parameter value to the stream source that was opened  
                              streamParameter.Value = dataStream;  
  
                              // Asynchronously send data from one database to another  
                              await writeCmd.ExecuteNonQueryAsync(cancellationToken);  
                           }  
                        }  
                     }  
                  }  
               }  
            }  
         }  
      }  
   }  
}  
  
```  
  
## 참고 항목  
 [ADO.NET에서 데이터 검색 및 수정](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)