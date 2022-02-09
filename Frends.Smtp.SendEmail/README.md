# Frends.SMTP.SendEmail


[![Frends.Smtp.SendEmail Main](https://github.com/FrendsPlatform/Frends.Smtp/actions/workflows/SendEmail_main.yml/badge.svg)](https://github.com/FrendsPlatform/Frends.Regex/actions/workflows/IsMatch_build_and_test_on_main.yml)
![MyGet](https://img.shields.io/myget/frends-tasks/v/Frends.Smtp.SendEmail?label=NuGet)
 ![GitHub](https://img.shields.io/github/license/FrendsPlatform/Frends.Smtp?label=License)
 ![Coverage](https://app-github-custom-badges.azurewebsites.net/Badge?key=FrendsPlatform/Frends.Smtp/Frends.Smtp.SendEmail|main)

Frends task for sending emails with SMTP. Task sends emails via SMTP protocol and can handle attachments either from file or as raw string input.

## Installing

You can install the Task via frends UI Task View or you can find the NuGet package from the following NuGet feed
https://www.myget.org/F/frends-tasks/api/v2.

## Task Parameters

### Message
Settings for message properties

| Property             | Type                 | Description                          | Example |
| ---------------------| ---------------------| ------------------------------------ | ----- |
| To | string | Recipient addresses separated by , or ; | jane.doe@somedomain.com |
| Cc | string | Cc recipient addresses separated by , or ; | jane.doe@somedomain.com |
| Bcc | string | Bcc recipient addresses separated by , or ; | jane.doe@somedomain.com |
| From | string | The email address the message is sent from | john.doe@somedomain.com |
| Sender Name | string | Name of the sender | Frends errors |
| Subject | string | Subject of the message | Hello Jane |
| Message | string | Body of the message | You've got mail! |
| Is message html | bool |  Indicates whether the mail message body is in Html | false |
| Message encoding| string | Encoding of message body and subject. Use following table's name column for other options. https://msdn.microsoft.com/en-us/library/system.text.encoding(v=vs.110).aspx#Anchor_5 | utf-8 |


### Attachments

Settings for included attachments

| Property             | Type                 | Description                          | Example |
| ---------------------| ---------------------| ------------------------------------ | ----- |
| Attachment type | enum { FileAttachment, AttachmentFromString } | Chooses if the attachment file is created from a string or copied from disk  | FileAttachment |
| File content | string |  Usable with Attachment type AttachmentFromString. Sets the content of the attachment file | Lorem ipsum... |
| File name | string | Usable with Attachment type AttachmentFromString. Sets the name of the attachment file | error.txt |
| File path | string | Usable with Attachment type FileAttachment. Attachment file's path. Uses Directory.GetFiles(string, string) as a pattern matching technique. See https://msdn.microsoft.com/en-us/library/wz42302f(v=vs.110).aspx. Exception: If the path ends in a directory, all files in that folder are added as attachments. | C:\\temp\\*.csv |
| Throw exception if attachment not found | bool | Usable with Attachment type FileAttachment. If set true and no files match the given path, an exception is thrown | true |
| Send if no attachments found | bool | Usable with Attachment type FileAttachment. If set true and no files match the given path, email will be sent nevertheless | false |

### SMTP Settings

Settings for connecting to SMTP server

| Property             | Type                 | Description                          | Example |
| ---------------------| ---------------------| ------------------------------------ | ----- |
| SMTP server | string | SMTP server address | smtp.somedomain.com |
| Port | int | SMTP server port | 25 |
| Use ssl| bool | Set this true if SMTP expects to be connected using SSL | false |
| Use windows authentication | bool | Set this true if you want to use windows authentication to authenticate to SMTP server | false |
| User name| string | Usable when windows authentication is set false. Use this username to log in to the SMTP server | user |
| Password | string | Usable when windows authentication is set false. Use this password to log in to the SMTP server | password |


## Returns

| Property             | Type                 | Description                          | Example |
| ---------------------| ---------------------| ------------------------------------ | ----- |
| EmailSent | bool | Returns true if email message has been sent | true |
| StatusString| string | Contains information about the task's result. | No attachments found matching path \"C:\\temp\\*.csv\". No email sent. |

## Building

Clone a copy of the repository

`git clone https://github.com/FrendsPlatform/Frends.SMTP.git`

Rebuild the project

`dotnet build`

Run tests

`dotnet test`

Create a NuGet package

`dotnet pack --configuration Release`

# Testing

## Unit Tests

Unit tests are run on each push and can be run manually by `dotnet test` command.

## Integration Tests

Integration tests in Frends.SMTP are run as part of unit test runs.

## Performance Tests

No performance tests are done in Frends.SMTP as the SMTP server itself is the main component during execution.

# Changelog

## [1.0.0] - 2022-02-09
### Added
- Initial implementation